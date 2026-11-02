# Project 01, Build a Learning Platform Workspace

## The engineering problem

An application team needs a predictable place for configuration and operating instructions. If every file is in one directory, you can confuse active settings with backups and cannot explain what should be preserved.

Build a small workspace that another learner can reproduce. You will publish its synthetic configuration, directory guide, and verified inventory in your own GitHub portfolio.

## 1. Establish the project location

Use the regular account from the lab:

```bash
id -u
```

Expected: nonzero. Create the portfolio parent:

```bash
mkdir -p "$HOME/veriqta-devops-labs/linux/day-02/portfolio"
```

Expected: no output. Create a fresh project:

```bash
mkdir "$HOME/veriqta-devops-labs/linux/day-02/portfolio/platform-workspace"
```

Expected: no output. If the project already exists, inspect it instead of overwriting it. A retake can use platform-workspace-retry-01 consistently throughout both projects.

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/portfolio/platform-workspace"
```

Expected: no output. Verify:

```bash
pwd
```

Expected: your private home prefix followed by `/linux/day-02/portfolio/platform-workspace`.

## 2. Create the directory responsibilities

```bash
mkdir config docs logs backups scratch
```

Expected: five new directories and no output. Inspect:

```bash
ls -la
```

Expected: those directories. Use config for active synthetic settings, docs for instructions, logs for later runtime output, backups for before-change copies, and scratch for explicitly disposable work.

Create a marker:

```bash
touch -- .lab-only
```

Expected: no output. Verify it appears when hidden names are included:

```bash
ls -la
```

Expected: .lab-only and the five directories. This marker communicates purpose; it does not enforce security.

## 3. Create complete synthetic configuration

```bash
vi config/app.env
```

Expected: vi opens a new file. Press i and enter:

```text
APP_NAME=learning-platform
APP_ENV=lab
RELEASE=v001
SUPPORT_MODE=training
```

Press Esc, enter the following **inside vi**, and press Enter:

```text
:wq
```

Expected: save and return to the shell. Verify:

```bash
cat config/app.env
```

Expected: the four lines above. Each setting is a name and value. These are deliberately invented training settings with no password or token. The file is not executed in this project.

## 4. Write a reproducible project README

```bash
vi README.md
```

Press i in the new file and enter the document below. Its internal command fences belong in the file; the tutorial's outer four-backtick fence does not.

````markdown
# Learning Platform Workspace

## Purpose

I built an organized Linux workspace for synthetic application configuration.
The project demonstrates path handling, directory roles, hidden-file inspection,
and verification of saved files.

## Directory guide

| Directory | Responsibility |
| --- | --- |
| config | Active synthetic application settings. |
| docs | Inventory, decisions, and operating instructions. |
| logs | Reserved for later service output. |
| backups | Before-change copies, introduced in the recovery project. |
| scratch | Only explicitly disposable practice files. |

The .lab-only marker identifies the training workspace. It is not a security control.

## Reproduce locally

Use an authorized Linux lab and a regular account. Choose a fresh workspace.

```bash
mkdir -p "$HOME/veriqta-devops-labs/linux/day-02/portfolio"
```

Create the project directory only if it does not already exist:

```bash
mkdir "$HOME/veriqta-devops-labs/linux/day-02/portfolio/platform-workspace"
```

Enter it:

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/portfolio/platform-workspace"
```

Create the roles:

```bash
mkdir config docs logs backups scratch
```

Create the marker:

```bash
touch -- .lab-only
```

Use vi to create config/app.env with the synthetic values shown in this
repository. Save it, read it from the shell, and inspect the workspace:

```bash
find . -maxdepth 2 -print
```

Directory creation normally prints nothing. The inventory should include the
five roles, marker, and configuration. The working-directory prefix and listing
order can differ between environments.

## Project files

- [Synthetic configuration](config/app.env).
- [Verified inventory](docs/inventory.md).

## Result

[replace with your actual layout and verification result]

## Limits

