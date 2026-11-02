# Day 01 follow-along lab

Outcome: create a private, evidence-based environment baseline and reopen it successfully.

Run commands one at a time. In live instruction, stop after each requested checkpoint and wait for feedback. Independently, compare your result with the stated expectation before proceeding. All sample output below is illustrative, not a transcript from your machine.

## Step 1, confirm Linux before changing anything

Open your Linux terminal. Run:

```sh
uname -s
```

`uname` asks for system information; `-s` selects the kernel name. Expected result: `Linux`. If you see `Darwin`, an unrecognized-command error, or another result, pause and use the [environment guide](../01%20Notes/README.md#your-lab-environment). Do not install or change system configuration.

This confirms the visible kernel family only. It does not tell you whether the shell runs in a VM, WSL, a container, or a full host.

## Step 2, check your identity and shell

```sh
id -u
```

This prints your effective numeric user ID. A regular lab account often has an ID such as `1000`, but other nonzero values are normal. If the result is `0`, pause and switch to an existing regular lab account before continuing. Do not change accounts or permissions on a shared machine without authorization.

Next, identify the account name:

```sh
id -un
```

Record the actual name privately. Do not assume it is the same as your display name or email address.

Check that Bash is available:

```sh
bash --version
```

You should see a Bash version banner. This confirms availability, not your current shell. To ensure the remaining commands use Bash, start it:

```sh
bash
```

Your prompt might look unchanged. You have started a shell inside the previous shell. You can return to the previous shell with `exit` when finished. If Bash is unavailable, stop and record the exact error.

## Step 3, identify the distribution and architecture

```sh
cat /etc/os-release
```

`cat` reads the named file. Look for `PRETTY_NAME` and `ID`; record `VERSION_ID` if present. Example pattern:

```text
PRETTY_NAME="Example Linux 1"
ID=example
VERSION_ID="1"
```

These example values are deliberately fictional. Record your actual values. If the file is missing, do not invent a distribution. Use [troubleshooting](../06%20Troubleshooting/README.md).

```sh
uname -m
```

Examples include `x86_64` or `aarch64`. The result matters when choosing compatible software later. It does not identify your distribution.

## Step 4, create and verify your private workspace

First, inspect your current location:

```sh
pwd
```

An absolute Linux path begins with `/`. Your initial location can differ from another learner's.

Create the workspace:

```sh
mkdir -p "$HOME/veriqta-devops-labs/day-01"
```

`-p` creates any missing parent directories. Bash expands `$HOME`; the quotes keep the path together. The command creates directories under your own home and does not erase existing contents. Success normally prints nothing. Silence by itself is not your final verification.

Move into it:

```sh
cd "$HOME/veriqta-devops-labs/day-01"
```

Verify the location:

```sh
pwd
```

Expected pattern: your actual home directory followed by `/veriqta-devops-labs/day-01`. If it differs, stop before writing the file and resolve the path.

Inspect space for this workspace:

```sh
df -h .
```

Read the `Avail` and `Mounted on` columns. Your filesystem name and sizes can differ. You are inspecting one filesystem, not measuring the application's future storage needs.

Record the current timestamp:

```sh
date -Iseconds
```

Example pattern: `2026-11-02T14:20:00+01:00`. Use your actual timestamp. The offset tells you how the displayed time relates to UTC.

## Step 5, write your first baseline in vi

Open the baseline file:

```sh
vi baseline.md
```

If a previous baseline already exists, inspect it first. Preserve its observations. To make a separate attempt, leave the editor without changes using `Esc`, then `:q!`, then Enter, and open a new filename such as `baseline-retry-01.md`. Replace the filename consistently in later verification commands. Never overwrite evidence just to make a rerun look new.

For a new file, press `i` to enter insert mode. Enter the complete small document below, replacing every bracketed placeholder with your observed values or a truthful limitation:

```markdown
# Day 01 Environment Baseline

Captured at: [actual timestamp including timezone offset]
Kernel name: [uname -s result]
Distribution: [PRETTY_NAME and ID, plus VERSION_ID if present]
Architecture: [uname -m result]
Current user: [id -un result, keep private]
Numeric user ID: [id -u result]
Bash version: [version from the banner]
Workspace: [pwd result after entering day-01]
Available space for this workspace: [Avail value from df -h .]

Observation: [one fact you confirmed]
Limitation: [one thing these checks do not prove]
Next action: Verify this file, then complete the Day 01 assessment.
```

This is a text document, not a script. You are writing a record of observed evidence, so do not paste example answers as your own results.

Press `Esc`, type `:wq`, then press Enter. `w` writes the file and `q` quits. If writing fails, remain in the editor and use the troubleshooting guidance; do not assume the file was saved.

## Step 6, verify the saved artifact

```sh
ls -l baseline.md
```

You should see a listing for a regular file with a nonzero size. Ownership and permissions will be explored later. A listing alone does not prove the contents are correct.

```sh
cat baseline.md
```

Read it. Are all placeholders replaced? Do the values agree with what you observed? Does the limitation avoid claiming more than the evidence proves? If not, reopen the file in vi, correct it, save, and read it again.

## Step 7, prove you can resume

Leave the workspace:

```sh
cd "$HOME"
```

Return:

```sh
cd "$HOME/veriqta-devops-labs/day-01"
```

Read the saved file again:

```sh
cat baseline.md
```

Your content should still be present. The file lives in the filesystem, not in the terminal's display history. A local saved file can survive closing a terminal, but disposable containers or cloud labs can still lose their files when the environment itself is deleted.

![Teaching diagram showing inspect, record, reopen, and explain as separate verification checkpoints.](../07%20Images/baseline-checkpoints.svg)

Text equivalent: inspection produces observations, recording saves those observations, reopening checks persistence, and explanation checks that your conclusions match the evidence. None of these steps alone proves that an application is healthy.

## Finish, cleanup, and resumption

Keep your baseline for later lessons. There are no cloud resources or background services to remove. No deletion command is needed. Use `exit` once to leave the extra Bash shell you started, if you want to return to its parent.

If you stop early, record the last verified step and error privately. On return, repeat the identity check and navigate back to the same workspace before continuing. Do not regenerate earlier evidence without noting the new observation time.

For a 30-minute session, finish through Step 4 and record that checkpoint. Resume at Step 5 next time. Do not mark the day complete until you have verified the saved artifact and completed the assessment.

Continue with the [project connection](../03%20Portfolio%20Projects/README.md), [knowledge checks](../04%20Knowledge%20Checks/README.md), and [assessment](../05%20Practical%20Assessment/README.md).

[Lesson overview](../README.md)
