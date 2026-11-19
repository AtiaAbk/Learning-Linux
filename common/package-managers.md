# 📦 Package Management Across Distributions

> [!TIP]
> Distro-specific deep dives:
> 👉 **[APT Field Guide (Part 2)](../terminal%20basics%20/book_study_linu_part2.md#-chapter-07--package-management-with-apt)**
> 👉 **[Ubuntu Package Management](../Ubuntu%20desktop/package-management.md)**

---

## 🔄 Cross-Distro Command Comparison

| Action | Ubuntu / Debian (`apt`) | Fedora / RHEL (`dnf`) | Kali Linux (`apt`) | Arch (`pacman`) |
|---|---|---|---|---|
| Refresh metadata | `sudo apt update` | `sudo dnf check-update` | `sudo apt update` | `sudo pacman -Sy` |
| Upgrade all packages | `sudo apt upgrade -y` | `sudo dnf upgrade -y` | `sudo apt full-upgrade -y` | `sudo pacman -Syu` |
| Install package | `sudo apt install <pkg>` | `sudo dnf install <pkg>` | `sudo apt install <pkg>` | `sudo pacman -S <pkg>` |
| Remove package | `sudo apt remove <pkg>` | `sudo dnf remove <pkg>` | `sudo apt remove <pkg>` | `sudo pacman -R <pkg>` |
| Search repositories | `apt search <pkg>` | `dnf search <pkg>` | `apt search <pkg>` | `pacman -Ss <pkg>` |

---

[⬅️ Back to Main README](../README.md)
