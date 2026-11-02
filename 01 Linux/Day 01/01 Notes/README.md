# Linux, Day 01 notes

## 1. Your lab environment

You need a terminal in an authorized Linux computer, Linux VM, WSL Linux distribution, or suitable training environment. Use a regular user account. These notes assume Bash and GNU utilities. The editor is vi. You need no cloud account or paid resource for this lesson.

A terminal is the window where you type and see results. A shell interprets what you type. The kernel manages processes, memory, and devices. A Linux distribution combines a kernel with packages, utilities, and operating-system conventions.

Use the copy button on a command block and paste it into your Linux terminal. Run one block at a time. Do not copy the expected-output blocks as commands. Sample output shows a pattern; your username, version, paths, time, and sizes can differ.

If you do not have a Linux environment, arrange it before continuing. PowerShell and macOS Terminal are not substitutes for the Linux lab described here. If a required tool is missing, record your distribution and exact error rather than running an unrelated installation script.

### Confirm the visible kernel

Copy and run:

```bash
uname -s
```

Expected output in this lab:

```text
Linux
```

The program asks for system information, and the option selects the kernel name. This is a read-only check. If your result differs, confirm that you opened the intended Linux terminal.

### Confirm your account privileges

Copy and run:

```bash
id -u
```

Example output:

```text
1000
```

This prints your effective numeric user ID. Other nonzero values are normal. Zero means root in the current context. If the result is zero, stop and use an existing authorized regular lab account. Do not create accounts or alter a shared system to bypass the check.

A terminal prompt can be customized. Its final symbol does not reliably establish your privileges.

### Identify the account name

Copy and run:

```bash
id -un
```

Example output:

```text
learner
```

The options select the effective user identity and request its name. This is your Linux account name, not necessarily your email or display name. Keep the actual value private when sharing evidence.

### Confirm Bash is available

Copy and run:

```bash
bash --version
```

The first line should identify GNU Bash and its installed version. Additional license information can follow. Record your actual version rather than copying a version from an example. This check does not prove which shell you are currently using.

To work in Bash, copy and run:

```bash
bash
```

Expected result: a new Bash prompt, which may look identical to the previous one. You have started a child shell. The final section explains how to leave that child shell when you are finished.

## 2. Inspect before you change

Imagine entering a restaurant kitchen. Before replacing equipment, you check which kitchen you are in, which workbench is yours, and what equipment is present. A correct instruction applied in the wrong place can still cause a problem.

Your distribution is part of the environment. Your identity affects permissions. Your working directory determines where relative filenames point. Your baseline records the observations before later changes.

The analogy has limits. A container can share its host's kernel while presenting different filesystem contents. No single check establishes every layer of the environment.

![Separate checks for kernel, distribution, identity, and workspace.](../07%20Images/environment-map.svg)

Text equivalent: your terminal displays input and output, Bash interprets commands, and individual utilities inspect separate facts. Check these facts independently before drawing conclusions.

## 3. Identify your distribution

Copy and run:

```bash
cat /etc/os-release
```

The utility reads the file named after it. This file contains distribution identity information. Look for these fields:

```text
PRETTY_NAME="Example Linux 1"
ID=example
VERSION_ID="1"
```

These values are fictional examples of the format. Read the actual values on your machine. The first field is a readable distribution name. The other two identify the distribution and its release; some systems omit the release field.

The earlier kernel check and this file answer different questions. A Linux kernel name alone does not prove you are using Ubuntu or tell you which package instructions to choose.

If the file is absent, record that fact and use the lesson's troubleshooting section. Do not guess the distribution.

## 4. Identify machine architecture

Copy and run:

```bash
uname -m
```

One example result is:

```text
x86_64
```

Another possible result is:

```text
aarch64
```

The option asks for the machine architecture label. Record only your actual result. Software built for one architecture does not automatically work on another. The label alone does not establish all compatibility requirements.

## 5. Understand your location and paths

An absolute Linux path starts with a slash. A relative path is interpreted from your current directory. The dot means the current directory. The home-directory variable is already provided by the shell; do not reassign it.

Copy and run:

```bash
pwd
```

Example output:

```text
/home/learner
```

This prints the working directory. Your path can differ. Reading a filename without a full path asks the shell's launched program to look relative to this directory.

### Create a safe notes workspace

Copy and run:

```bash
mkdir -p "$HOME/veriqta-devops-labs/linux/day-01/notes-practice"
```

Expected result: no output on success. This creates the directory and any missing parents. The option accepts existing directories and does not erase their contents. The quotes preserve the expanded path as a single argument, including spaces.

This notes-practice directory keeps your practice file separate from the guided lab's baseline. Never respond to a wrong path by adding administrator privileges.

### Enter the directory

Copy and run:

```bash
cd "$HOME/veriqta-devops-labs/linux/day-01/notes-practice"
```

