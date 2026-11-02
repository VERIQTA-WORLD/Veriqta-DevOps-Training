# Day 02 follow-along lab

Build a learning-platform workspace and practice a controlled file change. This is a filesystem lab with synthetic configuration, not a running application. Use no real credentials.

## 1. Establish your lab context

```bash
id -u
```

Expected: a nonzero numeric ID. Stop if you are using root.

```bash
mkdir -p "$HOME/veriqta-devops-labs/linux/day-02"
```

Expected: no output. Create a fresh lab directory:

```bash
mkdir "$HOME/veriqta-devops-labs/linux/day-02/lab"
```

Expected: no output. If it already exists, stop and inspect it. For a repeat, use lab-retry-01 consistently instead of overwriting an existing result.

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/lab"
```

Expected: no output. Confirm:

```bash
pwd
```

Expected: your home prefix followed by `/linux/day-02/lab`.

## 2. Build the project layout

```bash
mkdir -p learning-platform/config learning-platform/docs learning-platform/logs learning-platform/backups learning-platform/scratch
```

Expected: no output. Each space separates a different directory argument. The option creates the shared parent as needed.

```bash
cd learning-platform
```

Expected: no output. Inspect the top level:

```bash
ls -la
```

Expected: config, docs, logs, backups, and scratch, plus dot entries. These names represent configuration, instructions, later log output, before-change copies, and disposable practice work.

![The directories and their intended responsibilities.](../07%20Images/workspace.svg)

Text equivalent: separate configuration, documentation, logs, backups, and disposable files so that each operation has an explicit scope.

## 3. Add a hidden lab marker

```bash
touch -- .lab-only
```

Expected: no output and an empty hidden marker. Check ordinary entries:

```bash
ls -l
```

Expected: the five directories, without the marker. Include hidden entries:

```bash
ls -la
```

Expected: .lab-only is now included. Hidden is a naming convention, not an access control.

## 4. Create synthetic configuration

```bash
vi config/app.env
```

Expected: vi opens a new file. Press i and enter:

```text
APP_NAME=learning-platform
APP_ENV=lab
RELEASE=v001
```

Press Esc, then use this **editor command** and press Enter:

```text
:wq
```

Expected: vi saves and exits. Read the result:

```bash
cat config/app.env
```

Expected: the three lines above. The filename resembles configuration used by applications, but nothing is executing it in this exercise.

## 5. Make and verify a before-change copy

```bash
cp -i -- config/app.env backups/app.env.v001
```

Expected: no output when the destination is new. The source remains in config. If prompted to overwrite, answer n, inspect your earlier work, and choose a fresh backup name rather than replacing your evidence.

```bash
cmp -- config/app.env backups/app.env.v001
```

Expected: no output when equal. Immediately run:

```bash
echo $?
```

Expected: zero. A nonzero result needs investigation before you modify the active configuration.

## 6. Practice a controlled rename

```bash
touch -- scratch/change-draft.txt
```

Expected: no output. Rename the file:

```bash
mv -i -- scratch/change-draft.txt scratch/change-review.txt
```

Expected: no output for a new destination. Inspect the directory:

```bash
ls -la -- scratch
```

Expected: change-review.txt, without change-draft.txt. A rename changes the name used to reach that file; it does not create a second backup copy.

## 7. Change the active configuration

```bash
vi config/app.env
```

Expected: the saved configuration opens. In normal mode, type the following **inside vi** and press Enter:

```text
/RELEASE=v001
```

This searches for the release line. Press the zero key to move to its beginning, press capital C to replace that line from the cursor to its end, and type:

```text
RELEASE=v002
```

Press Esc, then save and exit:

```text
:wq
```

Read the active file:

```bash
cat config/app.env
```

Expected: APP_NAME and APP_ENV are unchanged and RELEASE is v002. Read the preserved copy:

```bash
cat backups/app.env.v001
```

Expected: RELEASE is still v001. If you changed the backup instead of the active file, stop and record the mistake before proceeding.

Compare the files:

```bash
cmp -- config/app.env backups/app.env.v001
```

Expected: a difference message. Immediately read the status:

```bash
echo $?
```

Expected: one. That is the intended content difference, not a missing-file error.

## 8. Restore and verify

You are deliberately replacing the active file with the verified v001 copy. Inspect the names above before answering the prompt.

```bash
cp -i -- backups/app.env.v001 config/app.env
```

Expected: an overwrite prompt naming config/app.env. Type y and press Enter after confirming that this is the intended lab file. Then compare:

```bash
cmp -- config/app.env backups/app.env.v001
```

Expected: no output. Immediately run:

```bash
echo $?
```

Expected: zero. Read the restored file:

```bash
cat config/app.env
```

Expected: RELEASE=v001. Your recovery evidence needs both a verified comparison and a readable restored result. This demonstrates file restoration, not database recovery or application health.

## 9. Inspect the finished workspace

```bash
find . -maxdepth 2 -print
```

Expected: the project directories, marker, configuration, backup, and renamed scratch file. Order can differ. The inventory should include config/app.env and backups/app.env.v001.

Create a short record:

```bash
vi docs/lab-results.md
```

Press i in a new file and enter the following, replacing the bracketed fields with actual observations:

```markdown
# Workspace Lab Results

Observed at: [actual timestamp with timezone offset]
Workspace: $HOME/veriqta-devops-labs/linux/day-02/lab/learning-platform
Initial copy comparison: [actual result]
Changed active release: [actual value]
Preserved backup release: [actual value]
Comparison after the controlled change: [actual result]
Restored active release: [actual value]
Comparison after restoration: [actual result]
Limitation: This is a synthetic file-change exercise, not a running service test.
```

Save with Esc, then the editor command:

```text
:wq
```

Capture the timestamp if needed:

```bash
date -Iseconds
```

Expected: actual time with offset. Enter it in the record, save again, and read:

```bash
cat docs/lab-results.md
```

Expected: a complete record of the checks you actually performed.

## 10. Resume and clean up only disposable work

Leave the project:

```bash
cd "$HOME"
```

Return using the full home-based path:

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/lab/learning-platform"
```

Both commands normally print nothing. Verify persistence:

```bash
cat config/app.env
```

Expected: the restored v001 content. Remove only the empty scratch file created in this lab:

```bash
rm -i -- scratch/change-review.txt
```

Expected: a removal prompt. Confirm the filename, type y, and press Enter. Check scratch:

```bash
ls -la -- scratch
```

Expected: only its dot entries. Remove that now-empty directory:

```bash
rmdir -- scratch
```

Expected: no output. Leave config, docs, logs, backups, and .lab-only intact. No broad recursive deletion or cloud teardown is needed.

## Checkpoint

Keep your lab. You have a known layout, preserved source evidence, a before-change copy, a demonstrated difference, and a verified restoration. Continue with the portfolio projects to build and publish your own reproducible work.

For a shorter session, stop after Step 5 and record that checkpoint. Resume with the same workspace and inspect its state before making the change.

[Portfolio Projects](../03%20Portfolio%20Projects/README.md) · [Day 02](../README.md)
