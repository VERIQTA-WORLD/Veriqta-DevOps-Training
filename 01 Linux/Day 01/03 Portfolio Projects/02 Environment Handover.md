# Project 02, Build and Test an Environment Handover

You have a saved environment baseline. Now imagine another operator needs to continue your work without asking where the files are or guessing what the report means.

You will write the operator's procedure, follow it yourself, test a harmless wrong-path failure, record recovery, and publish the result beside Project 01. This tutorial supplies the procedure and explains how to adapt and verify it.

## Before you start

Complete [Project 01](01%20System%20Baseline.md). Keep its local `system-baseline` directory and your personal `linux-foundations-portfolio` repository. This project uses both. You do not need a second GitHub repository.

Your handover explains how to navigate a local workspace. A visitor reading your public repository can inspect the report online, but their computer does not automatically contain your local files. The instructions must make that distinction clear.

![A verified baseline becomes an explained and tested handover.](../07%20Images/portfolio-projects.svg)

Text equivalent: Project 01 produces the baseline, Project 02 teaches an operator to locate and interpret it, and verification proves that the instructions and recovery steps work.

## Step 1, verify the source report

In your Linux terminal, check your account:

```sh
id -u
```

Use the same regular account as Project 01. A zero result requires you to stop and use an existing authorized regular lab account.

Navigate to the baseline project:

```sh
cd "$HOME/veriqta-devops-labs/linux/day-01/portfolio/system-baseline"
```

Read the source report:

```sh
cat baseline.md
```

Confirm that it contains your actual distribution, architecture, capture time, and evidence limits. If it is missing, return to Project 01. A handover cannot be verified against a file that does not exist.

## Step 2, create the handover project directory

```sh
mkdir -p "$HOME/veriqta-devops-labs/linux/day-01/portfolio/environment-handover"
```

This creates a sibling directory beside `system-baseline`. The shared parent is `portfolio`. Sibling means neither project is inside the other.

```sh
cd "$HOME/veriqta-devops-labs/linux/day-01/portfolio/environment-handover"
```

Check your position:

```sh
pwd
```

It should end in `/linux/day-01/portfolio/environment-handover`. You are creating new project files here and preserving the source baseline next door.

## Step 3, write the operator handover

Open the file:

```sh
vi handover.md
```

For a new file, press `i` and enter the full guide below. Replace the two `[replace ...]` fields using your actual baseline. Preserve the command blocks as shown.

````markdown
# Linux Lab Environment Handover

## Purpose

Use this guide to find and interpret the Linux environment baseline for a
personal training lab before continuing application work.

## Source record

