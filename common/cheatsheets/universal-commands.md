# ⚡ Universal Linux Commands Cheat Sheet

> Quick-reference printable guide for every Linux distribution.

---

### 🧭 Navigation & Files
```bash
pwd                       # Current directory
ls -lah                   # Detailed list including hidden files
cd ~                      # Home directory
cd -                      # Previous directory
mkdir -p a/b/c            # Nested directories
touch file.txt            # Create or update timestamp
cp -r dir1 dir2           # Copy directory recursively
mv old.txt new.txt        # Move or rename
rm -rf temp_dir/          # Force delete directory (careful!)
```

### 🔍 Searching & Inspection
```bash
find . -name "*.log"      # Find files by pattern
find / -size +100M        # Find files larger than 100MB
grep -rn "keyword" .      # Search text recursively with line numbers
which python3             # Show executable path
whereis nginx             # Show binary, source, and man pages
head -n 20 file.txt       # First 20 lines
tail -f /var/log/syslog   # Follow file changes in real time
```

### 🔐 Permissions & Administration
```bash
chmod 755 script.sh       # rwxr-xr-x
chmod 644 file.txt        # rw-r--r--
sudo chown -R $USER:$USER /var/www  # Recursive ownership change
sudo systemctl status ssh # Check service status
sudo systemctl restart ssh# Restart service
```

---

[⬅️ Back to Main README](../../README.md)
