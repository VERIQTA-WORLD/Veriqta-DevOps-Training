# Linux, Day 01 notes

## Your lab environment

Open a terminal in a personal Linux computer, disposable Linux VM, or authorized Linux training environment. Use a regular account. If `id -u` returns `0`, stop and use an existing authorized regular lab account. Do not create users or change permissions on a shared computer to bypass the checkpoint.

You need Bash, vi, `/etc/os-release`, and common utilities including uname, id, pwd, cat, mkdir, ls, df, and date. No cloud account, package installation, Git installation, or paid resource is required today.

| Your environment | What to check |
| --- | --- |
| Linux computer or VM | Use its Linux terminal and a regular account. |
| WSL Linux distribution | Open the Linux distribution's terminal and use its Linux home directory. Later service and network labs need separate compatibility checks. |
| Disposable container | The visible kernel and filesystem may belong to different layers; many containers default to root. A container does not replace every full-host lab. |
| Remote Linux machine | Confirm permission and keep system details private. |
| PowerShell or macOS Terminal | Arrange a Linux lab first. Do not assume Linux-specific instructions work unchanged here. |

If you have no Linux environment or a required tool is unavailable, stop and record your operating system and exact error. Request an environment-specific setup step. Do not run an unreviewed remote installation script.

Keep your practice under `$HOME/veriqta-devops-labs/day-01/`, outside any repository checkout. `$HOME` already identifies your home directory; do not reassign it. Keep raw screenshots and system details private. You can study this lesson on GitHub without cloning the repository.

## Inspect before you change

Imagine entering a restaurant kitchen to prepare a meal. You first check which kitchen you are in, what equipment you have, and which workbench is yours. A useful instruction applied in the wrong kitchen can still create a problem.

Your Linux distribution is part of the operating environment. Your identity affects permissions. Your working directory determines where relative paths point. Your practice folder is your workbench. The baseline records what you actually found before changes.

The analogy is limited. A container can share its host's kernel while showing different filesystem contents. A single command does not identify every layer.

![Teaching diagram of the separate environment checks.](../07%20Images/environment-map.svg)

Text equivalent: your terminal shows commands and output, Bash interprets commands, and utilities inspect separate facts about the kernel, distribution, identity, and working directory. Record these facts in your own private baseline.


## Terminal, shell, and operating system

Your terminal is the interface where you enter text and see output. Bash is a shell: it interprets commands, expands variables, and launches programs. The Linux kernel manages resources such as processes and devices. A distribution combines a kernel with tools, packages, and operating-system conventions.

A prompt is the text displayed before your command. Your prompt might end in `$`, `#`, or something else. Prompts are customizable, so do not use their appearance as proof of your privileges. The lab uses `id -u` to check.

Copy only commands from code blocks. Do not type the prompt. Case matters: `HOME` and `home` are different variable names, and Linux paths are generally case-sensitive.

## Four different questions

| Question | Evidence | What it does not establish |
| --- | --- | --- |
| What kernel family is visible? | `uname -s` | Your distribution, cloud provider, or complete host architecture. |
| What distribution identifies this userspace? | `/etc/os-release` | That you have a full VM, systemd, or a particular kernel. |
| Which account is running this command? | `id -un` and `id -u` | All permissions on every file or service. |
| Which directory are you working in? | `pwd` | That the directory is safe to modify or belongs to you. |

`uname -m` reports a machine architecture label. Examples include `x86_64` and `aarch64`. Do not assume downloaded software built for one architecture will run on the other.

Read `PRETTY_NAME` in `/etc/os-release` for a human-readable distribution name. Fields such as `ID` and `VERSION_ID` are useful for identifying it precisely. Some distributions do not provide every field.

## Paths and your home directory

An absolute path starts with `/`, such as `/home/learner/veriqta-devops-labs/day-01`. A relative path is interpreted from your current directory, such as `baseline.md`. The special path `.` means the current directory.

`$HOME` expands to your home directory in Bash. Do not set it to a course folder. Double quotes in `"$HOME/veriqta-devops-labs/day-01"` keep the expanded path together if it contains spaces. The quote characters are not part of the directory name.