- Source file: system-baseline/baseline.md.
- Baseline capture time: [replace with the source report's timestamp and offset].
- Recorded environment: [replace with the report's distribution and architecture].
- Local location: $HOME/veriqta-devops-labs/linux/day-01/portfolio/system-baseline/baseline.md.

The source timestamp belongs to the original report. It is not the time when
you read this handover.

## Prerequisites

Use the regular lab account that owns the project files, a Linux terminal, and
the local workspace created in Project 01. If you are reading only the public
GitHub repository, inspect its system-baseline folder online. The public
repository does not automatically create this local workspace for you.

## Operator walkthrough

First, check your effective numeric identity:

```sh
id -u
```

Continue only with the intended regular account and a nonzero ID.

Return to your home directory:

```sh
cd "$HOME"
```

Navigate to the baseline project:

```sh
cd "$HOME/veriqta-devops-labs/linux/day-01/portfolio/system-baseline"
```

Verify where you are:

```sh
pwd
```

The path should end in /linux/day-01/portfolio/system-baseline. Your actual home
prefix can differ from another operator's.

Read the report:

```sh
cat baseline.md
```

Read its capture time, distribution, architecture, and limitations. Do not
assume its disk-space observation is still current.

If you need a fresh space observation, run:

```sh
df -h .
```

Record a new observation time before reporting the result:

```sh
date -Iseconds
```

Do not silently replace the original baseline. Keep a separately dated update
if you need a new baseline.

## Interpretation

Use the distribution to select appropriate package instructions and the
architecture to select compatible software builds. Use pwd to confirm where
relative filenames point. A readable report does not prove service health.

## If a file cannot be found

Run pwd to check your location. If you are outside the baseline project, use the
full quoted home-based path above, then run cat baseline.md again. If the
correct directory still lacks the file, stop and inspect the Project 01 result.
Do not create an empty replacement or claim the missing evidence exists.

## Stop conditions

Stop if the account is wrong, the intended directory cannot be established, or
the baseline is missing or inconsistent. Do not use administrator privileges or
broad permission changes as a shortcut.

## Next action

Complete the Day 01 assessment. Continue with files, paths, and project workspace
practice after the Day 01 checks are satisfied.
````

Save with `Esc`, `:wq`, Enter. The outer four-backtick fence is not part of the file. Internal three-backtick fences format the commands in Markdown.

Read the saved guide:

```sh
cat handover.md
```

Check the timestamp against the original baseline. The guide uses `$HOME` rather than exposing your personal home-directory prefix. Explain it as a portable shell variable, not a path that every computer automatically has.

## Step 4, follow your own handover from the beginning

Your test is whether the instructions work, not whether the writing looks convincing. Leave the project directory:

```sh
cd "$HOME"
```

Now follow the Operator walkthrough in your saved handover, one command at a time. It should take you to `system-baseline` and print the real `baseline.md`.

Compare the report's timestamp and recorded environment with the Source record in your handover. They must agree. If they do not, correct the handover and repeat the walkthrough before recording success.

An optional peer test uses another authorized person in the same lab context. Do not give them account credentials or remote access merely to complete this exercise. You can complete the self-test without a peer.

## Step 5, test a harmless failure and recover

You will intentionally use a relative filename from the wrong project directory. This simulates an operator who remembered the filename but not the location. It changes no files.

Enter the handover directory:

```sh
cd "$HOME/veriqta-devops-labs/linux/day-01/portfolio/environment-handover"
```

List its contents:

```sh
ls -l
```

Confirm that it has `handover.md` and does not have `baseline.md`. If an earlier attempt left a baseline here, preserve it and record that this particular missing-file test is not applicable until you use a clean test directory. Do not delete work just to force an expected error.

Run:

```sh
cat baseline.md
```

Expected pattern, when that file is absent: an error saying it cannot find `baseline.md`. Exact wording varies. This does not mean the baseline vanished. The relative name was resolved in the wrong directory.

Inspect your location:

```sh
pwd
```

The result should end in `environment-handover`. Follow your handover's recovery instruction:

```sh
cd "$HOME/veriqta-devops-labs/linux/day-01/portfolio/system-baseline"
```

Read the baseline again:

```sh
cat baseline.md
```

You should now see the actual report. The explanation is specific: the file was present, but the earlier command looked in another directory. You recovered by correcting the working directory. You did not need sudo, a permission change, or a new baseline.

## Step 6, document the project for a portfolio visitor

Return to the handover directory:

```sh
cd "$HOME/veriqta-devops-labs/linux/day-01/portfolio/environment-handover"
```

Create its README:

```sh
vi README.md
```

Enter this document and fill the reflection field after performing the test:

```markdown
# Linux Environment Handover

## Overview

I created an operator guide for locating and interpreting a Linux lab baseline.
I tested its navigation steps and investigated a relative-path failure.

## Project files

- [Operator handover](handover.md).
- [Walkthrough and recovery evidence](verification.md).
- [Source baseline](../system-baseline/baseline.md).

## Reproduce the project

Build the local System Baseline project first. Read the handover's prerequisites,
then follow its Operator walkthrough from your own home directory. Verify the
source report rather than copying another operator's observed values.

For the controlled failure, enter the environment-handover directory and check
that it has no baseline.md. Read that relative filename, inspect your working
directory after the error, then navigate to system-baseline and read it again.
The test performs no deletion or configuration change.

## Result and interpretation

[replace with your actual walkthrough result, failure observation, and recovery]

## Limits

Local navigation requires the established local workspace. A public GitHub
visitor can inspect the linked source report online. This handover does not
provide remote access or establish application health.
```

Save, exit, and run `cat README.md`. The `../` in the source link means move up from `environment-handover` to the portfolio root, then enter its sibling `system-baseline`. That is why the repository folder layout must match the tutorial.

## Step 7, record actual verification evidence

Capture a check time:

```sh
date -Iseconds
```

Create the record:

```sh
vi verification.md
```

Enter the following, replacing every `[replace ...]` field with your result:

```markdown
# Handover Walkthrough and Recovery

Tested at: [replace with timestamp and timezone offset]

## Walkthrough

Starting location: my home directory, represented as $HOME.
Guide used: handover.md, Operator walkthrough.
Source report: ../system-baseline/baseline.md.

| Check | Actual result |
| --- | --- |
| Correct regular account confirmed | [replace with actual outcome] |
| Instructions reached the intended project | [replace with actual outcome] |
| Baseline opened and source details matched | [replace with actual outcome] |
| Handover file was saved and reread | [replace with actual outcome] |

## Controlled failure

Command: cat baseline.md.
Working directory: the environment-handover project directory.
Precondition: no baseline.md was present in that directory.
Actual symptom: [replace with the relevant redacted error, or explain why the test was not applicable].

## Diagnosis

A relative filename is interpreted from the current working directory. The
baseline belongs to system-baseline, not environment-handover.

## Recovery and verification

Action taken: [replace with your actual recovery action].
Result after repeating the read: [replace with the actual outcome].

## Reflection

[replace with one sentence explaining how this guide reduces guesswork for an operator]
```

Save it, then run `cat verification.md`. Do not mark a skipped or failed test as successful. If you changed the guide after finding a mistake, repeat its walkthrough and record the result of that corrected version.

## Step 8, publish beside your baseline

Open your own `linux-foundations-portfolio` repository. Using the Create new file procedure from [Project 01, Step 8](01%20System%20Baseline.md#step-8-publish-the-three-project-files), publish these reviewed files from the repository's top level:

| GitHub filename | Local file to copy |
| --- | --- |
| environment-handover/README.md | This project's README.md. |
| environment-handover/handover.md | This project's handover.md. |
| environment-handover/verification.md | This project's verification.md. |

Use meaningful commit messages, for example `Add tested Linux environment handover`. Use the same branch as the published baseline, following any repository review rules. Never copy the private original baseline or your full terminal history into the public repository.

## Step 9, connect both projects on your portfolio homepage

Open the top-level README in your personal portfolio and select its pencil edit icon. In the Projects list, retain the existing System Baseline link and add:

```markdown
- [Linux Environment Handover](environment-handover/README.md), operator guidance,
  a tested walkthrough, and a documented path-error recovery.
```

Preview and commit. This is your portfolio homepage, not VERIQTA's training README.

Follow the new link. Then open the handover, verification record, and source baseline from the project's README. All should work. Verify that the source link points to the real published baseline and that the Markdown commands render correctly.

For a public repository, check the project in a signed-out window. A public visitor should be able to inspect both projects without needing your local computer.

## Troubleshooting your handover project

| Symptom | Cause to inspect | Fix and verification |
| --- | --- | --- |
| Walkthrough cannot find the local project | Wrong account, workspace not built, or a mistyped path. | Check id and pwd, then verify Project 01's location. Repeat the walkthrough. |
| Source timestamp differs | You copied a current check time instead of the baseline's capture time, or used a different report. | Compare the actual files, correct the handover, and retest. |
| Controlled error does not occur | A baseline.md is present in the test directory. | Record the actual state and preserve existing work. Do not invent an error. |
| Baseline link fails on GitHub | Wrong sibling path or project files published on different branches. | Check the default branch layout and the ../system-baseline/baseline.md link. |
| Files exist but the homepage has no project link | The root portfolio README was not updated or its change was not committed. | Edit your portfolio's Projects list and follow the saved link. |

## Completion and cleanup

You have finished when the guide works from the stated starting point, source details match, recovery is demonstrated or its test limitation is explained, and the GitHub links expose the reviewed project files correctly.

Retain both local projects. No service, cloud infrastructure, or billable resource was created. Your portfolio now contains the baseline, a usable operator guide, and evidence of a diagnosed failure and verified recovery.

[Projects](README.md) · [Day 01](../README.md)
