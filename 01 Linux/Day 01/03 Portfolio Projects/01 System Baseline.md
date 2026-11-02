# Project 01, Build and Publish Your Linux System Baseline

You are preparing a Linux lab for an application. Before choosing software or changing configuration, you need a starting record that another engineer can read and reproduce.

You will build three files, verify them locally, and publish reviewed copies in your own GitHub repository. Follow each step in order. Your result is a documented Linux investigation, not simply a list of tasks to attempt.

## What you need

Complete the Day 01 lab first. Use the same regular Linux account, Bash terminal, and vi editor. You also need a GitHub account and a browser for publication. You do not need Git installed, a cloud account, or a paid resource.

Use your real observations. Text labeled `[replace ...]` is a field to fill with your result. The literal label `[redacted]` is an intentional privacy label and may remain in a public copy.

![The four checkpoints, inspect, record, reopen, and explain.](../07%20Images/baseline-checkpoints.svg)

Text equivalent: collect actual observations, save them, reopen the saved record, and explain the conclusions and limits. The portfolio adds reproducible instructions and a verification record to this process.

## Step 1, find your original lab work

Run:

```sh
id -u
```

The result is your effective numeric user ID. It must be nonzero for this lab. If it is zero, switch to an existing authorized regular lab account before continuing.

Return to the original Day 01 workspace:

```sh
cd "$HOME/veriqta-devops-labs/linux/day-01"
```

`cd` changes the shell's working directory. `$HOME` expands to your home directory, and the quotes keep the path together. If this fails, return to the guided lab and resolve the missing workspace before proceeding.

Read your existing baseline:

```sh
cat baseline.md
```

`cat` prints the saved file. You should see the record you created in the lab. You will preserve this private original and build a separate portfolio report. You are not overwriting your first observations.

## Step 2, create a dedicated project directory

```sh
mkdir -p "$HOME/veriqta-devops-labs/linux/day-01/portfolio/system-baseline"
```

`mkdir` creates directories. `-p` creates missing parents and accepts existing directories. This command does not erase existing files. If you are repeating the project, inspect existing work before editing it and preserve an earlier attempt when useful.

```sh
cd "$HOME/veriqta-devops-labs/linux/day-01/portfolio/system-baseline"
```

Check the location:

```sh
pwd
```

The path should end in `/linux/day-01/portfolio/system-baseline`. Do not create the project files until this is correct.

## Step 3, collect the observations for your report

Run each command separately. Read its result before moving on. You may refer to your original baseline, but this project report must say when its own observations were taken.

| Command | What you learn | What to record |
| --- | --- | --- |
| `date -Iseconds` | The current timestamp with an offset from UTC. | Your observation time, such as the format `2026-11-02T15:00:00+01:00`, using your actual result. |
| `uname -s` | The visible kernel name. | The actual kernel name, expected to be Linux. |
| `cat /etc/os-release` | The distribution's identifying fields. | PRETTY_NAME and ID, plus VERSION_ID when present. |
| `uname -m` | The machine architecture label. | Your actual architecture, for example x86_64 or aarch64. |
| `bash --version` | The installed Bash version. | The version from the first line, rather than the entire banner. |
| `id -u` | Your effective numeric user ID. | Privately confirm that it is nonzero; the public report can state that fact without your exact ID. |
| `pwd` | Your working directory. | Confirm the project path; use the portable `$HOME` form in public instructions. |
| `df -h .` | Space information for the filesystem containing this directory. | The actual Avail value with its unit and the observation time. |

The dot in `df -h .` selects the current directory's filesystem. `-h` asks for readable units. The result does not describe all disks or prove the application has enough capacity.

Keep account names, real home paths, and unnecessary filesystem identifiers private. Do not upload your complete terminal history. Your public report can retain useful distribution and architecture facts while omitting private identity details.

## Step 4, write your portfolio baseline

Open a new file in the project directory:

```sh
vi baseline.md
```

For a new file, press `i` to type. Enter the whole document below. Replace the `[replace ...]` fields with the observations you just collected. Keep the privacy labels where shown.

