# OpenVPN Setup Guide

## Overview

This document describes the installation and configuration of the OpenVPN server used in the Enterprise SOC Monitoring & Incident Response Home Lab.

The server provides secure remote access from the AWS-hosted Kali Linux attacker machine to the isolated VMware lab network, simulating a corporate VPN gateway.

---

# Environment

| Item             | Value             |
| ---------------- | ----------------- |
| Operating System | Ubuntu Server LTS |
| VPN Software     | OpenVPN           |
| PKI              | Easy-RSA          |
| Internal Network | 192.168.10.0/24   |
| VPN Network      | 10.8.0.0/24       |
| VPN Server IP    | 10.8.0.1          |

---

# Install OpenVPN

Update the system:

```bash
sudo apt update && sudo apt upgrade -y
```

Install OpenVPN and Easy-RSA:

```bash
sudo apt install openvpn easy-rsa -y
```

Verify installation:

```bash
openvpn --version
```

---

# Configure Public Key Infrastructure (PKI)

Create the Easy-RSA directory:

```bash
make-cadir ~/easy-rsa
```

Navigate to the directory:

```bash
cd ~/easy-rsa
```

Initialize the PKI:

```bash
./easyrsa init-pki
```

Build the Certificate Authority:

```bash
./easyrsa build-ca
```

Generate the server certificate:

```bash
./easyrsa build-server-full server nopass
```

Generate the client certificate:
replace `CLIENT_NAME` with your client name

```bash
./easyrsa build-client-full CLIENT_NAME nopass
```

Generate Diffie-Hellman parameters:

```bash
./easyrsa gen-dh
```

Generate the TLS authentication key:

```bash
openvpn --genkey secret ta.key
```
---

# Copy Certificates to OpenVPN Server Directory

Before starting OpenVPN, you MUST copy all generated keys to the OpenVPN server path.

Copy files:

```bash
sudo cp ~/easy-rsa/pki/ca.crt /etc/openvpn/server/
sudo cp ~/easy-rsa/pki/issued/server.crt /etc/openvpn/server/
sudo cp ~/easy-rsa/pki/private/server.key /etc/openvpn/server/
sudo cp ~/easy-rsa/pki/dh.pem /etc/openvpn/server/
sudo cp ~/easy-rsa/ta.key /etc/openvpn/server/
```

---

# Configure OpenVPN Server

Copy the sample configuration:

```bash
sudo cp /usr/share/doc/openvpn/examples/sample-config-files/server.conf /etc/openvpn/server/
```

Edit the configuration:

```bash
sudo nano /etc/openvpn/server/server.conf
```

 Protocol Configuration:

If UDP VPN is blocked in your country like me, switch OpenVPN to TCP.

Replace:

```text
proto udp
```
with:

```text
proto tcp
```

Configure the VPN network:

```text
server 10.8.0.0 255.255.255.0
```

Push the internal route:

```text
push "route 192.168.10.0 255.255.255.0"
```

Enable client-to-client communication:

```text
client-to-client
```

Certificate Paths (use absolute paths)
```text
ca /etc/openvpn/server/ca.crt
cert /etc/openvpn/server/server.crt
key /etc/openvpn/server/server.key
dh /etc/openvpn/server/dh.pem
```

Enable TLS Authentication (tls-auth)
```text
tls-auth /etc/openvpn/server/ta.key 0
```
Set HMAC Authentication Algorithm (auth)
This is critical – both server and client must use the same algorithm.
Add the following line right after tls-auth:

```text
auth SHA512
```
Without this, OpenVPN defaults to SHA1, which will cause a TLS handshake failure if the client expects a different hash (e.g. SHA512).

(Optional) Allow Modern and Legacy Ciphers
To ensure compatibility with clients using AES-256-GCM (modern) or AES-256-CBC (legacy), uncomment this line (remove the leading";"):

```text
data-ciphers AES-256-GCM:AES-128-GCM:?CHACHA20-POLY1305:AES-256-CBC
```

If left commented, only the default set is used (usually AES-256-GCM:AES-128-GCM). If your client uses AES-256-CBC and this line is commented, the connection will fail after TLS setup. For a uniform config, it’s best to let the client also use AES-256-GCM.


Enable Logging:

```text
log-append  /var/log/openvpn/openvpn.log
```

Save the configuration.

---

# Enable IP Forwarding

Open:

```bash
sudo nano /etc/sysctl.conf
```

Uncomment:

```text
net.ipv4.ip_forward=1
```

Apply the changes:

```bash
sudo sysctl -p
```

---
# Configure Routing for VPN Clients

Since VPN clients only need access to the internal LAN (`192.168.10.0/24`), Network Address Translation (NAT) is not required.

Instead, every internal machine must know that the VPN subnet (`10.8.0.0/24`) is reachable through the OpenVPN server.

> **Note:**  
> In this lab environment, there is no router or Layer 3 switch to distribute routes automatically. Therefore, a static route must be added manually to each internal machine that needs to communicate with VPN clients.
>
> In a production environment, this route is typically configured once on the organization's router or Layer 3 switch, allowing all internal devices to reach the VPN subnet without individual configuration.

## Windows

On every Windows machine, run the following command from an elevated Command Prompt:

```cmd
route -p add 10.8.0.0 mask 255.255.255.0 192.168.10.40
```