This project organizes files. It does not start a service, enforce access
permissions, or establish that the configuration is consumed by an application.
````

Replace the result field with your own observations. Save with Esc, then:

```text
:wq
```

Read your saved README:

```bash
cat README.md
```

Expected: the complete project introduction and no unresolved result field.

## 5. Verify the inventory and preserve evidence

```bash
find . -maxdepth 2 -print
```

Expected paths include config/app.env, README.md, .lab-only, and all five directories. Order is not fixed. You have not yet created the inventory file, so it will not appear until you save it below.

Capture the observation time:

```bash
date -Iseconds
```

Expected: your actual timestamp with timezone offset.

```bash
vi docs/inventory.md
```

Press i and enter:

```markdown
# Workspace Inventory

Checked at: [replace with actual timestamp and timezone offset]
Portable local path: $HOME/veriqta-devops-labs/linux/day-02/portfolio/platform-workspace

## Observed entries

[replace with relevant paths from your actual bounded inventory]

## Checks

Configuration content read from the shell: [actual result].
Hidden marker visible in the all-entries listing: [actual result].
README saved and read back: [actual result].

## Decisions

I separated active settings from before-change copies and reserved scratch for
explicitly disposable files. Empty directory names alone do not prove that a
backup, logging system, or application exists.
```

Replace every bracketed field, save with Esc and the editor command:

```text
:wq
```

Read it:

```bash
cat docs/inventory.md
```

Expected: actual observation paths, time, and verification outcomes.

Leave and return:

```bash
cd "$HOME"
```

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/portfolio/platform-workspace"
```

Both normally print nothing. Verify the configuration still exists and has the intended values:

```bash
cat config/app.env
```

Expected: release v001 and the other three original settings.

## 6. Publish the workspace in your portfolio

Use your personal linux-foundations-portfolio repository from Day 01. Work from its top level. GitHub can create files and subdirectories in its web editor. For each path in the table, use Add file, Create new file, paste the corresponding reviewed local contents, preview, and commit to your working branch. On an unrestricted personal training repository you can commit to its default branch; follow any required review rules if direct commits are blocked.

| GitHub file path | Local contents |
| --- | --- |
| platform-workspace/README.md | README.md. |
| platform-workspace/config/app.env | The synthetic four-line configuration. |
| platform-workspace/docs/inventory.md | Your reviewed inventory record. |
| platform-workspace/.lab-only | A short sentence saying this is a training workspace. |

The local marker is empty, but you may give the public marker an explanatory sentence when using the browser editor. Record that documentation difference rather than claiming byte-for-byte identity.

Git does not track empty directories by themselves. The README documents the roles of logs, backups, and scratch even if they do not appear in GitHub until a file is added. Your local inventory is evidence of the local layout, not a claim that the repository already contains every empty directory.

In your personal portfolio's root README, use the pencil editor to add this Projects entry:

```markdown
- [Learning Platform Workspace](platform-workspace/README.md), Linux file layout,
  synthetic configuration, and verified inventory.
```

Preview and commit. Follow the new link and both project-file links. For a public repository, check that a signed-out visitor can open them. Do not modify the shared course README or publish personal home paths or credentials.

## 7. Completion and troubleshooting

| Symptom | Check and correction | Verification |
| --- | --- | --- |
| Project directory already exists | Inspect it and preserve earlier work; use a fresh attempt name for a retake. | The intended path is established before writing. |
| Configuration cannot be saved | Confirm config exists and you are in the project directory. | The saved file can be read from the shell. |
| Hidden marker seems missing | Use a listing that includes hidden entries. | .lab-only is visible. |
| Empty folders do not appear on GitHub | Empty directories alone are not tracked. Keep their roles in the README. | Public file links work; local inventory remains accurate. |
| Public paths are nested twice | Check the filename path relative to the repository top level. | The root project link reaches the correct README. |

Keep this workspace. Project 02 uses its active configuration. No service or cloud resource was created.

[Continue to Project 02](02%20Configuration%20Change%20and%20Recovery.md) · [Projects](README.md)