```markdown
# Linux System Baseline

## Scope

A personal Linux training environment inspected before application installation.

## Observations

| Item | Observed result |
| --- | --- |
| Captured at, including timezone offset | [replace with observation timestamp] |
| Kernel name | [replace with uname -s result] |
| Distribution PRETTY_NAME | [replace with PRETTY_NAME] |
| Distribution ID | [replace with ID] |
| Distribution VERSION_ID | [replace with VERSION_ID, or not provided] |
| Architecture | [replace with uname -m result] |
| Bash version | [replace with Bash version] |
| User context | Regular account, nonzero effective user ID verified |
| Account name | [redacted] |
| Portable workspace | $HOME/veriqta-devops-labs/linux/day-01/portfolio/system-baseline |
| Available space for this workspace | [replace with Avail value and unit] |

## Interpretation

The distribution helps me choose suitable package instructions. The architecture
helps me choose compatible software builds. The current path confirms where
project files are being created.

## Limits

This report does not establish application health, security hardening, future
storage needs, or the complete host and virtualization architecture. Available
space can change after the observation time.

## Evidence handling

This is a reviewed public report. Private account names and real home paths are
not included. Recorded technical results come from my actual observations.
```

Press `Esc`, type `:wq`, and press Enter. `w` saves and `q` exits after saving succeeds. If the file already exists, read it before editing rather than pasting a second document over it.

Verify the saved contents:

```sh
cat baseline.md
```

Check that the report matches your output. Every `[replace ...]` field must be resolved. Do not replace a failed check with a successful example. If your account check failed, stop and resolve it before claiming a regular-user context.

## Step 5, write the project README

A README is the introduction GitHub displays when a visitor opens a directory. Your README should explain the work, point to the evidence, and give reproduction instructions.

```sh
vi README.md
```

For a new file, press `i` and enter:

````markdown
# Linux System Baseline

## Overview

I inspected a personal Linux lab and recorded an environment baseline before
application installation. This project demonstrates environment inspection,
file verification, and evidence-based technical reporting.

## Files

- [Environment report](baseline.md).
- [Verification record](verification.md).

## Reproduce the inspection

Use your own authorized Linux environment and a regular user account. Run each
command separately and interpret your own results.

```sh
uname -s
```

Check the visible kernel name.

```sh
cat /etc/os-release
```

Read the distribution fields.

```sh
uname -m
```

Record the architecture.

```sh
bash --version
```

Read the installed Bash version.

```sh
id -u
```

Confirm that your effective numeric user ID is nonzero.

```sh
pwd
```

Confirm which directory you are inspecting.

```sh
df -h .
```

Read available space on that directory's filesystem.

```sh
date -Iseconds
```

Record when you inspected the environment. These read-only commands do not
install software or deploy an application.

## Result

[replace with two sentences describing your actual result and what you verified]

## Lessons learned

[replace with one concrete distinction you learned, such as kernel versus distribution]

## Limitations

The report is a point-in-time observation. Different environments can produce
different values. It does not establish application health or production readiness.
````

The outer four-backtick fence belongs to this tutorial's formatting. Copy the document inside it, including its internal three-backtick command fences, not the outer fence itself. Replace both reflection fields with your own result, save with `Esc`, `:wq`, Enter, and read `README.md` with `cat`.

## Step 6, verify the files and record the checks

List the files:

```sh
ls -l
```

`ls` lists directory contents; `-l` includes file metadata. You should see `README.md` and `baseline.md`, both with nonzero sizes. Read each file with `cat` to verify its content, not just its presence.

Leave the project directory:

```sh
cd "$HOME"
```

Return:

```sh
cd "$HOME/veriqta-devops-labs/linux/day-01/portfolio/system-baseline"
```

Read the report again:

```sh
cat baseline.md
```

Your saved observations should remain present. Run `uname -m` and `cat /etc/os-release` again and compare them with the report. For disk space, compare meaning and units rather than expecting the number to stay unchanged forever.

Create your verification record:

```sh
vi verification.md
```

Enter and fill this record only after performing the corresponding checks:

