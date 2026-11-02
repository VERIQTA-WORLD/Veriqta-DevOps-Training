# Day 02 practical assessment

## Live lab, prepare a configuration release without losing the original

A teammate delivered a new synthetic configuration file, but the active workspace still uses the older release. Their handover points to the wrong directory name. You must preserve the original, place the new content correctly, repair the instructions, remove only approved disposable material, and prove that protected files remain unchanged.

This is an independent task on your actual Linux lab. The setup creates the starting state; it does not solve the release task.

| Condition | Requirement |
| --- | --- |
| Working time | 45 minutes after setup. |
| Environment | Authorized Linux lab, regular account, Bash, vi, Coreutils, Findutils, and Diffutils. |
| References | Day 02 notes and official documentation for syntax. No copied full solution. |
| Scope | This fresh assessment attempt only. Preserve Day 01, the Day 02 lab, and portfolio work. |
| Completion | At least 80 out of 100, all mandatory checks met, and timing recorded honestly. |

Timing and scoring are manual. This Markdown page does not monitor or grade your terminal automatically. A reviewer can observe the checkpoints, or you can self-assess against actual files and output after stopping the timer.

![Inspect, preserve, change, and verify in a bounded assessment workspace.](../07%20Images/assessment.svg)

Text equivalent: inspect the starting files, preserve the old configuration, publish the candidate content to the active location, repair navigation, and verify both the intended change and protected originals.

## Preparation, outside the timer

### 1. Use a fresh private attempt

```bash
id -u
```

Expected: a nonzero ID. Stop if you are root.

```bash
mkdir -p "$HOME/veriqta-devops-labs/linux/day-02/assessment"
```

Expected: no output. Create the attempt without accepting an existing one:

```bash
mkdir "$HOME/veriqta-devops-labs/linux/day-02/assessment/attempt-01"
```

Expected: no output. If it already exists, stop and use attempt-02 consistently for a retake. Preserve the old attempt.

```bash
cd "$HOME/veriqta-devops-labs/linux/day-02/assessment/attempt-01"
```

Expected: no output. Check:

```bash
pwd
```

Expected: the chosen attempt path. Create its roles:

```bash
mkdir config incoming backups docs scratch
```

Expected: no output and five directories.

### 2. Create the existing active configuration

```bash
vi config/app.env
```

Press i in the new file and enter:

```text
APP_NAME=learning-platform
APP_ENV=assessment
RELEASE=v001
```

Save with Esc, then this **editor command** and Enter:

```text
:wq
```

Expected: return to the shell. Verify:

```bash
cat config/app.env
```

Expected: exactly the three v001 lines above.

### 3. Create the incoming candidate

```bash
vi incoming/app-v002.env
```

Press i and enter:

```text
APP_NAME=learning-platform
APP_ENV=assessment
RELEASE=v002
```

Save with Esc, then:

```text
:wq
```

Read it:

```bash
cat incoming/app-v002.env
```

Expected: the three v002 lines. This is the delivered candidate, which must remain unchanged during your task.

### 4. Create the faulty handover

```bash
vi docs/operator.md
```

Press i and enter:

````markdown
# Operator Instructions

From the attempt directory, the active configuration is Config/app.env.

```bash
cat Config/app.env
```

The incoming file can be deleted after the new file is installed. There is no
need to preserve the earlier active file. A readable file proves service health.
````

The outer four-backtick fence is tutorial formatting. Include the internal command fence in the file. Save with Esc, then:

```text
:wq
```

Expected: saved file and return to the shell. Verify:

```bash
cat docs/operator.md
```

Expected: the intentionally faulty instructions above. Do not correct them during preparation.

### 5. Create disposable and protected scratch files

```bash
touch -- scratch/obsolete.txt
```

Expected: no output, a disposable empty file.

```bash
vi scratch/keep.txt
```

Press i and enter:

```text
Keep this assessment note unchanged.
```

Save with Esc, then:

```text
:wq
```

Verify:

