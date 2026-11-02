# Project 02, Configuration Change and File Recovery

## The engineering problem

A change request asks you to update the training configuration from release v001 to v002. The change is then withdrawn. You need to recover the earlier file and prove that recovery worked without destroying your evidence.

You will use the workspace from Project 01, preserve the starting configuration, apply one controlled edit, show the difference, restore the original, and publish a change record and reusable recovery instructions.

This is file-level recovery practice. A production backup strategy also needs independent storage, retention, access controls, and application-consistent recovery procedures.

![Preserve, change, compare, restore, and verify.](../07%20Images/recovery.svg)

Text equivalent: make and verify a before-change copy, change only the active file, observe the difference, restore from the preserved copy, and verify equality and readable content.

## 1. Inspect the starting state

```bash
id -u
```

Expected: nonzero. Enter the existing project:

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/portfolio/platform-workspace"
```

Expected: no output. If you used a retry name in Project 01, use it consistently here.

```bash
pwd
```

Expected: the intended platform-workspace path. Read the active file:

```bash
cat config/app.env
```

Expected: APP_NAME=learning-platform, APP_ENV=lab, RELEASE=v001, and SUPPORT_MODE=training. If the release differs, inspect the existing history before starting a new change attempt.

Check your backup destination:

```bash
ls -l -- backups/app.env.before-v002
```

Expected on the first attempt: a file-not-found error. If it exists, preserve it and choose a fresh backup name throughout this attempt. Do not overwrite an earlier recovery source.

## 2. Preserve and verify the original

```bash
cp -i -- config/app.env backups/app.env.before-v002
```

Expected: no output for the new destination. Compare:

```bash
cmp -- config/app.env backups/app.env.before-v002
```

Expected: no output. Immediately check:

```bash
echo $?
```

Expected: zero. Stop if the files differ or cannot be read. A backup needs to be verified before you depend on it.

Record the starting time:

```bash
date -Iseconds
```

Expected: current time with timezone offset. Retain it for the change record.

## 3. Apply the requested edit

```bash
vi config/app.env
```

Expected: the active configuration opens. Press Esc to ensure normal mode. Enter this search **inside vi** and press Enter:

```text
/RELEASE=v001
```

Expected: the cursor moves to the release line. Press zero to reach the beginning of the line, then capital C to replace that line, and type:

```text
RELEASE=v002
```

Press Esc and save:

```text
:wq
```

Expected: the editor exits after writing. Read the active file:

```bash
cat config/app.env
```

Expected: only the release value changed to v002. Read the backup:

```bash
cat backups/app.env.before-v002
```

Expected: v001 remains. Compare:

```bash
cmp -- config/app.env backups/app.env.before-v002
```

Expected: a difference message. Immediately run:

```bash
echo $?
```

Expected: one. A higher value means a comparison error, not successful proof of an intended change.

## 4. Recover when the change is withdrawn

The intended action now is to replace the active configuration with its verified before-change copy. Inspect the source and destination names carefully.

```bash
cp -i -- backups/app.env.before-v002 config/app.env
```

Expected: an overwrite prompt for config/app.env. Confirm that target, type y, and press Enter. Do not approve any unexpected file.

```bash
cmp -- config/app.env backups/app.env.before-v002
```

Expected: no output. Immediately check:

```bash
echo $?
```

Expected: zero. Read the active configuration:

```bash
cat config/app.env
```

Expected: release v001 and the unchanged other settings. The backup must still exist; the restoration used a copy, not a move.

```bash
ls -l -- backups/app.env.before-v002
```

Expected: a regular-file listing. Capture a finish time:

```bash
date -Iseconds
```

Expected: actual completion time with offset. Record the result; do not infer success from the overwrite prompt alone.

## 5. Write a complete change record

```bash
vi docs/change-record.md
```

Press i in a new file and enter:

```markdown
# Configuration Change and Recovery Record

## Request

Change the training configuration from release v001 to v002, then restore v001
when the change is withdrawn.

## Scope

A synthetic file in the local platform-workspace. No running application or
production system is changed.

## Timeline

Started at: [replace with actual timestamp and offset].
Finished at: [replace with actual timestamp and offset].

## Evidence

| Stage | Active release | Backup release | Comparison result |
| --- | --- | --- | --- |
| Before edit | [actual value] | [actual value] | [actual result] |
| After edit | [actual value] | [actual value] | [actual result] |
| After restore | [actual value] | [actual value] | [actual result] |