```markdown
# System Baseline Verification

Checked at: [replace with actual check time and timezone offset]

| Check | Actual result |
| --- | --- |
| Regular-user identity checked | [replace with your observed outcome] |
| Project directory verified with pwd | [replace with your observed outcome, using a portable path] |
| README and baseline saved and read from the shell | [replace with actual outcome] |
| Left the directory, returned, and read the baseline | [replace with actual outcome] |
| Distribution and architecture compared with the report | [replace with actual outcome] |
| Private identifiers removed from the public copy | [replace with what you reviewed] |
| All replacement fields resolved | [replace with actual review result] |

## Issue and resolution

[replace with an actual issue and your verified resolution, or state that no issue occurred]
```

Save it, then run `cat verification.md`. A verification record reports what happened; writing the word passed does not make a failed check pass.

## Step 7, create your GitHub portfolio repository

A repository stores files and their change history. A commit saves a named revision. You will use the browser for this first publication.

Sign in to GitHub. Open [New repository](https://github.com/new), choose your personal account, and name it `linux-foundations-portfolio`. Add a short description, select Public for reviewed portfolio work, enable a README, and create the repository. If that name already holds your work, open it instead. If it belongs to another purpose, choose a different name. Organization permissions may differ.

The browser URL should identify your own account and repository. Do not add your personal results to VERIQTA's shared course repository.

## Step 8, publish the three project files

From your repository's top level, select Add file, then Create new file. Enter `system-baseline/baseline.md` as the filename; the slash creates the subdirectory. Paste your reviewed local file contents into the editor. Select Preview and inspect the rendered report. Select Commit changes, enter a message such as `Add verified Linux baseline`, choose the current default branch for your personal training repository, and confirm Commit changes. A branch is a line of repository history; the default branch is usually named main.

Repeat from the repository's top level for `system-baseline/README.md` and `system-baseline/verification.md`, using each corresponding local file's actual contents. Use the same branch. If repository rules prevent a direct commit, follow the account's required review workflow rather than treating the proposed change as published. GitHub's [pull request guide](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) explains that separate workflow.

Only copy files you reviewed. You do not need to upload your entire workspace, private original baseline, terminal history, or credentials.

## Step 9, introduce your portfolio

At your personal repository's top level, open its README and use the pencil icon to edit it. Replace the initial placeholder introduction with:

```markdown
# Linux Foundations Portfolio

Practical Linux projects with reproducible instructions and verified results.

## Projects

- [Linux System Baseline](system-baseline/README.md), environment inspection,
  a reviewed report, and a file-verification record.

## Working approach

I use an authorized Linux lab, record actual results, and keep private account
details out of public evidence.
```

Preview and commit the change. This edits your portfolio README, not the course README.

## Step 10, verify the published project

Open your repository's top-level README and follow the System Baseline link. From its README, open the environment report and verification record. Confirm that every link works, Markdown tables render, code blocks are readable, and the content matches your reviewed local files.

For a public repository, open the project URL in a signed-out browser window and confirm that a visitor can read it. Record the actual repository URL in your private learning notes. Do not claim publication until you have inspected the published files.

## If something goes wrong

| Symptom | Inspect and fix | Verify |
| --- | --- | --- |
| Local directory is missing | Check the original lab path and the mkdir step. Avoid using sudo to work around a wrong path. | pwd shows the project directory. |
| vi opens an existing file | Read the existing contents first. Edit deliberately or preserve the attempt under another name. | cat shows one coherent saved document. |
| A public link returns an error | Check capitalization and folder placement. The three project files belong inside system-baseline, not all at repository root. | Follow the links from the root README. |
| A table or code fence renders badly | Compare the raw Markdown with the supplied file content. Check fence pairs and table separators. | Preview and reopen the rendered file. |
| Private information is visible | Restrict access if needed and arrange removal from history. Revoke exposed credentials immediately if any were included. | Review the repository and relevant history, not just the latest text. |

## Project completion

You have finished when your three local project files are accurate and verified, your GitHub project opens through working links, and you can explain the meaning and limits of the recorded observations.

Keep the local files; Project 02 uses them. No cloud resource or background service was created, so there is nothing billable to tear down.

## References

- [GitHub, creating a repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository).
- [GitHub, creating files and subdirectories](https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files).
- [GitHub, editing files](https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files).
- [Day 01 command explanations](../01%20Notes/README.md).

[Continue to Project 02](02%20Environment%20Handover.md) · [Projects](README.md)
