# VPN – Connect Securely with OpenVPN and WireGuard

Virtual Private Networks (VPNs) are essential for **anonymity**, **privacy**, and **remote access**. Two of the most popular and secure protocols are **OpenVPN** and **WireGuard**.

This page helps you generate commands to connect to or configure a VPN using either OpenVPN or WireGuard from the command line.

👉 [Generate OpenVPN / WireGuard Commands on SploitHQ](https://sploithq.com/vpn)

---

## 🛡 Why Use a VPN?

- **Mask your IP address**
- **Encrypt network traffic** against eavesdropping
- **Access private or internal networks**
- **Bypass network restrictions or filtering**
- **Stay anonymous during recon or testing**

---

## 🔧 OpenVPN Usage

OpenVPN uses `.ovpn` configuration files and supports both TCP and UDP.

### 📥 Import and Connect to a VPN

```bash
sudo openvpn --config client.ovpn
```

### 📂 Background Run with Logging

```bash
sudo openvpn --daemon --config client.ovpn --log /var/log/openvpn.log
```

### 🔑 Use Separate Auth File

```bash
sudo openvpn --config client.ovpn --auth-user-pass creds.txt
```

Where `creds.txt` contains:
```
username
password
```

---

## ⚙️ WireGuard Usage

WireGuard uses `.conf` files and runs in kernel space (faster and leaner).

### 🆑 Connect Using wg-quick

```bash
sudo wg-quick up wg0
```

> Make sure `wg0.conf` is in `/etc/wireguard/`

### 📴 Disconnect

```bash
sudo wg-quick down wg0
```

### 🔍 Show Interface and Peers

```bash
sudo wg show
```

---

## 📋 Configuration Examples

### 📝 `wg0.conf` example:

```ini
[Interface]
PrivateKey = <your_private_key>
Address = 10.0.0.2/24
DNS = 1.1.1.1

[Peer]
PublicKey = <peer_public_key>
Endpoint = vpn.example.com:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25
```

---

## 💡 Notes

- OpenVPN requires **root/sudo privileges** to modify routing tables.
- WireGuard requires the `wireguard-tools` package and kernel support.
- To auto-connect on boot: use systemd for both OpenVPN and WireGuard.

---

## 🧪 Test VPN Connectivity

```bash
curl ifconfig.me
```

Confirm that your public IP has changed after connection.

---

## 🌐 SploitHQ VPN Command Generator

Use the form to:
- Choose between OpenVPN and WireGuard
- Upload config or set fields
- Generate full command to copy and run

👉 [Launch the VPN Command Generator Tool](https://sploithq.com/vpn)

---

## 🔗 Related Tools

- [IP Lookup](https://sploithq.com/ip-lookup)
- [Traceroute](https://sploithq.com/traceroute)
- [Nmap VPN Scan Tips](https://sploithq.com/nmap)

---

## 📄 Legal Notice

Use VPNs responsibly. Never use them to bypass lawful controls or perform unauthorized access. SploitHQ supports ethical use only.