```bash
cat scratch/keep.txt
```

Expected: the exact sentence above. Only obsolete.txt is approved for removal. The scratch directory itself must remain because it contains the protected file.

### 6. Start timing

```bash
date -Iseconds
```

Expected: your actual timestamp with timezone offset. Record it and start a 45-minute timer on your device. Continue independently with the task brief.

## Task brief

### A. Inspect and record the starting state, 10 minutes

Establish the attempt's actual directory layout, account context, active release, incoming release, and protected scratch contents. Record a bounded inventory and relevant actual output. Identify the handover's path failure from a real attempted read and your location evidence.

### B. Preserve the original and apply the candidate, 15 minutes

Preserve the original v001 active configuration as backups/app.env.v001. Verify that preserved copy before replacing the active file. Install the incoming v002 content at config/app.env while keeping the incoming file unchanged.

Demonstrate that the final active content matches the incoming candidate and differs from the preserved v001 copy. Record the relevant comparison statuses immediately after the comparisons. No service needs to be started or reloaded.

### C. Repair instructions and perform bounded cleanup, 10 minutes

Correct docs/operator.md so an operator can locate and read the active file from a stated starting point. Fix the instructions about retaining the candidate and before-change copy. Explain that file readability alone is not service health.

Remove only scratch/obsolete.txt. Keep scratch/keep.txt unchanged and keep its parent directory. Do not use recursive deletion or administrator privileges.

### D. Verify and deliver evidence, 10 minutes

Leave the attempt directory, follow the corrected handover, and read the active configuration successfully. Prove the original v001 copy, unchanged incoming v002 candidate, and protected scratch note are all still present with the required contents.

Create docs/assessment-evidence.md recording actual start and finish times, elapsed time, original error, diagnosis, before-change verification, final comparisons, cleanup evidence, and any unresolved limitation. Retain actual output, not just a written claim of success. Stop the timer after recording your finish timestamp.

## Required final state

| Path within the attempt | Required result |
| --- | --- |
| config/app.env | v002, matching the incoming candidate. |
| incoming/app-v002.env | Original candidate unchanged. |
| backups/app.env.v001 | Verified original v001 content. |
| docs/operator.md | Correct path, working navigation, preservation guidance, and accurate health limits. |
| docs/assessment-evidence.md | Actual observations, command results, timing, and recovery explanation. |
| scratch/keep.txt | Original protected sentence unchanged. |
| scratch/obsolete.txt | Absent after approved removal. |

## Scoring

| Area | Marks | Observable evidence |
| --- | --- | --- |
| Starting-state inspection | 20 | Correct location and account, 5. Relevant inventory and actual release observations, 10. Genuine path-error evidence, 5. |
| Preservation and change | 35 | Original v001 copy verified before replacement, 15. Final active content equals incoming v002, 10. Candidate unchanged and old copy differs from active with valid comparison results, 10. |
| Handover and cleanup | 25 | Corrected instructions work after leaving the directory, 10. Preservation and health statements corrected, 5. Only the approved file removed and protected note unchanged, 10. |
| Evidence and timing | 20 | Actual outputs and results support the claims, 10. Start, finish, and elapsed time are recorded honestly, 5. Limits and unresolved issues are explained, 5. |

Mandatory checks: the preserved v001 copy exists, the incoming candidate and protected note remain unchanged, active v002 is verified, the handover works, and work stays inside the authorized scope. Fabricated output cannot satisfy a criterion.

Pass requires at least 80, all mandatory checks, and completion within 45 minutes. If correct but slower, record completed outside the target and use a fresh attempt for a retake. Record interruptions as interruptions, not uninterrupted timed success.

After grading, explain why a copy was required instead of a move, how case caused the original path failure, and why removing the entire scratch directory would have been incorrect. Keep the attempt. No service or cloud resources need teardown.

[Notes](../01%20Notes/README.md) · [Troubleshooting](../06%20Troubleshooting/README.md) · [Day 02](../README.md)
