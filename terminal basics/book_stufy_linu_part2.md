<div align="center">

# 🐧 LINUX COMMAND-LINE FIELD GUIDE
### Chapters 07 · 08 · 09

**APT Package Management · File Reading & Editing · Pipes & Redirection**

[![Linux](https://img.shields.io/badge/Platform-Linux-FCC624?logo=linux&logoColor=black)](https://www.kernel.org/)
[![Beginner Friendly](https://img.shields.io/badge/Level-Beginner%20Friendly-2ea44f)](#)
[![Topics](https://img.shields.io/badge/Chapters-07%20%7C%2008%20%7C%2009-6f42c1)](#)

*Learn the command. Understand the syntax. See the output. Know when to use it.*

</div>

---

## 🧭 Navigation

| Chapter | Topic | What you will learn |
|:--:|---|---|
| **07** | 📦 [Package Management](#-chapter-07--package-management-with-apt) | Search, install, update, upgrade and remove software |
| **08** | 📄 [Reading & Editing Files](#-chapter-08--reading-and-editing-files) | Display, browse, monitor and edit text files |
| **09** | 🔀 [Pipes & Redirection](#-chapter-09--pipes-and-redirection) | Control input/output and connect commands |
| **Bonus** | 🧪 [Command Cookbook](#-command-cookbook--all-commands-at-a-glance) | Quick syntax and demo examples for every command |
| **Practice** | 🎯 [Hands-on Challenges](#-hands-on-challenges) | Test what you have learned |

---

## 👋 About This Guide

This is a practical study guide for people learning Linux from the terminal. It is written to explain **what a command does, how its syntax works, what the output may look like, and how it differs from similar commands**.

### By the end, you should be able to:

- Manage software on Ubuntu/Debian using APT.
- Read short and large text files comfortably.
- Edit files using Nano and understand basic Vim.
- Redirect command output into files.
- Pass the output of one command into another using a pipe.
- Build useful command pipelines for everyday tasks.

> **Compatibility note:** APT examples are for Ubuntu/Debian-based Linux. Most file and shell examples also work on macOS, although some options and tools can differ. macOS users generally use Homebrew instead of APT.

## 🧰 Before You Start

Open a terminal and check your system:

```bash
cat /etc/os-release
```

Create a safe practice folder:

```bash
mkdir -p ~/linux-practice
cd ~/linux-practice
```

All practice files in this guide can be created inside this folder.

### Read these symbols first

| Symbol | Meaning |
|---|---|
| `$` | Normal user prompt (do not type it) |
| `#` | Root prompt in examples (do not type it) |
| `~` | Your home directory |
| `.` | Current directory |
| `..` | Parent directory |
| `&&` | Run the next command only if the previous one succeeds |
| `\|` | Pipe: send one command's output to another command |

---

# 📦 CHAPTER 07 — PACKAGE MANAGEMENT WITH APT

## 1. What is a package manager?

A **package** is a program or software component that can be installed on a computer. A **package manager** helps the operating system install, update, inspect and remove software.

APT (Advanced Package Tool) is commonly used on Ubuntu and Debian.

Think of APT as a software store controlled from the terminal:

- `search` — find software.
- `show` — inspect software details.
- `install` — install software.
- `update` — refresh the available-package catalogue.
- `upgrade` — upgrade installed software.
- `remove` / `purge` — uninstall software.

> 🔐 **Safety:** Commands that change system software commonly need `sudo`. Read the proposed changes before confirming them.

## 2. Refresh package information — `apt update`

### Syntax

```bash
sudo apt update
```

### What it does

Downloads the latest package information from the software repositories configured on your system.

It **does not install updates to your applications**. It refreshes the package catalogue so APT knows which versions are available.

### Demo

```bash
sudo apt update
```

Example output (your package sources and version numbers will differ):

```text
Hit:1 http://archive.ubuntu.com/ubuntu noble InRelease
Get:2 http://archive.ubuntu.com/ubuntu noble-updates InRelease
Reading package lists... Done
Building dependency tree... Done
```

## 3. Upgrade installed software — `apt upgrade`

### Syntax

```bash
sudo apt upgrade
```

### What it does

Installs available upgrades for packages already installed on the system.

### `update` vs `upgrade`

| Command | Actual job | Easy way to remember |
|---|---|---|
| `sudo apt update` | Refreshes package information | Refresh the shop catalogue |
| `sudo apt upgrade` | Upgrades installed packages | Update the software you own |

Run them together:

```bash
sudo apt update && sudo apt upgrade
```

`&&` means the second command runs only if the first command succeeds.

## 4. Install software — `apt install`

### Syntax

```bash
sudo apt install package-name
```

### Install one package

```bash
sudo apt install tree
```

### Install multiple packages

```bash
sudo apt install tree curl wget htop
```

| Package | What it is used for |
|---|---|
| `tree` | Displays folders and files in a tree structure |
| `curl` | Transfers data to or from a URL |
| `wget` | Downloads files from the web |
| `htop` | Interactive process and resource monitor |

Try the installed command:

```bash
tree ~
```

Example:

```text
/home/learner
├── Documents
├── Downloads
└── linux-practice
    └── notes.txt
```

## 5. Search for software — `apt search`

### Syntax

```bash
apt search keyword
```

### Demo

```bash
apt search screenshot
```

Searches package names and descriptions for the word `screenshot`.

Another example:

```bash
apt search cowsay
```

**Use it when:** You know what kind of application you need but do not know the exact package name.

## 6. Inspect a package — `apt show`

### Syntax

```bash
apt show package-name
```

### Demo

```bash
apt show htop
```

This displays package details such as its description, version, dependencies and download size.

**Difference:** `apt search` helps you find a package; `apt show` gives details about a package you have identified.

## 7. List installed packages — `apt list`

### Syntax

```bash
apt list --installed
```

Displays packages currently installed through APT.

Count the displayed lines:

```bash
apt list --installed | wc -l
```

The count can include a heading, so treat it as an approximate count.

## 8. Remove software — `apt remove`, `apt purge`, `apt autoremove`

These commands are related, but they do different jobs.

| Command | What it removes |
|---|---|
| `sudo apt remove tree` | Removes the package; package configuration may remain |
| `sudo apt purge tree` | Removes the package and its package-managed system configuration |
| `sudo apt autoremove` | Removes automatically installed dependencies that are no longer needed |

### Examples

```bash
sudo apt remove tree
```

```bash
sudo apt purge tree
```

```bash
sudo apt autoremove
```

> ⚠️ Before confirming a removal, inspect APT's list of packages that it proposes to remove. Do not assume every proposed removal is harmless.

## 9. Other software sources

### Local `.deb` package

A `.deb` file is a Debian software package.

```bash
sudo apt install ./application.deb
```

`./` tells APT to use a local file in the current directory.

Only install packages from official or trusted sources, and check that the architecture is compatible.

### PPA — Personal Package Archive

A PPA is an additional software repository.

General syntax:

```bash
sudo add-apt-repository ppa:owner/archive
sudo apt update
```

`owner/archive` is a placeholder, not a repository to copy blindly. Only add repositories you trust.

### Snap

Snap is another application packaging and distribution system.

Example on a compatible Ubuntu system:

```bash
sudo snap install code --classic
```

---

## 📌 Chapter 07 — Quick Command Card

| Command | Purpose | Needs `sudo`? |
|---|---|:--:|
| `sudo apt update` | Refresh package catalogue | Yes |
| `sudo apt upgrade` | Upgrade installed packages | Yes |
| `sudo apt install name` | Install a package | Yes |
| `apt search word` | Search packages | Usually no |
| `apt show name` | Inspect package information | Usually no |
| `apt list --installed` | List installed packages | Usually no |
| `sudo apt remove name` | Remove a package | Yes |
| `sudo apt purge name` | Remove package and package-managed config | Yes |
| `sudo apt autoremove` | Remove unused auto-installed dependencies | Yes |
| `sudo snap install name` | Install a Snap package | Usually yes |

---

# 📄 CHAPTER 08 — READING AND EDITING FILES

## 1. Prepare a practice file

Run these commands inside `~/linux-practice`:

```bash
cd ~/linux-practice

echo "Day 1: Linu came home" > linu-diary.txt
echo "Day 2: Linu played" >> linu-diary.txt
echo "Day 3: Linu went to the vet" >> linu-diary.txt
echo "Day 4: Linu ate fish" >> linu-diary.txt
echo "Day 5: Linu slept all day" >> linu-diary.txt
```

We will use this file to practise reading and editing commands.

## 2. `cat` — display file content

### Syntax

```bash
cat filename
```

### Demo

```bash
cat linu-diary.txt
```

Output:

```text
Day 1: Linu came home
Day 2: Linu played
Day 3: Linu went to the vet
Day 4: Linu ate fish
Day 5: Linu slept all day
```

### Other useful forms

Display two files one after another:

```bash
cat file1.txt file2.txt
```

Create a file from typed terminal input:

```bash
cat > newfile.txt
```

Type your text, then press `Ctrl + D` to finish input and save.

**Best for:** Quickly displaying short files or joining file contents.

## 3. `less` — read a file page by page

### Syntax

```bash
less filename
```

### Demo

```bash
less linu-diary.txt
```

`less` opens an interactive viewer. You can move through the file without printing the entire content at once.

### Navigation keys

| Key | Action |
|---|---|
| `Space` / `PageDown` | Move down one page |
| `PageUp` | Move up one page |
| `↑` / `↓` | Move one line |
| `/word` | Search forward for `word` |
| `n` | Next search match |
| `g` | Beginning of file |
| `G` | End of file |
| `q` | Quit |

### `cat` vs `less`

| `cat` | `less` |
|---|---|
| Prints content directly | Opens a navigable viewer |
| Convenient for short files | Better for long files |
| No built-in page navigation | Supports searching and page navigation |

**Rule of thumb:** `cat` for a quick look; `less` for exploring a long file.

## 4. `head` — show the beginning of a file

### Syntax

```bash
head [option] filename
```

By default, `head` displays the first 10 lines.

```bash
head linu-diary.txt
```

Display only the first two lines:

```bash
head -n 2 linu-diary.txt
```

Example output:

```text
Day 1: Linu came home
Day 2: Linu played
```

**Use it when:** You want to inspect the beginning of a file, such as the first lines of a CSV or log.

## 5. `tail` — show the end of a file

### Syntax

```bash
tail [option] filename
```

By default, `tail` displays the last 10 lines.

```bash
tail linu-diary.txt
```

Display only the last two lines:

```bash
tail -n 2 linu-diary.txt
```

Example output:

```text
Day 4: Linu ate fish
Day 5: Linu slept all day
```

### `head` vs `tail`

| Command | Default output | Typical use |
|---|---|---|
| `head file.txt` | First 10 lines | Check the beginning |
| `tail file.txt` | Last 10 lines | Check the newest/end entries |

## 6. `tail -f` — follow a file live

### Syntax

```bash
tail -f filename
```

`-f` means **follow**. The command keeps running and prints new lines when they are appended to the file.

### Two-terminal demo

**Terminal 1:**

```bash
tail -f linu-diary.txt
```

**Terminal 2:**

```bash
echo "Day 6: Linu learned a new trick" >> linu-diary.txt
```

The new line appears in Terminal 1.

Stop monitoring with:

```text
Ctrl + C
```

**Real-world use:** Watching a server log while new requests arrive.

```bash
tail -f /var/log/nginx/access.log
```

You may need permission to read system log files.

## 7. `nano` — beginner-friendly text editor

### Syntax

```bash
nano filename
```

### Demo

```bash
nano my-notes.txt
```

Type your text inside the editor.

| Shortcut | Action |
|---|---|
| `Ctrl + O` | Save (Write Out) |
| `Enter` | Confirm filename |
| `Ctrl + X` | Exit |
| `Ctrl + K` | Cut current line |
| `Ctrl + U` | Paste cut text |
| `Ctrl + W` | Search |

In Nano's shortcut bar, `^` means `Ctrl`. So `^X` means `Ctrl + X`.

### Save and exit

1. Press `Ctrl + O`.
2. Press `Enter` to confirm.
3. Press `Ctrl + X` to exit.

## 8. `vim` — a modal text editor

### Syntax

```bash
vim filename
```

Vim uses modes. The most important beginner modes are:

| Mode | Purpose |
|---|---|
| Normal mode | Navigate and run editing commands |
| Insert mode | Type text |

### Beginner editing demo

```bash
vim test.txt
```

1. Press `i` to enter Insert mode.
2. Type your text.
3. Press `Esc` to return to Normal mode.
4. Type `:wq` and press `Enter` to save and quit.

### Essential Vim commands

| Command | Action |
|---|---|
| `i` | Enter Insert mode |
| `Esc` | Return to Normal mode |
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Quit without saving changes |

**If you get stuck:** Press `Esc`, type `:q!`, and press `Enter`.

### Nano vs Vim

| Nano | Vim |
|---|---|
| Easier for beginners | More powerful, modal editor |
| Shortcuts shown on screen | Commands depend on current mode |
| Good for quick edits | Useful for advanced editing workflows |

---

## 📌 Chapter 08 — Quick Command Card

| Command | Purpose |
|---|---|
| `cat file.txt` | Print the whole file |
| `cat a.txt b.txt` | Print multiple files in sequence |
| `cat > file.txt` | Create/write a file from terminal input |
| `less file.txt` | Browse a file page by page |
| `head file.txt` | Show first 10 lines |
| `head -n 5 file.txt` | Show first 5 lines |
| `tail file.txt` | Show last 10 lines |
| `tail -n 5 file.txt` | Show last 5 lines |
| `tail -f file.txt` | Follow newly appended lines |
| `nano file.txt` | Open file in Nano |
| `vim file.txt` | Open file in Vim |

---

# 🔀 CHAPTER 09 — PIPES AND REDIRECTION

## 1. Understand the three standard streams

A command receives data, processes it and produces output. Linux uses three standard streams:

| Stream | Name | Number | Meaning |
|---|---|:--:|---|
| `stdin` | Standard input | `0` | Data a command reads |
| `stdout` | Standard output | `1` | Normal output |
| `stderr` | Standard error | `2` | Error messages |

By default, a command usually reads from the keyboard and prints output to the terminal. Redirection lets you change those destinations.

## 2. `>` — redirect output (overwrite)

### Syntax

```bash
command > filename
```

Sends standard output into a file.

### Demo

```bash
echo "First note" > output.txt
cat output.txt
```

Output:

```text
First note
```

Now run:

```bash
echo "Replacement note" > output.txt
cat output.txt
```

Output:

```text
Replacement note
```

The old content was overwritten.

> ⚠️ **Be careful:** `>` replaces existing file content. Check the filename before running it.

## 3. `>>` — append output

### Syntax

```bash
command >> filename
```

Adds standard output to the end of a file without replacing the existing content.

### Demo

```bash
echo "Line 1" > diary.txt
echo "Line 2" >> diary.txt
echo "Line 3" >> diary.txt
cat diary.txt
```

Output:

```text
Line 1
Line 2
Line 3
```

### `>` vs `>>`

| Operator | Meaning | Existing content |
|---|---|---|
| `>` | Write/overwrite | Replaced |
| `>>` | Append | Preserved |

Memory trick: **one arrow replaces; two arrows add.**

## 4. `|` — pipe output into another command

### Syntax

```bash
command1 | command2
```

A pipe sends the **standard output** of the command on the left to the **standard input** of the command on the right.

```text
┌────────────┐       pipe        ┌────────────┐
│  Command 1 │ ─────────────────▶│  Command 2 │
│  produces  │     output →      │  receives  │
│  output    │                    │  input     │
└────────────┘                    └────────────┘
```

### Demo 1 — browse a long list

```bash
ls /usr/bin | less
```

`ls` lists entries. `less` lets you browse the list. Press `q` to quit.

### Demo 2 — filter matching lines

```bash
ls /usr/bin | grep zip
```

`grep zip` prints lines containing `zip`.

### Demo 3 — count matching lines

```bash
ls /usr/bin | grep zip | wc -l
```

The output of each command becomes the input of the next command.

## 5. `grep` — search for matching text

### Syntax

```bash
grep [option] "pattern" filename
```

Create a sample file:

```bash
cat > names.txt << 'EOF'
Rahim
Karim
Atia
Raisa
Karim
EOF
```

Search for `Karim`:

```bash
grep "Karim" names.txt
```

Output:

```text
Karim
Karim
```

Useful options:

| Option | Meaning | Example |
|---|---|---|
| `-i` | Ignore uppercase/lowercase differences | `grep -i "atia" names.txt` |
| `-n` | Show line numbers | `grep -n "Karim" names.txt` |
| `-v` | Show lines that do not match | `grep -v "Karim" names.txt` |
| `-c` | Count matching lines | `grep -c "Karim" names.txt` |

**Difference:** `grep` searches for matching text; `wc -l` counts lines. Combine them when you need to count matches:

```bash
grep "Karim" names.txt | wc -l
```

## 6. `wc` — count lines, words and bytes

`wc` means **word count**.

### Syntax

```bash
wc [option] [filename]
```

| Option | Counts |
|---|---|
| `-l` | Lines |
| `-w` | Words |
| `-c` | Bytes |
| `-m` | Characters |

### Demo

```bash
wc names.txt
wc -l names.txt
wc -w names.txt
wc -c names.txt
```

### Why does `<` change the output?

Compare these two commands:

```bash
wc -l names.txt
```

Example output:

```text
5 names.txt
```

Now:

```bash
wc -l < names.txt
```

Example output:

```text
5
```

Both count the lines. The difference is how the input reaches `wc`:

- `wc -l names.txt` — the filename is passed as a command-line argument.
- `wc -l < names.txt` — the shell redirects the file to standard input.

Because the second command receives standard input rather than a named-file argument, `wc` prints only the count.

## 7. `<` — redirect input from a file

### Syntax

```bash
command < filename
```

The shell opens the file and supplies its content as the command's standard input.

### Demo

```bash
sort < names.txt
```

This asks `sort` to read from standard input, which is connected to `names.txt`.

Compare it with:

```bash
sort names.txt
```

Both sort the file's lines. The first uses input redirection; the second passes the filename as an argument.

## 8. `sort` — arrange lines

### Syntax

```bash
sort [option] filename
```

Create a file:

```bash
cat > fruits.txt << 'EOF'
orange
apple
banana
apple
EOF
```

Alphabetical sort:

```bash
sort fruits.txt
```

Output:

```text
apple
apple
banana
orange
```

Useful options:

| Option | Meaning | Example |
|---|---|---|
| `-r` | Reverse order | `sort -r fruits.txt` |
| `-n` | Numeric sort | `sort -n numbers.txt` |
| `-rn` | Numeric, reverse order | `sort -rn numbers.txt` |

For example, create numeric data:

```bash
printf "20\n3\n100\n11\n" > numbers.txt
sort -n numbers.txt
```

Output:

```text
3
11
20
100
```

## 9. `uniq` — report or remove adjacent duplicates

### Syntax

```bash
uniq [option] filename
```

`uniq` normally checks **adjacent** repeated lines. It does not automatically group identical lines that are separated.

Example:

```bash
uniq fruits.txt
```

Because the duplicate `apple` entries are not adjacent in the original file, both may remain.

Sort first, then use `uniq`:

```bash
sort fruits.txt | uniq
```

Count repeated adjacent lines:

```bash
sort fruits.txt | uniq -c
```

Example output:

```text
      2 apple
      1 banana
      1 orange
```

Useful option:

| Option | Meaning |
|---|---|
| `-c` | Show the number of occurrences for each adjacent group |

## 10. `cut` — extract fields or columns

### Syntax

```bash
cut -d 'delimiter' -f field_number filename
```

`cut` extracts selected fields from each line.

Create a file:

```bash
cat > people.txt << 'EOF'
Rahim:Developer:Dhaka
Karim:Designer:Rajshahi
Nila:Student:Khulna
EOF
```

Extract the first field:

```bash
cut -d ':' -f 1 people.txt
```

Output:

```text
Rahim
Karim
Nila
```

Extract the second field:

```bash
cut -d ':' -f 2 people.txt
```

Output:

```text
Developer
Designer
Student
```

| Part | Meaning |
|---|---|
| `-d ':'` | The colon is the delimiter |
| `-f 1` | Select field 1 |
| `-f 2` | Select field 2 |

## 11. `&&` — run the next command only after success

### Syntax

```bash
command1 && command2
```

Demo:

```bash
mkdir demo-folder && cd demo-folder
```

If `mkdir demo-folder` succeeds, the shell runs `cd demo-folder`.

**Pipe vs `&&`:**

| Operator | What it connects | When does the next command run? |
|---|---|---|
| `\|` | Output of one command to input of another | As part of the pipeline |
| `&&` | Two commands in sequence | Only if the first succeeds |

---

## 🧪 Mini Project — Analyse a Visitor Log

### Goal

Find which IP address appears most often in a simple website access log.

### Step 1 — Create sample data

```bash
cat > otithi-khata.txt << 'EOF'
10.0.0.5 GET /home
10.0.0.9 GET /about
10.0.0.5 GET /products
10.0.0.7 GET /home
10.0.0.5 GET /contact
10.0.0.9 GET /home
10.0.0.5 GET /products
10.0.0.7 GET /about
10.0.0.5 GET /home
10.0.0.9 GET /products
EOF
```

Inspect the file:

```bash
cat otithi-khata.txt
```

### Step 2 — Extract the IP address

```bash
cut -d ' ' -f 1 otithi-khata.txt
```

The first field is the IP address.

### Step 3 — Sort the addresses

```bash
cut -d ' ' -f 1 otithi-khata.txt | sort
```

Sorting groups identical IP addresses together.

### Step 4 — Count each address

```bash
cut -d ' ' -f 1 otithi-khata.txt | sort | uniq -c
```

Expected output:

```text
      5 10.0.0.5
      2 10.0.0.7
      3 10.0.0.9
```

### Step 5 — Put the highest count first

```bash
cut -d ' ' -f 1 otithi-khata.txt | sort | uniq -c | sort -rn
```

Expected output:

```text
      5 10.0.0.5
      3 10.0.0.9
      2 10.0.0.7
```

### Step 6 — Show only the top result

```bash
cut -d ' ' -f 1 otithi-khata.txt | sort | uniq -c | sort -rn | head -n 1
```

Expected output:

```text
      5 10.0.0.5
```

### Understand the pipeline

```text
otithi-khata.txt
       │
       ▼
      cut       → Extract IP addresses
       │
       ▼
      sort      → Group identical addresses
       │
       ▼
     uniq -c    → Count each address
       │
       ▼
    sort -rn    → Highest count first
       │
       ▼
   head -n 1    → Display the top result
```

> This is a learning example, not a complete security analysis. A high request count alone does not prove malicious activity.

---

# 🗂️ COMMAND COOKBOOK — ALL COMMANDS AT A GLANCE

Use this section as a quick revision sheet. Each row shows the command's main job and a practical example.

## 📦 Package management

| Command | Main job | Demo |
|---|---|---|
| `sudo` | Run a command with elevated privileges | `sudo apt update` |
| `apt update` | Refresh package information | `sudo apt update` |
| `apt upgrade` | Upgrade installed packages | `sudo apt upgrade` |
| `apt install` | Install package(s) | `sudo apt install tree` |
| `apt search` | Search package catalogue | `apt search browser` |
| `apt show` | Show package details | `apt show htop` |
| `apt list` | List packages | `apt list --installed` |
| `apt remove` | Remove a package | `sudo apt remove tree` |
| `apt purge` | Remove package and package-managed config | `sudo apt purge tree` |
| `apt autoremove` | Remove unused auto-installed dependencies | `sudo apt autoremove` |
| `add-apt-repository` | Add a software repository | `sudo add-apt-repository ppa:owner/archive` |
| `snap install` | Install a Snap package | `sudo snap install code --classic` |

## 📄 File reading and editing

| Command | Main job | Demo |
|---|---|---|
| `cat` | Print file content | `cat notes.txt` |
| `less` | Browse a file interactively | `less notes.txt` |
| `head` | Show the first lines | `head -n 5 notes.txt` |
| `tail` | Show the last lines | `tail -n 5 notes.txt` |
| `tail -f` | Follow new lines live | `tail -f app.log` |
| `nano` | Edit in Nano | `nano notes.txt` |
| `vim` | Edit in Vim | `vim notes.txt` |

## 🔀 Search, count and process text

| Command | Main job | Demo |
|---|---|---|
| `grep` | Find matching text | `grep "error" app.log` |
| `wc` | Count lines, words or bytes | `wc -l notes.txt` |
| `sort` | Sort lines | `sort names.txt` |
| `uniq` | Handle adjacent duplicate lines | `sort names.txt \| uniq -c` |
| `cut` | Extract fields | `cut -d ':' -f 1 people.txt` |
| `ls` | List directory entries | `ls -l` |
| `echo` | Print text | `echo "Hello Linux"` |
| `printf` | Print formatted text | `printf "one\ntwo\n"` |
| `mkdir` | Create a directory | `mkdir practice` |
| `cd` | Change directory | `cd ~/linux-practice` |
| `history` | Show shell command history | `history` |
| `tree` | Display directory structure | `tree ~/linux-practice` |

## ➡️ Operators and special keys

| Symbol / key | Main job | Demo |
|---|---|---|
| `>` | Redirect output; overwrite file | `echo "Hi" > hi.txt` |
| `>>` | Append output to file | `echo "Again" >> hi.txt` |
| `<` | Read file as standard input | `wc -l < hi.txt` |
| `\|` | Pipe output into another command | `cat hi.txt \| grep Hi` |
| `&&` | Run next command only after success | `mkdir test && cd test` |
| `Ctrl + C` | Stop foreground process | Stop `tail -f` |
| `Ctrl + D` | Send end-of-input | Finish `cat > file.txt` |
| `Ctrl + O` | Save in Nano | Nano save |
| `Ctrl + X` | Exit Nano | Nano exit |
| `Esc` | Return to Vim Normal mode | Vim editing |
| `:wq` | Save and quit Vim | Vim command line |
| `:q!` | Quit Vim without saving | Vim command line |

> **Note:** The cookbook includes a few supporting commands used in the demonstrations, not only the main chapter headings. Some commands (such as `tree`, `htop`, `snap`, and `add-apt-repository`) may need to be installed or may not be available on every distribution.

---

# 🎯 HANDS-ON CHALLENGES

Try each task before looking back at the examples.

## Level 1 — Beginner

- [ ] Create a directory named `linux-lab`.
- [ ] Create a file named `about-me.txt`.
- [ ] Add three lines to the file.
- [ ] Display the file using `cat`.
- [ ] Show only the first two lines using `head`.
- [ ] Show only the last line using `tail`.

## Level 2 — File skills

- [ ] Open a file using `less` and search for a word.
- [ ] Edit a file using Nano and save it.
- [ ] Open a file in Vim, insert text, save and quit.
- [ ] Monitor a file using `tail -f` while adding a line from another terminal.

## Level 3 — Pipes and redirection

- [ ] Save the output of `ls -l` into `directory.txt`.
- [ ] Append the current date to that file.
- [ ] Search the file for a word using `grep`.
- [ ] Count the lines using `wc -l`.
- [ ] Compare `wc -l directory.txt` with `wc -l < directory.txt`.
- [ ] Sort a list of names and count duplicates.

## Level 4 — Package management

On an Ubuntu/Debian test system:

- [ ] Search for `htop`.
- [ ] Inspect its package information.
- [ ] Install it.
- [ ] Run it and exit with `q`.
- [ ] Practise removing it only if you no longer need it.

---

# 🧠 FINAL REVISION — WHAT MUST YOU REMEMBER?

| If you want to… | Use |
|---|---|
| Refresh available package information | `sudo apt update` |
| Upgrade installed software | `sudo apt upgrade` |
| Find a package | `apt search` |
| Read a short file | `cat` |
| Browse a long file | `less` |
| See the first lines | `head` |
| See the last lines | `tail` |
| Watch new log entries | `tail -f` |
| Edit a file simply | `nano` |
| Send output to a new/overwritten file | `>` |
| Add output to an existing file | `>>` |
| Feed a file to a command | `<` |
| Connect commands | `\|` |
| Search text | `grep` |
| Count lines | `wc -l` |
| Sort lines | `sort` |
| Count adjacent duplicates | `uniq -c` (often after `sort`) |
| Extract a field | `cut` |

## 📚 Official references

- [Ubuntu Documentation](https://documentation.ubuntu.com/)
- [Debian APT User's Guide](https://www.debian.org/doc/manuals/apt-guide/)
- [GNU Coreutils Manual](https://www.gnu.org/software/coreutils/manual/)
- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
- [GNU Grep Manual](https://www.gnu.org/software/grep/manual/)
- [Nano Editor](https://www.nano-editor.org/)
- [Vim Documentation](https://www.vim.org/docs.php)
- [Homebrew — macOS package manager](https://brew.sh/)

## 🍎 Note for macOS learners

The file, text-processing and shell-redirection examples are useful on macOS too. However:

- APT is for Debian/Ubuntu-based Linux, not macOS.
- macOS users commonly use [Homebrew](https://brew.sh/) to install command-line tools.
- macOS includes BSD versions of some utilities, while many Linux distributions use GNU versions. A few flags and behaviours may differ.

---

<div align="center">

### ⭐ Keep practising. Understand the flow, not just the command.

**Linux is not about memorising hundreds of commands. It is about combining a few useful tools to solve real problems.**

*End of Chapters 07–09*

</div>
