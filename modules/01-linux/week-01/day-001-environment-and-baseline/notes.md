# Day 001 notes

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

An absolute path starts with `/`, such as `/home/learner/veriqta-devops-labs/day-001`. A relative path is interpreted from your current directory, such as `baseline.md`. The special path `.` means the current directory.

`$HOME` expands to your home directory in Bash. Do not set it to a course folder. Double quotes in `"$HOME/veriqta-devops-labs/day-001"` keep the expanded path together if it contains spaces. The quote characters are not part of the directory name.

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

[Guided lab](lab.md) · [Lesson overview](README.md) · [Official references](../../../../docs/references.md)
