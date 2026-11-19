# Linux Command-Line Notes --- Chapters 7, 8 & 9



## Table of Contents

-   [Chapter 7 --- Package Management with
    APT](#chapter-7--package-management-with-apt)
    -   [What Is a Package Manager?](#what-is-a-package-manager)
    -   [Update the Package List](#1-update-the-package-list)
    -   [Upgrade Installed Packages](#2-upgrade-installed-packages)
    -   [Install Packages](#3-install-packages)
    -   [Search and Inspect Packages](#4-search-and-inspect-packages)
    -   [Remove Packages](#5-remove-packages)
    -   [Other Software Sources](#6-other-software-sources)
    -   [Chapter 7 Quick Reference](#chapter-7-quick-reference)
    -   [Chapter 7 Practice](#chapter-7-practice)
-   [Chapter 8 --- Reading and Writing
    Files](#chapter-8--reading-and-writing-files)
    -   [Create a Practice File](#create-a-practice-file)
    -   [cat](#1-cat--display-a-file)
    -   [less](#2-less--read-a-file-page-by-page)
    -   [head and tail](#3-head-and-tail--read-selected-lines)
    -   [tail -f](#4-tail--f--watch-a-file-live)
    -   [nano](#5-nano--edit-a-file)
    -   [vim](#6-vim--a-modal-text-editor)
    -   [Chapter 8 Quick Reference](#chapter-8-quick-reference)
    -   [Chapter 8 Practice](#chapter-8-practice)
-   [Chapter 9 --- Pipes and
    Redirection](#chapter-9--pipes-and-redirection)
    -   [Standard Input and Output](#standard-input-and-output)
    -   [Output Redirection: \>](#1-output-redirection-)
    -   [Append Redirection: \>\>](#2-append-redirection-)
    -   [Pipes: \|](#3-pipes---connect-commands)
    -   [Useful Commands for
        Pipelines](#4-useful-commands-for-pipelines)
    -   [Input Redirection:
        \<](#5-input-redirection---send-a-file-as-input)
    -   [Mini Project: Analyse a Visitor
        Log](#mini-project-analyse-a-visitor-log)
    -   [Chapter 9 Quick Reference](#chapter-9-quick-reference)
    -   [Chapter 9 Practice](#chapter-9-practice)
-   [Common Mistakes](#common-mistakes)
-   [Final Revision Checklist](#final-revision-checklist)
-   [Further Learning](#further-learning)

------------------------------------------------------------------------



# Chapter 7 --- Package Management with APT

## What Is a Package Manager?

A **package** is a software application or a component that an operating
system can install and manage.

A **package manager** helps you:

-   Find available software.
-   Install applications.
-   Update package information.
-   Upgrade installed applications.
-   Remove software that you no longer need.
-   Manage software dependencies.

On Ubuntu and Debian, a common package-management tool is **APT**
(Advanced Package Tool).

Think of APT as a software store that works through the terminal.

> **Remember:** APT commands shown in this chapter are for
> Ubuntu/Debian-based Linux. They are not macOS commands.

## 1. Update the Package List

``` bash
sudo apt update
```

### What does it do?

It downloads the latest package information from the configured software
repositories.

It does **not** upgrade or install all applications.

Think of it as refreshing the store's catalogue before shopping.

### Important parts

  Part       Meaning
  ---------- -----------------------------------------------
  `sudo`     Run the command with administrator privileges
  `apt`      Package-management tool
  `update`   Refresh package information

## 2. Upgrade Installed Packages

``` bash
sudo apt upgrade
```

### What does it do?

It installs available upgrades for packages that are already installed
on the system.

### Update vs. Upgrade

  -----------------------------------------------------------------------
  Command                 Purpose                 Simple comparison
  ----------------------- ----------------------- -----------------------
  `sudo apt update`       Refreshes package       Checks the latest store
                          information             catalogue

  `sudo apt upgrade`      Upgrades installed      Updates the software
                          packages                you already have
  -----------------------------------------------------------------------

A common maintenance command is:

``` bash
sudo apt update && sudo apt upgrade
```

### Why use `&&`?

`&&` runs the second command only if the first command finishes
successfully.

In this example:

1.  APT refreshes the package information.
2.  If that succeeds, APT upgrades installed packages.

## 3. Install Packages

### Install one package

``` bash
sudo apt install htop
```

This installs `htop`, an interactive process-monitoring tool.

After installation, run:

``` bash
htop
```

Press `q` to quit `htop`.

### Install multiple packages

``` bash
sudo apt install tree curl wget
```

APT can install several packages in one command.

  Package   Common purpose
  --------- -----------------------------------------------
  `tree`    Displays directories in a tree-like structure
  `curl`    Transfers data to or from a URL
  `wget`    Downloads files from the web
  `htop`    Displays running processes interactively

Try:

``` bash
cd ~
tree
```

If `tree` is not installed, install it first.

## 4. Search and Inspect Packages

You do not need to install a package just to learn about it.

### Search for a package

``` bash
apt search screenshot
```

Searches package names and descriptions for the word `screenshot`.

Another example:

``` bash
apt search cowsay
```

### Display package information

``` bash
apt show htop
```

This displays information such as:

-   Package name
-   Version
-   Description
-   Package size
-   Dependencies

### List installed packages

``` bash
apt list --installed
```

Displays packages currently installed through APT.

You can count the displayed lines with:

``` bash
apt list --installed | wc -l
```

The result may include a heading, so it is an approximate count rather
than a guaranteed exact package count.

### Do these commands need `sudo`?

Usually, no.

``` bash
apt search htop
apt show htop
apt list --installed
```

These commands inspect information. They do not normally change
installed software.

**General rule:** Reading information usually does not require `sudo`;
changing system software usually does.

## 5. Remove Packages

APT provides different removal commands.

### Remove a package

``` bash
sudo apt remove tree
```

Removes the package but normally leaves its system-wide configuration
files behind.

### Purge a package

``` bash
sudo apt purge tree
```

Removes the package and its package-managed system configuration files.

### Remove unused dependencies

``` bash
sudo apt autoremove
```

Removes packages that were installed automatically as dependencies but
are no longer needed.

### Remove vs. Purge

  -----------------------------------------------------------------------
  Command                             What happens
  ----------------------------------- -----------------------------------
  `sudo apt remove package-name`      Removes the package; configuration
                                      files may remain

  `sudo apt purge package-name`       Removes the package and its
                                      package-managed configuration files

  `sudo apt autoremove`               Removes unused automatically
                                      installed dependencies
  -----------------------------------------------------------------------

> **Caution:** Review APT's proposed changes before confirming. Do not
> assume every suggested removal is harmless.

## 6. Other Software Sources

Not every application is available in the default APT repositories.
Ubuntu/Debian systems may use other software distribution methods.

### A. `.deb` files

A `.deb` file is a Debian software package file.

For example:

``` bash
sudo apt install ./google-chrome-stable_current_amd64.deb
```

The `./` tells APT to use the local file in the current directory rather
than search for a package by name in the repositories.

Only install `.deb` files from official or trusted sources. Also make
sure the package architecture matches your system.

### B. PPA

**PPA** means Personal Package Archive.

A PPA is an additional software repository, often used to distribute
software or newer package versions.

Example syntax:

``` bash
sudo add-apt-repository ppa:owner/archive
sudo apt update
```

The repository name above is a placeholder, not a real repository to
add.

Adding a repository gives its publisher a route to provide software to
your system. Only add PPAs from publishers you trust.

### C. Snap

Snap is another application packaging and distribution system.

Example:

``` bash
sudo snap install code --classic
```

This example installs Visual Studio Code through Snap on a compatible
Ubuntu system where the Snap service is available.

### Which source should you use?

1.  Search the official distribution repositories first.
2.  If the application is not available, check the application's
    official website.
3.  Read the installation instructions and verify the source before
    installing.

Avoid unofficial download sites that offer modified or repackaged
installers.

## Chapter 7 Quick Reference

  -----------------------------------------------------------------------
  Command                             Purpose
  ----------------------------------- -----------------------------------
  `sudo apt update`                   Refresh package information

  `sudo apt upgrade`                  Upgrade installed packages

  `sudo apt install package`          Install a package

  `apt search keyword`                Search for packages

  `apt show package`                  Display package information

  `apt list --installed`              List installed packages

  `sudo apt remove package`           Remove a package

  `sudo apt purge package`            Remove a package and
                                      package-managed configuration

  `sudo apt autoremove`               Remove unused automatic
                                      dependencies

  `sudo snap install package`         Install a Snap package
  -----------------------------------------------------------------------

## Chapter 7 Practice

Try these tasks on an Ubuntu/Debian test environment:

1.  Refresh the package list.

2.  Search for `cowsay`.

3.  Display the information for `htop`.

4.  Install `tree` and run it in your home directory.

5.  Install `cowsay`, then run:

    ``` bash
    cowsay "Hello, Linux!"
    ```

6.  Install `fortune` and try:

    ``` bash
    fortune | cowsay
    ```

7.  Count the lines in the installed-package list:

    ``` bash
    apt list --installed | wc -l
    ```

8.  Practise the difference between `remove`, `purge`, and `autoremove`
    in a safe test environment.

------------------------------------------------------------------------

# Chapter 8 --- Reading and Writing Files

Linux provides several commands for reading and editing text files. Each
command is useful in a different situation.

## Create a Practice File

First, move to your home directory:

``` bash
cd ~
```

Create a diary file using `echo`:

``` bash
echo "Day 1: Linu came home" > linu-diary.txt
echo "Day 2: Linu scratched the sofa" >> linu-diary.txt
echo "Day 3: Linu went to the vet" >> linu-diary.txt
echo "Day 4: Linu ate fish" >> linu-diary.txt
echo "Day 5: Linu slept all day" >> linu-diary.txt
```

The first command creates or overwrites the file. The later commands
append new lines.

## 1. `cat` --- Display a File

### Syntax

``` bash
cat filename
```

Example:

``` bash
cat linu-diary.txt
```

Displays the complete content of the file in the terminal.

### When should you use `cat`?

Use it when:

-   The file is short.
-   You want to display the whole file quickly.
-   You want to combine the contents of multiple files.

Example:

``` bash
cat file1.txt file2.txt
```

Displays the content of `file1.txt` followed by `file2.txt`.

> `cat` is useful for short files. For a very large file, its output may
> scroll past the terminal screen.

## 2. `less` --- Read a File Page by Page

### Syntax

``` bash
less filename
```

Example:

``` bash
less linu-diary.txt
```

`less` opens an interactive viewer. It does not normally load the entire
file onto one terminal screen.

### Useful `less` controls

  Key                     Action
  ----------------------- ------------------------------
  `Space` or `PageDown`   Move down one page
  `PageUp`                Move up one page
  `↑` / `↓`               Move up or down
  `/keyword`              Search forward for a keyword
  `n`                     Go to the next search match
  `g`                     Go to the beginning
  `G`                     Go to the end
  `q`                     Quit

### `cat` vs. `less`

  `cat`                           `less`
  ------------------------------- -----------------------------------
  Displays the content directly   Opens an interactive viewer
  Best for short files            Useful for long files
  Output may scroll quickly       Lets you move through the file
  No built-in page navigation     Supports searching and navigation

**Easy rule:** Use `cat` for short files and `less` for long files.

## 3. `head` and `tail` --- Read Selected Lines

Sometimes you do not need the entire file. You may only need its
beginning or end.

### `head` --- Display the beginning

``` bash
head linu-diary.txt
```

By default, it displays the first 10 lines.

Display only the first 2 lines:

``` bash
head -n 2 linu-diary.txt
```

### `tail` --- Display the end

``` bash
tail linu-diary.txt
```

By default, it displays the last 10 lines.

Display only the last 2 lines:

``` bash
tail -n 2 linu-diary.txt
```

### Quick comparison

  Command                Purpose
  ---------------------- ----------------
  `head file.txt`        First 10 lines
  `head -n 5 file.txt`   First 5 lines
  `tail file.txt`        Last 10 lines
  `tail -n 5 file.txt`   Last 5 lines

## 4. `tail -f` --- Watch a File Live

One of the most useful commands for monitoring log files is:

``` bash
tail -f linu-diary.txt
```

### What does `-f` mean?

`-f` means **follow**.

The command keeps running and displays new lines when they are added to
the file.

### Try a live demonstration

Open two terminal windows.

**Terminal 1:**

``` bash
tail -f ~/linu-diary.txt
```

**Terminal 2:**

``` bash
echo "Day 6: Linu learned something new" >> ~/linu-diary.txt
```

Look at Terminal 1. The new line should appear automatically.

Stop the live monitoring with:

``` text
Ctrl + C
```

### Real-world use case

A system administrator may monitor a web server log:

``` bash
tail -f /var/log/nginx/access.log
```

This can show new access-log entries as requests arrive. You need
suitable permissions to read some system log files.

## 5. `nano` --- Edit a File

`nano` is a beginner-friendly terminal text editor.

### Open or create a file

``` bash
nano linu-diary.txt
```

You can now type, delete, and edit text.

### Important nano shortcuts

  Shortcut     Action
  ------------ ------------------------
  `Ctrl + O`   Write Out (save)
  `Enter`      Confirm the filename
  `Ctrl + X`   Exit
  `Ctrl + K`   Cut the current line
  `Ctrl + U`   Paste the cut text
  `Ctrl + W`   Search within the file

In nano's help bar, `^` means the Ctrl key. For example, `^X` means
`Ctrl + X`.

### Save and exit

1.  Press `Ctrl + O`.
2.  Press `Enter` to confirm the filename.
3.  Press `Ctrl + X` to exit.

If you try to exit with unsaved changes, nano asks whether you want to
save them.

## 6. `vim` --- A Modal Text Editor

`vim` is a powerful terminal text editor. It uses different modes for
entering text and running editing commands.

Open a file:

``` bash
vim test.txt
```

### The two modes to know

  Mode          Purpose
  ------------- -----------------------------------
  Normal mode   Navigate and run editing commands
  Insert mode   Type text into the file

### Essential Vim commands

  Key or command   Action
  ---------------- -----------------------------
  `i`              Enter Insert mode
  `Esc`            Return to Normal mode
  `:w`             Save
  `:q`             Quit
  `:wq`            Save and quit
  `:q!`            Quit without saving changes

### How to exit Vim

If you accidentally open Vim and only want to leave:

1.  Press `Esc`.
2.  Type `:q!`.
3.  Press `Enter`.

### How to edit and save

1.  Open a file:

    ``` bash
    vim test.txt
    ```

2.  Press `i` and type your text.

3.  Press `Esc`.

4.  Type `:wq`.

5.  Press `Enter`.

Verify the content:

``` bash
cat test.txt
```

> You do not need to master Vim immediately. Knowing how to enter Insert
> mode, return to Normal mode, save, and exit is a useful starting
> point.

## Chapter 8 Quick Reference

  Command                Purpose
  ---------------------- -----------------------------------
  `cat file.txt`         Display the complete file
  `less file.txt`        Read a file page by page
  `head file.txt`        Display the first 10 lines
  `head -n 5 file.txt`   Display the first 5 lines
  `tail file.txt`        Display the last 10 lines
  `tail -n 5 file.txt`   Display the last 5 lines
  `tail -f file.txt`     Follow new lines live
  `nano file.txt`        Edit a file with Nano
  `vim file.txt`         Open a file in Vim
  `Ctrl + C`             Stop a running foreground command

## Chapter 8 Practice

1.  Create a file named `my-goals.txt` using Nano.

2.  Write at least five lines and save the file.

3.  Display the file using `cat`.

4.  Display only its first line using:

    ``` bash
    head -n 1 my-goals.txt
    ```

5.  Display only its last two lines using:

    ``` bash
    tail -n 2 my-goals.txt
    ```

6.  Open `/etc/passwd` with `less`, search for `root`, go to the end
    with `G`, and quit with `q`.

7.  Practise `tail -f` in two terminal windows.

8.  Open `test.txt` in Vim, enter two lines, save with `:wq`, and verify
    with `cat`.

------------------------------------------------------------------------

# Chapter 9 --- Pipes and Redirection

This chapter introduces one of the most powerful ideas in Linux:
connecting small commands to perform larger tasks.

## Standard Input and Output

A command can receive input, process it, and produce output.

Linux commonly uses three standard data streams:

  ------------------------------------------------------------------------
  Stream           Name                   File descriptor Purpose
  ---------------- ---------------- --------------------- ----------------
  Standard input   `stdin`                            `0` Data received by
                                                          a command

  Standard output  `stdout`                           `1` Normal output
                                                          produced by a
                                                          command

  Standard error   `stderr`                           `2` Error messages
                                                          produced by a
                                                          command
  ------------------------------------------------------------------------

By default, input usually comes from the keyboard, while output and
error messages usually appear in the terminal.

Redirection lets us change where input comes from or where output goes.

## 1. Output Redirection: `>`

### Syntax

``` bash
command > filename
```

The `>` operator sends a command's standard output to a file instead of
displaying it in the terminal.

Example:

``` bash
ls -l > file-list.txt
```

Now display the saved output:

``` bash
cat file-list.txt
```

### What happened?

1.  `ls -l` generated a directory listing.
2.  `>` redirected that output.
3.  The output was saved in `file-list.txt`.

### Important warning

`>` creates a file if it does not exist. If the file already exists, its
previous content is normally overwritten.

For example:

``` bash
echo "Old content" > example.txt
echo "New content" > example.txt
cat example.txt
```

Output:

``` text
New content
```

The old content was replaced.

## 2. Append Redirection: `>>`

The `>>` operator adds output to the end of a file without removing its
existing content.

Example:

``` bash
echo "Day 1: Linu came home" > diary.txt
echo "Day 2: Linu played" >> diary.txt
echo "Day 3: Linu slept" >> diary.txt
```

Display the file:

``` bash
cat diary.txt
```

Output:

``` text
Day 1: Linu came home
Day 2: Linu played
Day 3: Linu slept
```

### `>` vs. `>>`

  Operator   Meaning                      Existing content
  ---------- ---------------------------- ------------------
  `>`        Create or overwrite a file   Replaced
  `>>`       Append to a file             Preserved

**Easy rule:**

-   One arrow (`>`) = write from the beginning; existing content is
    overwritten.
-   Two arrows (`>>`) = add to the end; existing content is preserved.

## 3. Pipes: `|` --- Connect Commands

A **pipe** sends the standard output of one command to the standard
input of another command.

### Syntax

``` bash
command1 | command2
```

Think of it as:

``` text
Command 1 output  --->  Command 2 input
```

### Example 1: Read a long directory listing page by page

``` bash
ls /usr/bin | less
```

`ls /usr/bin` produces a list of files. The pipe sends that list to
`less`, allowing you to browse it page by page.

Press `q` to quit.

### Example 2: Search command names

``` bash
ls /usr/bin | grep zip
```

How it works:

1.  `ls /usr/bin` lists entries in `/usr/bin`.
2.  `|` sends the list to `grep`.
3.  `grep zip` displays lines containing `zip`.

### Example 3: Count the results

``` bash
ls /usr/bin | grep zip | wc -l
```

The commands work in sequence:

``` text
ls /usr/bin
     |
     v
grep zip
     |
     v
wc -l
     |
     v
Number of matching lines
```

This is the basic idea behind a command pipeline.

## 4. Useful Commands for Pipelines

### A. `wc` --- Count lines, words, and bytes

`wc` means **word count**.

Basic syntax:

``` bash
wc filename
```

Useful options:

  Option   Meaning
  -------- ------------------
  `-l`     Count lines
  `-w`     Count words
  `-c`     Count bytes
  `-m`     Count characters

Examples:

``` bash
wc linu-diary.txt
wc -l linu-diary.txt
wc -w linu-diary.txt
wc -c linu-diary.txt
```

### Why does `wc -l` sometimes show a filename?

Compare:

``` bash
wc -l otithi-khata.txt
```

Possible output:

``` text
10 otithi-khata.txt
```

Here, the filename is passed directly as a command-line argument.

Now compare:

``` bash
wc -l < otithi-khata.txt
```

Output:

``` text
10
```

Here, `<` redirects the file into the command's standard input. Since
`wc` receives standard input rather than a named file argument, it
displays the count without the filename.

Both commands count the lines. The difference is how the input is
provided and how the output is labelled.

### B. `sort` --- Sort lines

Basic syntax:

``` bash
sort filename
```

Example:

``` bash
sort names.txt
```

Sort numbers numerically:

``` bash
sort -n numbers.txt
```

Sort in reverse order:

``` bash
sort -r names.txt
```

Sort numbers in descending order:

``` bash
sort -rn numbers.txt
```

  Option   Meaning
  -------- ---------------------------
  `-n`     Numeric sorting
  `-r`     Reverse the sorting order

### C. `uniq` --- Handle repeated adjacent lines

Example file:

``` text
apple
apple
banana
banana
orange
```

Run:

``` bash
uniq fruits.txt
```

Output:

``` text
apple
banana
orange
```

Count adjacent repeated lines:

``` bash
uniq -c fruits.txt
```

Important: `uniq` normally compares adjacent lines. If identical entries
are separated, sort them first:

``` bash
sort fruits.txt | uniq -c
```

This is why `sort` is often used before `uniq`.

### D. `cut` --- Extract fields from lines

`cut` extracts selected sections from each line.

Example file:

``` text
Rahim:Developer:Dhaka
Karim:Designer:Rajshahi
Nila:Student:Khulna
```

Display the first field:

``` bash
cut -d ':' -f 1 people.txt
```

Output:

``` text
Rahim
Karim
Nila
```

Meaning:

  Part       Meaning
  ---------- --------------------------
  `-d ':'`   Use `:` as the delimiter
  `-f 1`     Select field number 1

Display the second field:

``` bash
cut -d ':' -f 2 people.txt
```

For space-separated data, an example is:

``` bash
cut -d ' ' -f 1 otithi-khata.txt
```

This selects the first field separated by a literal space. For more
complicated or irregular whitespace, other tools such as `awk` may be
more suitable.

## 5. Input Redirection: `<` --- Send a File as Input

The `<` operator redirects a file to a command's standard input.

### Syntax

``` bash
command < filename
```

Example:

``` bash
wc -l < otithi-khata.txt
```

The content of `otithi-khata.txt` is supplied to `wc` through standard
input.

Compare:

``` bash
wc -l otithi-khata.txt
```

with:

``` bash
wc -l < otithi-khata.txt
```

Both count the lines, but the first command receives a filename argument
while the second receives redirected standard input.

### Redirection symbols at a glance

  -----------------------------------------------------------------------
  Symbol                  Name                    Purpose
  ----------------------- ----------------------- -----------------------
  `>`                     Output redirection      Send standard output to
                                                  a file; overwrite it

  `>>`                    Append redirection      Add standard output to
                                                  the end of a file

  `<`                     Input redirection       Read standard input
                                                  from a file

  `|`                     Pipe                    Send one command's
                                                  standard output to
                                                  another command
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## Mini Project: Analyse a Visitor Log

### Scenario

Imagine that you manage a website. Your server records visitor IP
addresses and the pages they request.

You want to find which IP address made the most requests.

This is a simplified example of a task that can be useful when analysing
server logs.

### Step 1 --- Create a sample log file

Move to your home directory:

``` bash
cd ~
```

Create the file:

``` bash
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

The text between the two `EOF` markers is written into the file. The
quoted marker prevents shell expansion of special characters inside the
supplied text.

Verify the file:

``` bash
cat otithi-khata.txt
```

### Step 2 --- Extract only the IP addresses

``` bash
cut -d ' ' -f 1 otithi-khata.txt
```

Explanation:

-   `-d ' '` uses a space as the delimiter.
-   `-f 1` selects the first field.
-   The first field in each log line is the visitor IP address.

Expected output:

``` text
10.0.0.5
10.0.0.9
10.0.0.5
10.0.0.7
10.0.0.5
10.0.0.9
10.0.0.5
10.0.0.7
10.0.0.5
10.0.0.9
```

### Step 3 --- Sort the IP addresses

``` bash
cut -d ' ' -f 1 otithi-khata.txt | sort
```

Now identical IP addresses appear next to one another.

### Step 4 --- Count repeated IP addresses

``` bash
cut -d ' ' -f 1 otithi-khata.txt | sort | uniq -c
```

Expected output:

``` text
      5 10.0.0.5
      2 10.0.0.7
      3 10.0.0.9
```

Why did we use `sort` before `uniq -c`?

Because `uniq` counts adjacent repeated lines. Sorting brings identical
IP addresses together first.

### Step 5 --- Sort by request count

``` bash
cut -d ' ' -f 1 otithi-khata.txt | sort | uniq -c | sort -rn
```

Expected output:

``` text
      5 10.0.0.5
      3 10.0.0.9
      2 10.0.0.7
```

Explanation:

-   `-n` sorts numerically.
-   `-r` reverses the order.
-   Together, `-rn` places the largest count first.

### Step 6 --- Display only the most frequent IP

``` bash
cut -d ' ' -f 1 otithi-khata.txt | sort | uniq -c | sort -rn | head -n 1
```

Expected output:

``` text
      5 10.0.0.5
```

### What did we accomplish?

We combined five small commands:

``` text
cut  →  sort  →  uniq -c  →  sort -rn  →  head -n 1
```

Each command performs one specific task:

  Command       Job
  ------------- ---------------------------------------
  `cut`         Extract the IP address
  `sort`        Group identical IP addresses together
  `uniq -c`     Count each adjacent group
  `sort -rn`    Put the highest count first
  `head -n 1`   Display the top result

This is a practical example of the Unix philosophy: use small tools that
do one job well, then connect them to solve a larger problem.

> **Important:** This sample log is for learning. Real security
> investigations require more context; a high request count alone does
> not prove malicious activity.

## Chapter 9 Practice

1.  Save your command history to a file:

    ``` bash
    history > amar-itihas.txt
    ```

2.  Count the commands in your history:

    ``` bash
    history | wc -l
    ```

3.  Find commands in your history that contain `apt`:

    ``` bash
    history | grep apt
    ```

4.  Count how many lines in the diary contain the word `Linu`:

    ``` bash
    grep -i "linu" linu-diary.txt | wc -l
    ```

5.  Find the most frequently requested page in `otithi-khata.txt`. Hint:
    extract the third field instead of the first.

6.  Run:

    ``` bash
    ls /usr/bin | grep "^z"
    ```

    Observe the output. The `^` character in this pattern means the
    beginning of a line.

7.  Create a file using `>` and then add another line using `>>`. Verify
    the difference with `cat`.

8.  Compare the outputs of:

    ``` bash
    wc -l otithi-khata.txt
    wc -l < otithi-khata.txt
    ```

------------------------------------------------------------------------

# Common Mistakes

  ------------------------------------------------------------------------
  Mistake                 Why it is a problem     Better approach
  ----------------------- ----------------------- ------------------------
  Running `apt upgrade`   Package information may Run `sudo apt update`
  without refreshing      be outdated             first
  package information                             

  Using `sudo` for every  Unnecessary             Use `sudo` only when
  command                 administrator access    needed
                          increases risk          

  Using `>` when you      Existing file content   Use `>>` to append
  meant to append         is overwritten          

  Expecting `uniq` to     `uniq` normally checks  Use
  count all repeated      adjacent lines          `sort file \| uniq -c`
  lines automatically                             

  Forgetting to quit      The terminal remains    Press `q`
  `less`                  inside the viewer       

  Getting stuck in Vim    Vim has different modes Press `Esc`, then use
                                                  `:q!` or `:wq`

  Forgetting to stop      It keeps monitoring the Press `Ctrl + C`
  `tail -f`               file                    

  Assuming `<` and `>` do One redirects input;    Remember the direction
  the same job            the other redirects     of data flow
                          output                  
  ------------------------------------------------------------------------

# Final Revision Checklist

Use this checklist to test your understanding.

## Chapter 7 --- Package Management

-   [ ] I understand what a package manager does.
-   [ ] I can explain the difference between `apt update` and
    `apt upgrade`.
-   [ ] I can install and search for packages.
-   [ ] I understand `remove`, `purge`, and `autoremove`.
-   [ ] I know why software should come from trusted sources.

## Chapter 8 --- Reading and Writing Files

-   [ ] I can display a file with `cat`.
-   [ ] I can read a long file with `less`.
-   [ ] I can display selected lines with `head` and `tail`.
-   [ ] I understand how `tail -f` monitors new lines.
-   [ ] I can edit and save a file using Nano.
-   [ ] I know the basic Vim commands needed to edit, save, and exit.

## Chapter 9 --- Pipes and Redirection

-   [ ] I understand `stdin`, `stdout`, and `stderr`.
-   [ ] I know the difference between `>`, `>>`, `<`, and `|`.
-   [ ] I can use `wc`, `sort`, `uniq`, and `cut`.
-   [ ] I understand why `sort` is often used before `uniq`.
-   [ ] I can connect multiple commands in a pipeline.
-   [ ] I can analyse the sample visitor log.

------------------------------------------------------------------------

# Further Learning

Official documentation and useful references:

-   [Ubuntu Documentation](https://documentation.ubuntu.com/)
-   [Debian APT User's
    Guide](https://www.debian.org/doc/manuals/apt-guide/)
-   [GNU Coreutils
    Manual](https://www.gnu.org/software/coreutils/manual/)
-   [GNU Bash Reference
    Manual](https://www.gnu.org/software/bash/manual/)
-   [Nano Editor](https://www.nano-editor.org/)
-   [Vim Documentation](https://www.vim.org/docs.php)

## Notes for macOS Users

The file-reading, text-processing, and shell-redirection commands in
these notes are also useful on macOS because macOS includes a Unix-based
command-line environment.

However:

-   `apt` is for Debian/Ubuntu-based Linux, not macOS.
-   macOS users commonly install command-line software with
    [Homebrew](https://brew.sh/).
-   Some command options differ between GNU/Linux and the BSD tools
    included with macOS.
-   A command that works on Ubuntu may need a small adjustment on macOS.

## Final Thought

Linux becomes easier when you stop memorising commands as isolated
instructions and start understanding how data moves through the
terminal.

A single command can do a small job. A well-designed pipeline can turn
those small jobs into a powerful workflow.

**Keep practising, experiment carefully, and always understand a command
before running it.**