The `-p` option makes the route persistent after a reboot.

## Linux

### Temporary Route

```bash
sudo ip route add 10.8.0.0/24 via 192.168.10.40
```

### Persistent Route (Netplan)

Edit your Netplan configuration file:

```bash
sudo nano /etc/netplan/*.yaml
```

Add the following route under the interface connected to the internal LAN:

```yaml
routes:
  - to: 10.8.0.0/24
    via: 192.168.10.40
```

Apply the changes:

```bash
sudo netplan apply
```

## Route Details

- **VPN Subnet:** `10.8.0.0/24`
- **Gateway:** `192.168.10.40` (OpenVPN Server)

> **Why use routing instead of NAT?**
>
> This approach preserves the original VPN client IP addresses (`10.8.0.x`), allowing each connected user to be uniquely identified in server logs, firewall logs, and monitoring platforms such as Splunk. This is the recommended design for enterprise environments where auditing, user attribution, and security monitoring are required.

---

# Start OpenVPN

Enable the service:

```bash
sudo systemctl enable openvpn-server@server
```

Start the service:

```bash
sudo systemctl start openvpn-server@server
```

Verify:

```bash
sudo systemctl status openvpn-server@server
```

---

# Client Configuration

Instead of manually creating an `.ovpn` file, you can use a script that automatically generates the client profile directly from your Easy-RSA directory.

---

## Step 1: Create the Script

Navigate to your Easy-RSA directory:

```bash
cd ~/easy-rsa
```

Create a new file named `gen-client.sh`:

```bash
nano gen-client.sh
```

Paste the following script:

```bash
#!/bin/bash

# NOTE:
# - Replace YOUR_CLIENT_NAME.
# - Replace YOUR_PUBLIC_IP and YOUR_PORT.

set -e

CLIENT="YOUR_CLIENT_NAME"
OUTFILE="${CLIENT}.ovpn"
BASE=$(pwd)

# Verify required files exist
REQUIRED=(
    "$BASE/pki/ca.crt"
    "$BASE/pki/issued/${CLIENT}.crt"
    "$BASE/pki/private/${CLIENT}.key"
    "$BASE/ta.key"
)

for f in "${REQUIRED[@]}"; do
    if [ ! -f "$f" ]; then
        echo "[!] Missing required file: $f"
        exit 1
    fi
done

cat > "$OUTFILE" <<EOF
client
dev tun
proto tcp
remote YOUR_PUBLIC_IP YOUR_PORT
resolv-retry infinite
nobind
persist-key
persist-tun
remote-cert-tls server
auth SHA512
cipher AES-256-GCM
verb 3

<ca>
$(cat "$BASE/pki/ca.crt")
</ca>

<cert>
$(awk '/-----BEGIN CERTIFICATE-----/{flag=1} flag; /-----END CERTIFICATE-----/{flag=0}' "$BASE/pki/issued/${CLIENT}.crt")
</cert>

<key>
$(cat "$BASE/pki/private/${CLIENT}.key")
</key>

<tls-auth>
$(cat "$BASE/ta.key")
</tls-auth>

key-direction 1
EOF

```

Save the file:

* Press **Ctrl + O**, then **Enter**
* Press **Ctrl + X** to exit

---

## Step 2: Make the Script Executable

Grant execute permission to the script:

```bash
chmod +x gen-client.sh
```

---

## Step 3: Generate the Client Configuration

```bash
./gen-client.sh
```
---

## Step 4: Transfer the Configuration to the Client

Copy the generated `.ovpn` file to the client machine (e.g., Kali Linux).

Once transferred, import the profile into the OpenVPN client and connect to the VPN server.


---

# Linux Client Setup (Kali / Ubuntu)

## Install OpenVPN Client

```bash
sudo apt update
sudo apt install openvpn -y
openvpn --version
```

---

## Connect to VPN

Run:

```bash
sudo openvpn --config client.ovpn
```

If you want to run in background (Optional)

```bash
sudo openvpn --config client.ovpn --daemon
```

Success indicator:

* Initialization Sequence Completed
* tun0 interface appears


If you want to Stop:

```bash
sudo pkill openvpn
```

---

## Verify VPN Interface

```bash
ip addr
```

Expected:

* tun0 interface
* VPN IP: `10.8.0.2`

---

## Test Connectivity

```bash
ping -c4 10.8.0.1
ping -c4 192.168.10.20
ping -c4 192.168.10.30
```

---

# Verification Checklist

* Ubuntu fully updated
* OpenVPN installed
* Easy-RSA configured
* Certificates generated
* Keys copied to `/etc/openvpn/server/keys`
* TCP protocol enabled
* IP forwarding enabled
* NAT configured
* OpenVPN service running
* Client uses single `.ovpn`
* Linux client connects successfully
* Internal network reachable

---

# SOC Scenario

The OpenVPN server simulates an enterprise remote-access gateway.

In this lab model, an attacker obtains valid VPN credentials via phishing or endpoint compromise. After connecting, the attacker gains access to the internal network and performs reconnaissance, credential testing, and lateral movement.

Security monitoring tools (e.g., SIEM platforms) track:

* VPN authentication events
* Internal network scanning activity
* Lateral movement attempts
* Privilege escalation behavior