## Interpretation

[replace with what the comparison and file reads actually demonstrated]

## Problems encountered

[replace with an actual issue and verified correction, or state that none occurred]

## Limits

The checks establish file content equality at verification time. They do not
prove application health, metadata equality, or a complete disaster-recovery capability.
```

Fill every field from your actual run. Save with Esc and the editor command:

```text
:wq
```

Verify the record:

```bash
cat docs/change-record.md
```

Expected: a coherent timeline with no unresolved fields and no claim that an application was deployed.

## 6. Write reusable recovery instructions

```bash
vi docs/recovery.md
```

Press i and enter:

````markdown
# Restore the Training Configuration

## Scope and prerequisites

Use the authorized regular account and the existing Day 02 platform-workspace.
A verified backups/app.env.before-v002 must exist. Inspect its content before
using it. This procedure deliberately replaces config/app.env.

## Locate and inspect

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/portfolio/platform-workspace"
```

Normally there is no output. Verify the location:

```bash
pwd
```

The path must end with the intended project directory. Inspect both files:

```bash
cat config/app.env
```

```bash
cat backups/app.env.before-v002
```

The preserved copy should contain the intended v001 configuration. Stop if the
backup is missing, unverified, or not the version you intend to restore.

## Restore

```bash
cp -i -- backups/app.env.before-v002 config/app.env
```

Check the overwrite target, then answer y only for the intended training file.

## Verify

```bash
cmp -- config/app.env backups/app.env.before-v002
```

No comparison output is expected for equality. Read its status immediately:

```bash
echo $?
```

Zero means equal. One means different. A higher value means a comparison error.
Read the restored file as well:

```bash
cat config/app.env
```

Expected: the v001 configuration. The before-change copy remains in backups.
Record the actual result and time in the change record. Do not claim service
recovery because this procedure does not run an application health check.
````

Save with Esc, then:

```text
:wq
```

Expected: return to the shell. Read the procedure:

```bash
cat docs/recovery.md
```

Expected: your complete saved procedure. Adapt the path if you used a retry directory. Follow its locate and verification sections from outside the project to confirm the instructions work. There is no need to overwrite an already restored file again merely to add a test count.

## 7. Publish the recovery project

In your own linux-foundations-portfolio repository, add these files using the browser's Add file, Create new file workflow. Start at the repository root and enter each full path, paste the reviewed local contents, preview, and commit on the same branch as Project 01.

| GitHub path | Contents |
| --- | --- |
| platform-workspace/backups/app.env.before-v002 | Preserved synthetic v001 configuration. |
| platform-workspace/docs/change-record.md | Your actual change and verification record. |
| platform-workspace/docs/recovery.md | Your reusable recovery instructions. |

Verify the published active configuration at platform-workspace/config/app.env still agrees with your final restored local v001 file. If it differs, inspect why before updating the public copy. Never publish real service configuration or credentials.

Edit the project README and add:

```markdown
## Configuration change and recovery

- [Change record](docs/change-record.md).
- [Recovery procedure](docs/recovery.md).
- [Preserved v001 configuration](backups/app.env.before-v002).
```

Preview and commit. Follow every link. In your personal portfolio root README, expand the existing workspace entry to mention the demonstrated file restoration. You do not need a duplicate root entry or a new repository.

## 8. Troubleshooting and completion

| Symptom | Investigation | Safe result |
| --- | --- | --- |
| Backup destination already exists | Inspect previous work before creating a new attempt name. | Original recovery sources are preserved. |
| Active file and backup differ before editing | Read both files and inspect the intended source and destination. | A verified starting copy exists before the change. |
| Comparison says file not found | Check working directory, spelling, and case. | Both intended inputs can be read. |
| Restore prompt names an unexpected file | Decline and inspect the command and current directory. | Only the intended active file is replaced. |
| Public instructions link to the wrong file | Inspect repository paths and branch placement. | The project README reaches all reviewed artifacts. |

Complete the project when the original copy is preserved, v002 was observed, v001 was restored and compared successfully, and your published record explains those actual checks. Retain the workspace. No cloud resources or services need removal.

## References

- [GitHub file creation](https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files).
- [GitHub file editing](https://docs.github.com/en/repositories/working-with-files/managing-files/editing-files).
- [Day 02 command explanations](../01%20Notes/README.md).

[Projects](README.md) · [Knowledge Checks](../04%20Knowledge%20Checks/README.md) · [Day 02](../README.md)
