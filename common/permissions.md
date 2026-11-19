# 🔐 Linux Permissions & Ownership

> [!TIP]
> Comprehensive distro-specific guide:
> 👉 **[Ubuntu Permissions & Security Guide](../Ubuntu%20desktop/permissions.md)**
> 👉 **[Permissions Deep Dive in Terminal Basics](../terminal%20basics%20/book_study_linu_part1.md#5-understanding-file-permissions)**

---

## 📋 The Permission Matrix

| Value | Permission | Symbol | Binary |
|:---:|:---|:---:|:---:|
| **4** | Read | `r` | `100` |
| **2** | Write | `w` | `010` |
| **1** | Execute | `x` | `001` |
| **0** | None | `-` | `000` |

### Common Modes
- `chmod 755 script.sh` ➔ Owner: `rwx`, Group: `r-x`, Others: `r-x`
- `chmod 644 file.txt`  ➔ Owner: `rw-`, Group: `r--`, Others: `r--`
- `chmod 600 id_rsa`    ➔ Owner: `rw-`, Group: `---`, Others: `---`

```bash
# Changing ownership
sudo chown user:group filename
```

---

[⬅️ Back to Main README](../README.md)