`mkdir -p` creates missing parent directories and accepts a directory that already exists. It does not erase existing files. `cd` changes the current shell's directory. `pwd` shows the resulting location. Check that location before creating or changing files.

## A baseline records evidence

A baseline is a dated starting record. It helps you explain differences later, but it is not proof that an application is healthy. Record facts and limits separately.

For example, `df -h .` reports the filesystem containing your current directory. Its `Avail` column is an available-space estimate shown in readable units. It does not report all disks, prove that enough capacity exists for future workloads, or check quotas and inodes comprehensively.

Record timestamps with timezone or offset. `date -Iseconds` asks GNU date for an ISO-style timestamp with seconds and an offset. Two learners can see different local times without either clock being wrong.

## vi essentials

vi is a modal editor. In normal mode, keys perform editor actions. In insert mode, keys enter text.

| Action | Keys | Result |
| --- | --- | --- |
| Open a file | `vi baseline.md` at the shell | Opens an existing file or starts a buffer for a new file. |
| Start typing | `i` in normal mode | Enters insert mode. |
| Return to normal mode | `Esc` | Ends text entry. |
| Save and close | `:wq` then Enter | Writes the buffer and quits if writing succeeds. |
| Quit without saving | `:q!` then Enter | Discards unsaved edits. Use only when you intend that loss. |

Opening vi is not the same as saving a file. After leaving the editor, read the file with `cat` and verify that your latest content is present. If an existing baseline opens, inspect it before editing and preserve the original observations.

## Command reference

| Command | Purpose and important argument | Side effect |
| --- | --- | --- |
| `uname -s` | `-s` prints the kernel name. | None. |
| `id -u` | `-u` prints the current effective numeric user ID. Zero means root privileges in this context. | None. |
| `id -un` | `-u` selects the user ID and `-n` requests its name. | None. |
| `bash --version` | Reports the installed Bash version, not necessarily your current shell. | None. |
| `bash` | Starts a Bash shell. Use when you need the lesson's shell behavior. | Creates a shell process; `exit` returns to the parent shell. |
| `cat /etc/os-release` | Prints the distribution information file. | None. |
| `uname -m` | `-m` prints the machine architecture. | None. |
| `pwd` | Prints your working directory. | None. |
| `df -h .` | `-h` uses readable size units; `.` selects the current filesystem. | None. |
| `date -Iseconds` | Reports a timestamp including a timezone offset. | None. |
| `mkdir -p "path"` | Creates a directory and missing parents. `path` is a placeholder here. | Creates directories. |
| `cd "path"` | Moves your shell to the specified directory. `path` is a placeholder. | Changes shell location. |
| `ls -l baseline.md` | Shows the file's listing; `-l` includes metadata. | None. |
| `cat baseline.md` | Reads the saved file. | None. |

## What you are not concluding yet

You have not proved service health, production readiness, security hardening, or spare capacity. You have not established the virtualization type from the kernel name. You have established a useful, inspectable starting point for the next lessons.

[Guided lab](../02%20Follow%20Along%20Lab/README.md) · [Lesson overview](../README.md)

## Official references

Use these to confirm a command's behavior, not as an extra course to finish before the lab. Reference review date: 2 November 2026.

- [Bash manual](https://www.gnu.org/software/bash/manual/bash.html), shell commands, variables, and quoting.
- [GNU uname](https://www.gnu.org/software/coreutils/manual/html_node/uname-invocation.html), kernel and architecture information.
- [GNU id](https://www.gnu.org/software/coreutils/manual/html_node/id-invocation.html), numeric identity and account names.
- [GNU mkdir](https://www.gnu.org/software/coreutils/manual/html_node/mkdir-invocation.html), directory creation.
- [GNU Coreutils](https://www.gnu.org/software/coreutils/manual/coreutils.html), file, date, and disk-reporting utilities.
- [os-release specification](https://www.freedesktop.org/software/systemd/man/latest/os-release.html), distribution identity fields.
- [Vim basic editing](https://vimhelp.org/usr_02.txt.html), modal editing when vi is provided by Vim.

[Continue to the lab](../02%20Follow%20Along%20Lab/README.md) · [Day 01](../README.md)
