# 🐧 Linux Learning Notes

### A Beginner-to-Intermediate Journey into Linux Fundamentals and Command-Line Operations

![Linux](https://img.shields.io/badge/OS-Linux-FCC624?logo=linux&logoColor=black)
![Shell](https://img.shields.io/badge/Shell-Bash-4EAA25?logo=gnubash&logoColor=white)
![Status](https://img.shields.io/badge/Status-In%20Progress-blue)
![Notes](https://img.shields.io/badge/Notes-Chapters%201--6-orange)

A structured collection of Linux learning notes, command explanations, practical examples, and exercises. This repository documents my learning journey from understanding operating system fundamentals to working with Linux directories, files, permissions, and file-searching commands.

The primary goal is to understand **what each command does, why it is used, how it works, and when to use it in real-world situations.**

---

## 📚 Table of Contents

- [About This Repository](#-about-this-repository)
- [Learning Environment](#-learning-environment)
- [Chapter 1: Introduction to Linux](#-chapter-1-introduction-to-linux)
  - [What Is Linux?](#1-what-is-linux)
  - [Understanding the Kernel](#2-understanding-the-kernel)
  - [Linux Kernel vs Linux Distribution](#3-linux-kernel-vs-linux-distribution)
  - [Linux vs Windows vs macOS](#4-linux-vs-windows-vs-macos)
  - [What Happens When You Open an Application?](#5-what-happens-when-you-open-an-application)
  - [Understanding Deadlock](#6-understanding-deadlock)
- [Chapter 2: Bringing Linux Home](#-chapter-2-bringing-linux-home)
  - [Ways to Use Linux](#1-ways-to-use-linux)
  - [Virtual Machines](#2-virtual-machines)
  - [Using Linux Concepts on macOS](#3-using-linux-concepts-on-macos)
  - [First Commands](#4-first-commands)
- [Chapter 3: Understanding the Language of Linux](#-chapter-3-understanding-the-language-of-linux)
  - [Terminal vs Shell vs Bash](#1-terminal-vs-shell-vs-bash)
  - [Understanding the Linux Prompt](#2-understanding-the-linux-prompt)
  - [Command Structure](#3-command-structure)
  - [Linux Is Case-Sensitive](#4-linux-is-case-sensitive)
  - [Getting Help](#5-getting-help)
  - [Basic Commands](#6-basic-commands)
- [Chapter 4: Exploring the Linux Filesystem](#-chapter-4-exploring-the-linux-filesystem)
  - [Filesystem Structure](#1-understanding-the-linux-filesystem)
  - [Important Directories](#2-important-linux-directories)
  - [Absolute vs Relative Paths](#3-absolute-vs-relative-paths)
  - [Navigation Commands](#4-navigation-commands)
  - [Understanding File Permissions](#5-understanding-file-permissions)
  - [chmod and chown](#6-changing-permissions-and-ownership)
- [Chapter 5: Managing Files and Directories](#-chapter-5-managing-files-and-directories)
  - [mkdir](#1-mkdir--create-directories)
  - [touch](#2-touch--create-files)
  - [cp](#3-cp--copy-files-and-directories)
  - [mv](#4-mv--move-and-rename)
  - [rm](#5-rm--remove-files-and-directories)
  - [Hidden Files](#6-hidden-files)
  - [Wildcards](#7-wildcards)
  - [The -p Option](#8-understanding-the--p-option-in-mkdir)
- [Chapter 6: Finding Lost Files](#-chapter-6-finding-lost-files)
  - [find](#1-find--search-for-files-and-directories)
  - [grep](#2-grep--search-inside-files)
  - [which](#3-which--find-a-command-location)
  - [whereis](#4-whereis--find-program-related-files)
  - [locate](#5-locate--search-using-an-index)
  - [Command Comparison](#6-which-command-should-you-use)
- [Practical Exercises](#-practical-exercises)
- [Important Command Cheat Sheet](#-important-command-cheat-sheet)
- [Important Things to Remember](#-important-things-to-remember)
- [Learning Progress](#-learning-progress)
- [Upcoming Chapters](#-upcoming-chapters)



# 💻 Learning Environment

My primary computer is a **MacBook Air M4 with 16 GB RAM**.

I use macOS Terminal to practise common Unix commands and plan to use an Ubuntu virtual machine for Linux-specific administration and server-related tasks.

| Environment | Purpose |
|---|---|
| macOS Terminal | Practising basic terminal commands |
| Ubuntu Linux | Learning actual Linux administration |
| Virtual Machine | Running Linux separately from macOS |
| GitHub | Storing and organizing learning notes |

**Important distinction:** macOS is Unix-like, but it is not a Linux distribution. Many basic commands are similar, but some options, tools, and administrative commands differ.

---

# 🐧 Chapter 1: Introduction to Linux

## 1. What Is Linux?

Linux is an open-source operating system kernel.

It is widely used in:

- Servers
- Supercomputers
- Cloud infrastructure
- Embedded systems
- Networking devices
- Android-based devices

Linux is known for its flexibility, security features, stability, and open-source development model.

## 2. Understanding the Kernel

The **kernel** is the core component of an operating system.

It acts as a bridge between software and computer hardware.

Applications cannot normally control hardware directly. They request services from the operating system, and the kernel manages the required resources.

### Main Responsibilities of the Kernel

| Responsibility | Explanation |
|---|---|
| Process Management | Creates, schedules, and manages running processes |
| Memory Management | Allocates and manages RAM and virtual memory |
| Device Management | Communicates with hardware through device drivers |
| File System Management | Handles file operations and filesystem access |
| Security and Permissions | Enforces access controls |
| CPU Scheduling | Decides which process gets CPU time |

### Simple Example

When you open a browser:

1. The operating system receives the request to start the application.
2. The executable and required libraries are loaded.
3. The system creates a process and provides the necessary resources.
4. Virtual memory is assigned.
5. The scheduler provides CPU time.
6. The browser begins executing.

The kernel manages the underlying resources throughout this process.

## 3. Linux Kernel vs Linux Distribution

These two terms are related but not identical.

### Linux Kernel

The kernel is the central component responsible for managing hardware and system resources.

### Linux Distribution

A Linux distribution combines the Linux kernel with other software, system utilities, package-management tools, and often a desktop environment.

Examples:

- Ubuntu
- Debian
- Fedora
- Arch Linux

| Linux Kernel | Linux Distribution |
|---|---|
| Core of the operating system | Complete operating-system package |
| Manages hardware and resources | Provides a usable operating environment |
| Does not represent a complete desktop experience by itself | May include desktop environments and applications |
| Used as the foundation of distributions | Built around the Linux kernel |

**Remember:** Ubuntu is a Linux distribution, not simply another name for the Linux kernel.

## 4. Linux vs Windows vs macOS

All three operating systems manage hardware, memory, processes, files, and applications, but their internal architectures and ecosystems differ.

| Feature | Linux | Windows | macOS |
|---|---|---|---|
| Kernel architecture | Modular monolithic | Hybrid NT architecture | Hybrid XNU architecture |
| Kernel | Linux | Windows NT | XNU |
| Source model | Open source | Proprietary | XNU source available; macOS largely proprietary |
| Executable format | ELF | PE | Mach-O |
| Common filesystems | ext4, XFS, Btrfs | NTFS, FAT32, exFAT | APFS, HFS+ |
| Common distributions/versions | Ubuntu, Fedora, Debian | Windows 10, Windows 11 | macOS releases |

### Kernel Architecture

- Linux uses a modular monolithic kernel.
- Windows uses the Windows NT hybrid architecture.
- macOS uses the XNU hybrid kernel, combining technologies from Mach and BSD, along with IOKit.

### Executable Formats

| Operating System | Common Executable Format |
|---|---|
| Linux | ELF |
| Windows | PE |
| macOS | Mach-O |

An executable format defines how an operating system recognizes and loads program files.

## 5. What Happens When You Open an Application?

Opening an application involves several operating-system operations.

A simplified process:

1. **Application launch request:** The user requests to open an application.
2. **Executable loading:** The operating system locates and loads the executable.
3. **Library loading:** Required shared libraries or frameworks are made available.
4. **Process creation:** The operating system creates a process.
5. **Memory allocation:** The process receives virtual memory.
6. **Thread creation:** The application may create one or more execution threads.
7. **CPU scheduling:** The scheduler provides CPU time.
8. **Application execution:** The application begins performing its tasks.

### Process Creation Differences

- Linux commonly uses `fork()` and `execve()`, or `posix_spawn()` in some situations.
- Windows uses `CreateProcess()`.
- macOS commonly uses `posix_spawn()` and application-launch services.

These are different operating-system mechanisms that help create and launch processes.

## 6. Understanding Deadlock

A **deadlock** is a situation in which two or more processes are permanently waiting for resources held by one another.

As a result, none of the involved processes can continue.

### Example

Imagine two processes:

- Process A holds Resource 1 and waits for Resource 2.
- Process B holds Resource 2 and waits for Resource 1.

Neither process can continue because each is waiting for the other.

### Four Necessary Conditions of Deadlock

All four conditions must exist simultaneously for a deadlock to occur.

| Condition | Explanation |
|---|---|
| Mutual Exclusion | A resource can be used by only one process at a time |
| Hold and Wait | A process holds one resource while waiting for another |
| No Preemption | Resources cannot be forcibly taken away |
| Circular Wait | Processes form a circular chain of resource waiting |

### Ways to Prevent Deadlock

- Maintain a consistent order when acquiring locks.
- Avoid holding resources unnecessarily while waiting.
- Use timeouts where appropriate.
- Release resources properly.
- Design synchronization carefully.

Deadlock is possible in Linux, Windows, and macOS.

---

# 🖥️ Chapter 2: Bringing Linux Home

## 1. Ways to Use Linux

There are several ways to use Linux on a computer.

### Method 1: WSL2

WSL stands for **Windows Subsystem for Linux**.

WSL2 allows users to run a Linux environment inside Windows without setting up a traditional dual-boot system.

Basic installation process:

1. Open PowerShell as Administrator.
2. Execute:

```powershell
wsl --install
```

3. Restart the computer if required.
4. Open the installed Ubuntu distribution.
5. Create a Linux username and password.

**Important:** While entering a Linux password in the terminal, the characters usually do not appear on the screen. This is normal.

WSL2 is specifically for Windows.

### Method 2: Virtual Machine

A virtual machine is a software-based computer that runs inside a physical computer.

Virtualization software allows a computer to run another operating system independently.

For example:

- Physical computer: macOS
- Virtual machine: Ubuntu Linux

The book recommends approximately:

| Resource | Suggested Amount |
|---|---|
| Virtual machine RAM | 4 GB |
| Virtual disk | 25 GB |
| Physical host RAM | Ideally 8 GB or more |

These are learning recommendations, not universal minimum requirements.

### Important VM Terms

**ISO File:** An ISO is a disk-image file commonly used to install an operating system.

**Virtual Machine:** A software-based computer with virtual CPU, RAM, storage, and networking.

**Virtual Disk:** A file on the physical computer that acts as the VM's storage drive.

### Apple Silicon Consideration

For an Apple Silicon MacBook, use an ARM64/AArch64-compatible Linux image and virtualization software that supports Apple Silicon.

Do not assume that an x86 Ubuntu image or every virtualization application will work on an M-series Mac.

### Method 3: Dual Boot

Dual boot means installing two operating systems on the same physical computer.

At startup, the user chooses which operating system to run.

Example:

- Windows
- Linux

**Advantages:**

- Both operating systems run directly on the physical hardware.
- Useful for users who need native operating-system access.

**Disadvantages:**

- Requires disk partitioning.
- Installation mistakes can cause data loss.
- Requires careful backup and configuration.

Dual boot is not the recommended starting method for beginners.

## 2. Using Linux Concepts on macOS

macOS has a Unix-like command-line environment.

Many basic commands are similar to Linux commands.

Examples:

```bash
pwd
ls
cd
mkdir
touch
cp
mv
rm
find
grep
```

However, macOS uses its own system components and command implementations.

For example:

- macOS Terminal normally opens Zsh by default.
- Linux distributions commonly use Bash, although other shells are available.
- Some GNU/Linux command options are not available in macOS versions.

**Learning strategy:** Practise common commands on macOS first, then use Ubuntu for Linux-specific administration.

## 3. First Commands

### `echo`

**Purpose:** Displays text or the value of a shell variable.

Syntax:

```bash
echo [OPTION] [STRING]
```

Example:

```bash
echo "Hello Linux"
```

Output:

```text
Hello Linux
```

### `$USER`

`$USER` is a shell variable that commonly stores the current username.

Example:

```bash
echo $USER
```

It displays the username stored in the variable.

Remember that `$USER` is a variable, not a command.

---

# ⌨️ Chapter 3: Understanding the Language of Linux

## 1. Terminal vs Shell vs Bash

These terms are related, but they have different meanings.

### Terminal

A terminal is an application or interface where users enter commands and view their output.

Examples:

- macOS Terminal
- GNOME Terminal
- Konsole

### Shell

A shell is a command interpreter.

It receives commands, interprets them, and requests the operating system to perform the required operations.

### Bash

Bash stands for **Bourne Again Shell**.

It is a widely used Unix shell that supports:

- Command execution
- Variables
- Command history
- Loops
- Conditions
- Shell scripting
- Automation

Other popular shells include:

- Zsh
- Fish

### Relationship

```text
User
  |
  v
Terminal
  |
  v
Shell (Bash / Zsh / Fish)
  |
  v
Operating System
```

**Important:** macOS Terminal normally uses Zsh by default, not Bash.

## 2. Understanding the Linux Prompt

Example:

```bash
rahim@laptop:~$
```

Each part has a meaning.

| Part | Meaning |
|---|---|
| `rahim` | Username |
| `@` | Separates username and hostname |
| `laptop` | Hostname |
| `~` | Current user's home directory |
| `$` | Normal-user prompt |

### `$` vs `#`

- `$` usually indicates a normal user shell.
- `#` usually indicates a root shell.

Do not type the `$` or `#` prompt symbol when copying a command from a tutorial.

## 3. Command Structure

A common command structure is:

```bash
command -option argument
```

| Component | Purpose |
|---|---|
| Command | Performs an action |
| Option | Changes how the command works |
| Argument | Specifies the target or input |

Example:

```bash
ls -l /home
```

- `ls` = command
- `-l` = option
- `/home` = argument

### Common `ls` Options

```bash
ls
```

Lists directory contents.

```bash
ls -l
```

Displays detailed information.

```bash
ls -a
```

Displays hidden files and directories.

```bash
ls -la
```

Combines long-format and hidden-file listings.

## 4. Linux Is Case-Sensitive

Linux filenames and command names are case-sensitive.

For example:

```bash
ls
```

is different from:

```bash
LS
```

Similarly:

```text
Hello.txt
hello.txt
HELLO.txt
```

These are different filenames on a case-sensitive filesystem.

## 5. Understanding Spaces

Spaces separate commands, options, and arguments.

Correct:

```bash
ls -l
```

Incorrect:

```bash
ls-l
```

The second command is interpreted as a different command name.

## 6. Getting Help

When you do not understand a command, use its help information.

### Method 1: `--help`

Displays short help information for many GNU commands.

Example:

```bash
ls --help
```

### Method 2: `man`

Displays the manual page of a command.

Example:

```bash
man ls
```

Useful manual navigation:

| Key | Action |
|---|---|
| Up Arrow | Move upward |
| Down Arrow | Move downward |
| Space | Next page |
| `q` | Quit the manual |

### macOS Note

Many macOS commands use BSD versions rather than GNU versions.

For example, `ls --help` may not work on macOS.

Use:

```bash
man ls
```

for detailed documentation.

## 7. Basic Commands

### `date`

Displays the current date and time.

```bash
date
```

### `whoami`

Displays the effective username of the current user.

```bash
whoami
```

### `$USER` vs `whoami`

| `$USER` | `whoami` |
|---|---|
| Shell variable | Command |
| Displays the value stored in the variable | Reports the effective user identity |
| Can depend on shell environment | Reports the identity used by the running process |

They often display the same username, but they are not guaranteed to match in every situation.

---

# 📂 Chapter 4: Exploring the Linux Filesystem

## 1. Understanding the Linux Filesystem

Linux uses a hierarchical filesystem structure.

The filesystem starts from a single root directory:

```text
/
```

Everything in the Linux directory structure exists under this root.

Unlike Windows, which commonly uses drive letters such as `C:` and `D:`, Linux organizes its filesystem under `/`.

## 2. Important Linux Directories

### Main Directories

| Directory | Purpose |
|---|---|
| `/` | Root of the entire filesystem |
| `/home` | Home directories of normal users |
| `/root` | Home directory of the root user |
| `/etc` | System configuration files |
| `/var` | Variable data, logs, caches, and application data |
| `/usr` | Many installed programs and supporting files |
| `/bin` | Essential user commands; often merged into `/usr/bin` on modern distributions |
| `/tmp` | Temporary files |

### Additional Important Directories

| Directory | Purpose |
|---|---|
| `/boot` | Files required for booting the system |
| `/dev` | Device files representing hardware and virtual devices |
| `/proc` | Virtual filesystem providing process and kernel information |
| `/sys` | Virtual filesystem exposing device and kernel information |
| `/opt` | Optional application software |
| `/mnt` | Common temporary mount point |
| `/media` | Common mount point for removable media |
| `/srv` | Data served by system services |

### Examples of Files Inside Directories

#### `/etc`

Contains system configuration.

Examples:

```text
/etc/passwd
/etc/group
/etc/hostname
/etc/hosts
/etc/fstab
/etc/ssh/
/etc/apt/
```

#### `/var`

Contains changing system and application data.

Examples:

```text
/var/log/
/var/cache/
/var/lib/
/var/mail/
/var/spool/
/var/tmp/
```

#### `/usr`

Contains many installed programs and supporting resources.

Examples:

```text
/usr/bin/
/usr/sbin/
/usr/lib/
/usr/local/
/usr/share/
/usr/include/
```

#### `/boot`

Contains boot-related files.

Examples may include:

```text
vmlinuz
initrd.img
grub/
```

#### `/dev`

Contains device files.

Examples:

```text
/dev/null
/dev/zero
/dev/random
/dev/tty
/dev/sda
```

The exact devices depend on the machine.

#### `/proc`

Provides virtual information about running processes and the kernel.

Examples:

```text
/proc/cpuinfo
/proc/meminfo
/proc/version
```

It also contains directories named after process IDs.

#### `/sys`

Provides information about devices, drivers, and kernel interfaces through a virtual filesystem.

### Important macOS Difference

Linux commonly stores normal users' home directories under:

```text
/home/username
```

macOS normally uses:

```text
/Users/username
```

## 3. Absolute vs Relative Paths

### Absolute Path

An absolute path starts from the filesystem root `/`.

Example:

```text
/home/rahim/projects
```

It identifies a location independently of the current directory.

### Relative Path

A relative path describes a location from the current working directory.

Example:

```text
projects
```

Its meaning depends on where you currently are.

| Absolute Path | Relative Path |
|---|---|
| Starts from `/` | Starts from the current directory |
| Independent of current location | Depends on current location |
| Example: `/home/rahim` | Example: `rahim` |

## 4. Navigation Commands

### `pwd`

Stands for **Print Working Directory**.

Displays the current directory.

```bash
pwd
```

### `cd`

Stands for **Change Directory**.

Used to move between directories.

```bash
cd /tmp
```

Moves to `/tmp`.

```bash
cd ~
```

Moves to the current user's home directory.

```bash
cd
```

Also moves to the home directory.

```bash
cd ..
```

Moves one directory level upward.

```bash
cd -
```

Returns to the previous working directory.

### Understanding `~`

The tilde (`~`) represents the current user's home directory.

Example:

```bash
cd ~/Documents
```

Moves to the Documents directory inside the current user's home directory, if it exists.

### Tab Completion

Pressing the Tab key helps complete filenames and directory names.

Example:

```bash
cd Doc
```

Press Tab to complete the name if the match is unambiguous.

If multiple matches exist, pressing Tab again may display available options.

## 5. Understanding File Permissions

Linux uses permissions to control who can access files and directories.

There are three main permission categories:

| Category | Symbol | Meaning |
|---|---|---|
| User | `u` | Owner of the file |
| Group | `g` | Users belonging to the file's group |
| Others | `o` | All other users |
| All | `a` | User, group, and others |

### Three Basic Permissions

| Permission | Symbol | Numeric Value |
|---|---|---|
| Read | `r` | 4 |
| Write | `w` | 2 |
| Execute | `x` | 1 |

### Meaning for Files

| Permission | Meaning |
|---|---|
| Read (`r`) | Read the file's contents |
| Write (`w`) | Modify the file's contents |
| Execute (`x`) | Run the file as a program or script, subject to other requirements |

### Meaning for Directories

Directory permissions work differently.

| Permission | Meaning |
|---|---|
| Read (`r`) | List directory entries, subject to other permissions |
| Write (`w`) | Create, delete, or rename entries, subject to other restrictions |
| Execute (`x`) | Traverse or access the directory |

**Important:** Deleting a file generally depends on write and execute permissions on its parent directory, not simply on the file's own write permission.

You also need execute permission on the relevant parent directories in a path to access something inside them.

## 6. Reading Permission Output

Run:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 rahim developers 1200 Jul 12 10:30 notes.txt
```

Understanding the first part:

```text
-rw-r--r--
```

| Part | Meaning |
|---|---|
| `-` | Regular file |
| `rw-` | Owner permissions |
| `r--` | Group permissions |
| `r--` | Others permissions |

The first character indicates the file type:

| Symbol | Meaning |
|---|---|
| `-` | Regular file |
| `d` | Directory |
| `l` | Symbolic link |

### Useful Inspection Commands

```bash
ls -l
```

Displays detailed information about directory contents.

```bash
ls -ld /etc
```

Displays information about the `/etc` directory itself.

```bash
ls -l /etc/passwd
```

Displays information about the specified file.

```bash
ls -la
```

Displays detailed information, including hidden entries.

## 7. Changing Permissions and Ownership

### `chmod`

`chmod` means **Change Mode**.

It changes file or directory permissions.

#### Symbolic Method

```bash
chmod g+w file.txt
```

Adds write permission for the group.

```bash
chmod o-r file.txt
```

Removes read permission from others.

```bash
chmod a+r file.txt
```

Adds read permission for everyone.

```bash
chmod +x script.sh
```

Adds execute permission according to the command's default target classes.

### Numeric Method

Permission values:

- Read = 4
- Write = 2
- Execute = 1

Add the values to calculate each permission group.

#### Example: `chmod 755`

```bash
chmod 755 script.sh
```

Calculation:

| Category | Calculation | Permission |
|---|---|---|
| Owner | 4 + 2 + 1 = 7 | `rwx` |
| Group | 4 + 0 + 1 = 5 | `r-x` |
| Others | 4 + 0 + 1 = 5 | `r-x` |

Final permission:

```text
rwxr-xr-x
```

#### Example: `chmod 644`

```bash
chmod 644 notes.txt
```

Calculation:

| Category | Calculation | Permission |
|---|---|---|
| Owner | 4 + 2 = 6 | `rw-` |
| Group | 4 | `r--` |
| Others | 4 | `r--` |

Final permission:

```text
rw-r--r--
```

**Security warning:** Avoid using `chmod 777` without a specific reason. It gives everyone read, write, and execute permissions.

### `chown`

`chown` means **Change Owner**.

Changes the ownership of a file or directory.

```bash
chown user file.txt
```

Changes the owner.

```bash
sudo chown user:group file.txt
```

Changes the owner and group.

### `sudo`

`sudo` allows an authorized user to execute a command with elevated privileges.

Example:

```bash
sudo command
```

Use elevated privileges only when necessary. A command executed with `sudo` can make system-wide changes.

### User and Group Inspection

```bash
whoami
```

Shows the effective username.

```bash
groups
```

Shows the groups associated with the current user.

On Linux, additional user and group information can be found in:

```text
/etc/passwd
/etc/group
```

---

# 📁 Chapter 5: Managing Files and Directories

This chapter focuses on creating, copying, moving, renaming, and deleting files and directories.

## 1. `mkdir` — Create Directories

`mkdir` stands for **Make Directory**.

Syntax:

```bash
mkdir directory_name
```

Example:

```bash
mkdir khelna
```

Creates a directory named `khelna`.

### Creating Multiple Directories

```bash
mkdir khabar ghum
```

Creates two directories:

```text
khabar/
ghum/
```

### Creating Nested Directories

```bash
mkdir -p khelna/bol/lal
```

Creates the complete directory structure.

The `-p` option means **parents**.

It automatically creates missing parent directories.

More explanation is available in the dedicated section below.

## 2. `touch` — Create Files

`touch` creates an empty file if it does not already exist.

Syntax:

```bash
touch filename
```

Example:

```bash
touch note.txt
```

Creates an empty file named `note.txt`.

### Creating Multiple Files

```bash
touch file1.txt file2.txt file3.txt
```

Creates three empty files.

**Additional clarification:** If a file already exists, `touch` normally updates its modification timestamp rather than deleting or replacing its contents.

## 3. `cp` — Copy Files and Directories

`cp` means **Copy**.

Syntax:

```bash
cp source destination
```

### Copy a File

```bash
cp note.txt note-backup.txt
```

Creates a copy named `note-backup.txt`.

### Copy a File into a Directory

```bash
cp note.txt khelna/
```

Copies `note.txt` into the `khelna` directory.

### Copy a Directory

```bash
cp -r khelna khelna2
```

The `-r` option means recursive copying.

It allows the command to copy a directory and its contents.

Without the recursive option, copying a directory normally produces an error.

## 4. `mv` — Move and Rename

`mv` means **Move**.

It can move files and directories or rename them.

### Move a File

```bash
mv note-backup.txt ghum/
```

Moves `note-backup.txt` into the `ghum` directory.

### Rename a File

```bash
mv note.txt diary.txt
```

Renames `note.txt` to `diary.txt`.

### Move and Rename Together

```bash
mv diary.txt ghum/new-diary.txt
```

Moves the file into `ghum` and gives it the new name `new-diary.txt`.

## 5. `rm` — Remove Files and Directories

`rm` means **Remove**.

### Delete a File

```bash
rm diary.txt
```

Deletes the file.

### Delete a Directory and Its Contents

```bash
rm -r khelna2
```

The `-r` option means recursive removal.

### Force Removal

```bash
rm -f file.txt
```

The `-f` option means force.

### Recursive Force Removal

```bash
rm -rf folder
```

Combines recursive removal and force.

**Important safety warning:**

- `rm` normally does not move files to a Recycle Bin.
- Deleted files may be difficult or impossible to recover.
- Always check the path before running removal commands.
- Never experiment with dangerous removal commands on important system directories.

## 6. Hidden Files

In Unix-like systems, filenames beginning with a dot (`.`) are normally treated as hidden.

Examples:

```text
.bashrc
.profile
```

### List Hidden Files

```bash
ls -a
```

Displays hidden entries.

### Shell Configuration Files

`.bashrc` is commonly used to store Bash configuration.

It can contain:

- Aliases
- Shell variables
- Custom settings
- Command-related configuration

macOS normally uses Zsh by default, so its common interactive shell configuration file is `.zshrc`.

## 7. Wildcards

Wildcards allow commands to match multiple filenames.

### `*` — Match Any Number of Characters

The asterisk matches zero or more characters.

Example:

```bash
ls note*
```

Matches filenames beginning with `note`.

Example:

```bash
mv *.jpg chobi/
```

Moves all matching `.jpg` files into the `chobi` directory.

### `?` — Match Exactly One Character

Example:

```bash
ls note?.txt
```

Can match:

```text
note1.txt
note2.txt
noteA.txt
```

But it does not match:

```text
note10.txt
```

because `?` represents exactly one character.

**Safety tip:** Before using a wildcard with `rm`, inspect the matching files.

For example:

```bash
ls *.txt
```

Then decide whether deletion is appropriate.

## 8. Understanding the `-p` Option in `mkdir`

The `-p` option means **parents**.

It is used to create missing parent directories automatically.

### Without `-p`

```bash
mkdir animals/cats/persian
```

If `animals` and `cats` do not exist, the command fails because the parent directories are missing.

You would need to create them one by one:

```bash
mkdir animals
mkdir animals/cats
mkdir animals/cats/persian
```

### With `-p`

```bash
mkdir -p animals/cats/persian
```

Creates the entire directory structure in one command:

```text
animals/
└── cats/
    └── persian/
```

### Another Important Behaviour

If the directory already exists:

```bash
mkdir -p animals
```

The command does not report an error just because `animals` already exists.

### Comparison

| Command | Behaviour |
|---|---|
| `mkdir folder` | Creates one directory |
| `mkdir -p a/b/c` | Creates missing parent directories |
| `mkdir -p folder` | Does not complain if the directory already exists |

**When to use it:** Use `mkdir -p` whenever you want to create nested directories in one command or safely ensure a directory exists.

---

# 🔎 Chapter 6: Finding Lost Files

Chapter 6 introduces commands for locating files, searching inside files, and finding program locations.

The five important commands are:

1. `find`
2. `grep`
3. `which`
4. `whereis`
5. `locate`

## 1. `find` — Search for Files and Directories

**Purpose:** Searches for files and directories inside a specified location.

Syntax:

```bash
find location -name "filename"
```

### Practical Setup

```bash
cd ~

mkdir -p bari/ghor1 bari/ghor2/khat-er-niche

touch bari/ghor1/linu-r-bol.txt

touch bari/ghor2/khat-er-niche/linu.txt

touch bari/mach.jpg
```

This creates:

```text
bari/
├── ghor1/
│   └── linu-r-bol.txt
├── ghor2/
│   └── khat-er-niche/
│       └── linu.txt
└── mach.jpg
```

### Find a Specific File

```bash
find bari -name "linu.txt"
```

Example output:

```text
bari/ghor2/khat-er-niche/linu.txt
```

The command searches through subdirectories and displays the matching path.

### Search Using Wildcards

```bash
find bari -name "linu*"
```

Finds names beginning with `linu`.

```bash
find bari -name "*.jpg"
```

Finds files whose names end with `.jpg`.

### Search Only for Directories

```bash
find bari -type d
```

Here:

- `-type` specifies the type of item.
- `d` means directory.

### Search Only for Regular Files

```bash
find bari -type f
```

Here, `f` means regular file.

### Search the Home Directory

```bash
find ~ -name "*.pdf"
```

Finds PDF files inside the current user's home directory and its subdirectories.

### Case-Insensitive Filename Search

```bash
find bari -iname "LINU*"
```

`-iname` ignores uppercase and lowercase differences.

It can match:

```text
linu.txt
LINU.txt
Linu.txt
```

### Searching the Entire Filesystem

```bash
find / -name "something"
```

Starts searching from the root directory.

You may see:

```text
Permission denied
```

This happens when your normal user does not have permission to access certain locations.

It is a permission issue, not necessarily a command error.

Start with a specific directory when practising because searching the entire filesystem can take longer.

## 2. `grep` — Search Inside Files

**Purpose:** Searches for specific words or text inside files.

### `find` vs `grep`

- `find` searches for files and directories.
- `grep` searches for text inside files.

### Practical Example

Create a diary:

```bash
cd ~

echo "linu ke tika dite hobe 15 tarikh" > diary.txt

echo "aj linu saradin ghumiyeche" >> diary.txt

echo "linu r khabar sesh, kinte hobe" >> diary.txt
```

The meanings of `>` and `>>` will be studied in Chapter 9.

Now search for `tika`:

```bash
grep "tika" diary.txt
```

Output:

```text
linu ke tika dite hobe 15 tarikh
```

`grep` displays the matching line rather than printing the entire file.

### Useful `grep` Options

#### `-i` — Ignore Case

```bash
grep -i "LINU" diary.txt
```

Matches text without distinguishing uppercase and lowercase letters.

#### `-n` — Display Line Numbers

```bash
grep -n "linu" diary.txt
```

Example output:

```text
1:linu ke tika dite hobe 15 tarikh
2:aj linu saradin ghumiyeche
3:linu r khabar sesh, kinte hobe
```

#### `-r` — Recursive Search

```bash
grep -r "tika" ~/bari
```

Searches through files inside a directory and its subdirectories.

#### `-c` — Count Matching Lines

```bash
grep -c "linu" diary.txt
```

Displays the number of matching lines.

#### Combine Options

```bash
grep -rn "password" project/
```

This searches recursively and displays matching line numbers.

Useful when searching through a large programming project containing many files.

## 3. `which` — Find a Command Location

**Purpose:** Finds the executable selected through the shell's command search path.

Example:

```bash
which ls
```

Example output:

```text
/usr/bin/ls
```

This indicates the executable location selected for the `ls` command.

Other examples:

```bash
which grep
which python3
which git
```

Use `which` when you want to know which executable your shell will run for a command.

## 4. `whereis` — Find Program-Related Files

**Purpose:** Searches for a program and related files, such as executable and manual locations.

Example:

```bash
whereis ls
```

It may return locations associated with the `ls` program.

### `which` vs `whereis`

| `which` | `whereis` |
|---|---|
| Finds the executable selected through the command search path | Searches standard locations for program-related files |
| Useful for checking which command will run | Useful for locating binaries and manual files |

## 5. `locate` — Search Using an Index

**Purpose:** Searches for filenames using a previously created database or index.

### How It Works

`find` searches directories directly.

`locate` searches a stored index of filenames and their locations.

Therefore, `locate` is generally faster for large filename searches.

However, the index may be outdated.

A recently created file may not appear until the index is updated.

### Installing `plocate` on Ubuntu/Debian

```bash
sudo apt install plocate
```

Search for a file:

```bash
locate diary.txt
```

**Platform note:** The `apt` installation command is for Ubuntu/Debian-based Linux distributions. It is not a standard macOS Terminal command.

## 6. Which Command Should You Use?

| Requirement | Command |
|---|---|
| Find a file by name | `find` |
| Find a directory | `find -type d` |
| Find regular files | `find -type f` |
| Find text inside files | `grep` |
| Find a command's executable | `which` |
| Find program-related files | `whereis` |
| Quickly search using a filename index | `locate` |

### Easy Memory Technique

```text
File name             → find
Text inside a file    → grep
Command location      → which
Program-related files → whereis
Indexed file search   → locate
```

---

# 🧪 Practical Exercises

These exercises combine the commands studied so far.

## Exercise 1: Create a Directory Structure

```bash
cd ~

mkdir -p songsar
cd songsar

mkdir khelna chobi
```

Create files:

```bash
touch bol1.txt bol2.txt bol3.txt mach1.jpg mach2.jpg dori.txt
```

Check the files:

```bash
ls
```

Move image files:

```bash
ls *.jpg
mv *.jpg chobi/
```

Move files beginning with `bol`:

```bash
mv bol* khelna/
```

Rename a file:

```bash
mv dori.txt rossi.txt
```

Move the renamed file:

```bash
mv rossi.txt khelna/
```

View the complete directory structure:

```bash
ls -R
```

Return to the home directory:

```bash
cd ~
```

Delete the practice directory when you no longer need it:

```bash
rm -r songsar
```

## Exercise 2: Search for Files

Create the practice structure:

```bash
cd ~

mkdir -p golokdhadha/ghor{1,2,3}/tak

touch golokdhadha/ghor1/purono-note.txt

touch golokdhadha/ghor2/tak/dorkari-file.txt

touch golokdhadha/ghor3/chobi.jpg

touch golokdhadha/ghor3/tak/aro-chobi.jpg

echo "linu r janmodin 12 December" > golokdhadha/ghor2/tak/dorkari-file.txt
```

Now complete the following:

**Task 1:** Find `dorkari-file.txt`.

```bash
find golokdhadha -name "dorkari-file.txt"
```

**Task 2:** Find all JPG files.

```bash
find golokdhadha -name "*.jpg"
```

**Task 3:** Find all directories.

```bash
find golokdhadha -type d
```

**Task 4:** Search for `janmodin`.

```bash
grep -rn "janmodin" golokdhadha
```

**Task 5:** Find the location of `grep`.

```bash
which grep
```

---

# ⚡ Important Command Cheat Sheet

A quick reference for all the important commands covered in Chapters 1–6.

| Command | Purpose | Example |
|---|---|---|
| `echo` | Display text | `echo "Hello"` |
| `date` | Display date and time | `date` |
| `whoami` | Show effective username | `whoami` |
| `pwd` | Show current directory | `pwd` |
| `ls` | List directory contents | `ls` |
| `ls -l` | Detailed listing | `ls -l` |
| `ls -a` | Show hidden entries | `ls -a` |
| `ls -la` | Detailed listing including hidden entries | `ls -la` |
| `cd` | Change directory | `cd /tmp` |
| `mkdir` | Create directory | `mkdir folder` |
| `mkdir -p` | Create missing parent directories | `mkdir -p a/b/c` |
| `touch` | Create empty file or update timestamp | `touch file.txt` |
| `cp` | Copy files | `cp a.txt b.txt` |
| `cp -r` | Copy directories recursively | `cp -r folder backup` |
| `mv` | Move or rename | `mv a.txt b.txt` |
| `rm` | Remove files | `rm file.txt` |
| `rm -r` | Remove directories recursively | `rm -r folder` |
| `chmod` | Change permissions | `chmod 755 script.sh` |
| `chown` | Change ownership | `sudo chown user file.txt` |
| `sudo` | Execute with elevated privileges | `sudo command` |
| `find` | Search by filename or type | `find . -name "*.txt"` |
| `grep` | Search inside files | `grep "word" file.txt` |
| `which` | Find command executable | `which ls` |
| `whereis` | Find program-related files | `whereis ls` |
| `locate` | Search indexed filenames | `locate file.txt` |
| `man` | Open manual | `man ls` |
| `--help` | Display command help where supported | `ls --help` |
| `groups` | Display user groups | `groups` |

---

# 🧠 Important Things to Remember

1. Linux is the kernel; Ubuntu, Fedora, and Debian are Linux distributions.
2. The kernel manages hardware resources and provides core operating-system services.
3. Terminal, Shell, and Bash are different concepts.
4. macOS Terminal normally uses Zsh by default.
5. Linux commands and filenames are case-sensitive.
6. The Linux filesystem starts from `/`.
7. `/root` is the root user's home directory, while `/` is the filesystem root.
8. Absolute paths start with `/`; relative paths depend on the current directory.
9. `pwd` displays the current directory.
10. `cd ..` moves to the parent directory.
11. `~` represents the current user's home directory.
12. `r`, `w`, and `x` represent read, write, and execute permissions.
13. File and directory permissions have different practical meanings.
14. `chmod` changes permissions, while `chown` changes ownership.
15. `mkdir -p` creates missing parent directories automatically.
16. `touch` creates an empty file if it does not exist.
17. `cp -r` is used to copy directories recursively.
18. `mv` can both move and rename files.
19. `rm -r` removes directories and their contents.
20. Filenames beginning with `.` are normally hidden.
21. `*` matches zero or more characters; `?` matches exactly one character.
22. `find` searches for files and directories.
23. `grep` searches for text inside files.
24. `which` finds the executable selected through the command search path.
25. `whereis` searches for program-related files.
26. `locate` uses an index and may return outdated results.
27. `sudo` provides elevated privileges and must be used carefully.

---

# 📈 Learning Progress

| Chapter | Topic | Status |
|---|---|---|
| 01 | Introduction to Linux | ✅ Completed |
| 02 | Bringing Linux Home | ✅ Completed |
| 03 | Understanding the Language of Linux | ✅ Completed |
| 04 | Exploring the Linux Filesystem | ✅ Completed |
| 05 | Managing Files and Directories | ✅ Completed |
| 06 | Finding Lost Files | ✅ Completed |
| 07 | Installing Software with Package Managers | ⏳ Upcoming |

---

# 🚀 Upcoming Chapters

The next topics in this learning journey will include:

- Package management and software installation.
- APT and repository management.
- Reading and writing files.
- Text editors, including Vim.
- Input/output redirection.
- Shell scripting and automation.
- Linux administration and practical system operations.

The notes will be expanded as each chapter is completed.

---

## 🎯 Final Goal

Build a strong foundation in Linux so that I can confidently work with:

- Linux command-line tools.
- Filesystem navigation and management.
- Users, groups, and permissions.
- Software installation and package management.
- Shell scripting and automation.
- Linux servers and system administration.

**Learning Linux is not just about knowing commands. It is about understanding how the operating system works and knowing how to use its tools effectively.**

---

*Last updated: November 2026*  
*Repository: Linux Learning Notes*  
*Coverage: Chapters 1–6*
