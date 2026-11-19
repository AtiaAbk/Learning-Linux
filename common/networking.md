# 🌐 Linux Networking Fundamentals

> [!TIP]
> Distro-specific guide:
> 👉 **[Ubuntu Networking & Troubleshooting](../Ubuntu%20desktop/networking.md)**

---

## 🛠️ Essential Networking Commands

| Task | Modern Command | Legacy Equivalent |
|---|---|---|
| Show IP addresses | `ip addr show` / `ip a` | `ifconfig` |
| Show routing table | `ip route` | `route -n` |
| Active listening ports | `ss -tulpn` | `netstat -tulpn` |
| Test connectivity | `ping -c 4 <ip>` | `ping <ip>` |
| Query DNS records | `dig <domain>` | `nslookup <domain>` |
| Transfer files remotely | `rsync -avz src/ user@host:dest/` | `scp` |

---

[⬅️ Back to Main README](../README.md)