Expected result: normally no output. This changes the current shell's working directory. If it reports an error, resolve it before proceeding.

Verify the new location with this separate command:

```bash
pwd
```

Expected pattern:

```text
/home/learner/veriqta-devops-labs/linux/day-01/notes-practice
```

Your actual home prefix may differ. The path must end with the intended notes-practice directory. Silence from a directory-changing command is not a substitute for checking its result.

## 6. Inspect available filesystem space

While you are in notes-practice, copy and run:

```bash
df -h .
```

Example output pattern:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/example     40G   12G   26G  32% /
```

The filesystem identifier and numbers above are illustrative. The readable-size option changes the displayed units. The final dot selects the filesystem containing your current directory.

Read the available-space column and its unit. This is not a report of every disk, a complete inode or quota check, or proof that future application storage needs will be met. Do not use one space figure as a complete health diagnosis.

## 7. Record the observation time

Copy and run:

```bash
date -Iseconds
```

Example output format:

```text
2026-11-02T15:00:00+01:00
```

This asks GNU date for an ISO-style timestamp including seconds and a timezone offset. Use your actual result. The offset helps you compare observations from different locations. A baseline needs a capture time because system state can change.

## 8. Create and save a small file in vi

An editor lets you create or change file contents. vi has modes. Normal mode interprets keys as editor actions; insert mode accepts typed text.

Open a practice file:

```bash
vi practice.txt
```

Expected result: the editor opens. A new file can show empty lines and a filename indicator. If the file already exists, inspect it first and preserve useful earlier work.

These next actions happen **inside vi**, not at the shell prompt:

1. Press the i key to enter insert mode.
2. Type this line into a new practice file:

```text
Linux environment practice.
```

3. Press Esc to return to normal mode.
4. Enter the following editor command and press Enter:

```text
:wq
```

Expected result: vi saves the file and returns to the shell. The letters request writing and quitting. If an error appears, the save has not succeeded; do not assume your text is safely on disk.

To abandon unsaved edits deliberately, press Esc, then use this **editor command** and press Enter:

```text
:q!
```

This discards unsaved changes. Do not use it when you need to keep those edits. Do not paste either editor command into a Bash prompt.

## 9. Verify the file and its contents

First, copy and run:

```bash
ls -l practice.txt
```

Example output pattern:

```text
-rw-r--r-- 1 learner learner 28 Nov 2 15:00 practice.txt
```

Your permissions, account names, timestamp, and byte count can differ. The long listing shows metadata, including the filename and size. A nonzero size indicates the file has contents; it does not prove they are the right contents.

Read the actual saved content:

```bash
cat practice.txt
```

Expected output for the new file created above:

```text
Linux environment practice.
```

If this differs, reopen the file using the editor step, inspect what was saved, and correct the intended text. Then save and read it again.

### Check that location matters

Return to your home directory:

```bash
cd "$HOME"
```

Expected result: normally no output. You have changed directories; you have not deleted the practice file.

Return to your notes workspace:

```bash
cd "$HOME/veriqta-devops-labs/linux/day-01/notes-practice"
```

Expected result: normally no output. Now read the file again:

```bash
cat practice.txt
```

Expected output:

```text
Linux environment practice.
```

The saved file belongs to the filesystem, not the terminal's display history. Closing a terminal does not ordinarily erase the file. Deleting a disposable container or other temporary environment can erase its local filesystem, so do not confuse terminal persistence with a backup.

## 10. Finish the notes practice

Keep the practice file. This exercise created no service or cloud resource. If you started the extra Bash shell earlier and want to return to its parent, copy and run once:

```bash
exit
```

Expected result: the child Bash session ends and you return to its parent prompt. Running it at the outermost shell can close the terminal session, so do not repeat it blindly.

Your guided lab will create the actual Day 01 baseline in the main Day 01 workspace. The projects will turn that baseline into documented portfolio work.

## What you can now explain

- How the terminal, shell, kernel, and distribution differ.
- Why numeric identity is stronger evidence than a prompt's appearance.
- Why distribution and architecture need separate checks.
- How a working directory affects relative filenames.
- Why saving, listing, reading, and reopening are separate checks.
- Why a baseline needs an observation time and clear limitations.

## Official references

- [Bash manual](https://www.gnu.org/software/bash/manual/bash.html), shell behavior and quoting.
- [GNU Coreutils](https://www.gnu.org/software/coreutils/manual/coreutils.html), the system, file, and date utilities used here.
- [Distribution identity fields](https://www.freedesktop.org/software/systemd/man/latest/os-release.html).
- [Vim basic editing](https://vimhelp.org/usr_02.txt.html), when vi is provided by Vim.

[Continue to the lab](../02%20Follow%20Along%20Lab/README.md) · [Day 01](../README.md)
