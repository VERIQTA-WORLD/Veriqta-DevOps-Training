# Day 02 troubleshooting

Preserve the exact command, current location, and error before changing anything. All examples below assume the guided lab's learning-platform directory. If your problem is in a project or assessment, use its actual path and filenames instead.

![Inspect location, names, content, and recovery evidence before continuing.](../07%20Images/troubleshooting.svg)

Text equivalent: locate the task workspace, inspect actual source and destination names, use a bounded correction, and repeat the verification that failed.

## A relative filename cannot be found

Inspect your location:

```bash
pwd
```

Expected: the actual current path. A different directory can explain a failed relative read.

Return to the lab project when that is the task you are doing:

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/lab/learning-platform"
```

Expected: no output if it exists. Then inspect the intended child directory:

```bash
ls -la -- config
```

Expected: app.env in the completed lab. Check capitalization and spelling. Do not create a duplicate at the wrong location just to satisfy a mistaken command.

## A copy or move asks about overwriting

Inspect the named destination before approving a change. In the lab, read the active configuration:

```bash
cat config/app.env
```

Expected: the actual current release. Read the recovery source:

```bash
cat backups/app.env.v001
```

Expected: the preserved v001 content after the backup step. If the target is unexpected or the recovery source is unverified, answer n at the prompt and investigate. Do not treat a prompt as proof that the operation succeeded.

## A comparison result is unclear

Compare the actual lab files:

```bash
cmp -- config/app.env backups/app.env.v001
```

Expected: silence for equal bytes, a difference message for different content, or an error for trouble. Immediately inspect its status:

```bash
echo $?
```

Expected: zero for equal, one for different, greater than one for trouble. If you ran another command first, repeat the comparison and inspect the status immediately. Read both files to understand a difference rather than blindly replacing one.

## An empty-directory removal fails

Inspect hidden entries in the directory you intended to remove:

```bash
ls -la -- scratch
```

Expected before cleanup: the renamed practice file may remain. After approved file removal, only the dot entries should remain. Keep any unexpected content until its purpose is established. Do not replace an empty-directory operation with broad recursive deletion.

## A directory copy created an extra level

Inventory the current lab with a bounded read-only traversal:

```bash
find . -maxdepth 3 -print
```

Expected: actual paths beneath your current directory, order not guaranteed. If you see a source directory nested inside an existing destination, inspect whether the destination already existed. Preserve the results and use a fresh destination on a new attempt. Do not silently delete an old snapshot to make the layout resemble an example.

## Permission denied, unexpected editor warning, or missing utility

Confirm that you are using the authorized regular account and the intended private path. Preserve the exact message. Do not add administrator privileges, apply broad permission changes, remove editor recovery files blindly, or run an unreviewed installer. Tool installation and environment correction require instructions appropriate to your actual distribution.

## Publishing problems

| Symptom | What to inspect | Successful verification |
| --- | --- | --- |
| README link fails | Repository path, capitalization, relative location, and branch. | Open the target from the saved README. |
| Empty directory is absent | Whether any tracked file exists in it. | Local inventory and public documentation accurately describe different scopes. |
| Template fields remain | Raw file content before committing. | Your own observations replace every result field. |
| Private data was published | Current content and relevant history, not just the visible line. | Sensitive access is contained and any exposed credential is revoked or rotated. |

When asking for help, include the tool, day, section, exact command, expected result, actual redacted result, and last successful checkpoint. Do not upload your entire home directory.

[Notes](../01%20Notes/README.md) · [Day 02](../README.md)
