# Day 01 practical assessment

## Live lab, validate a Linux environment and repair its handover

You are taking over a small Linux training environment. A previous operator left an incomplete environment report and a handover containing a wrong file location. You must investigate the actual system, correct unsupported statements, restore a usable handover, and prove that another operator could follow it.

You perform the assessment on your own Linux machine. You are assessed on actions and observable results, not on writing an essay about commands.

| Assessment condition | Requirement |
| --- | --- |
| Working time | 40 minutes, starting after the setup checkpoint. |
| Environment | Your authorized Linux lab, Bash, vi, and a regular account. |
| Scope | Files inside this assessment attempt and read-only environment inspection. |
| Allowed reference | Day 01 notes and official command documentation for syntax. |
| Independent work | Choose and execute your own inspection and repair commands. Do not use a generated complete solution or another learner's results. |
| Submission | Corrected report, working handover, and evidence from your actual run. |
| Passing result | At least 80 out of 100, with all mandatory completion checks satisfied. |

The timer is manual. This page does not monitor your terminal, collect results, or grade automatically. You can self-assess against the rubric, or have an instructor observe the same checkpoints. If you need more time, record your elapsed time honestly, finish the work, and repeat a fresh timed attempt after reviewing the gaps.

![Independent work requires locating, verifying, recording, and explaining actual results.](../07%20Images/practical-assessment.svg)

Text equivalent: inspect the real environment, correct the report, repair the navigation instructions, and verify that the saved results work after leaving and returning.

## Preparation, outside the timer

Complete the guided lab and portfolio projects first. The setup below creates the assessment's starting state. It is not the solution and earns no marks.

### 1. Check your account

Copy and run:

```bash
id -u
```

Expected result: a nonzero numeric ID. If it is zero, stop and use an existing authorized regular lab account. Do not alter shared accounts or permissions.

### 2. Create a fresh attempt

Create the parent directory:

```bash
mkdir -p "$HOME/veriqta-devops-labs/linux/day-01/assessment"
```

Expected result: normally no output. Existing contents are preserved.

Create a new attempt directory:

```bash
mkdir "$HOME/veriqta-devops-labs/linux/day-01/assessment/attempt-01"
```

Expected result: no output. This time there is no parent-creation option: if the attempt already exists, the command should report that it exists. Stop rather than overwrite it. Use a new name such as attempt-02 consistently throughout these setup commands for a retake.

Enter your new attempt:

```bash
cd "$HOME/veriqta-devops-labs/linux/day-01/assessment/attempt-01"
```

Expected result: normally no output. Verify your location:

```bash
pwd
```

Your path should end in `/assessment/attempt-01`, or the new attempt name you chose.

Create the report directory:

```bash
mkdir records
```

Expected result: no output. This creates a directory inside the attempt, rather than elsewhere on the machine.

### 3. Create the faulty source report

Open the report file:

```bash
vi records/environment-report.md
```

Expected result: vi opens a new file buffer. Press i to type. Enter this starting document exactly as shown. Its errors are deliberate assessment inputs.

```markdown
# Environment Report

Captured at: not recorded.
Observed kernel: not checked.
Observed distribution: not checked.
Observed architecture: not checked.
Observed Bash version: not checked.
User context: not checked.
Workspace: not checked.
Available space: not checked.

## Previous operator conclusions

A Linux kernel name proves that the distribution is Ubuntu.
Every Linux software download works on every machine architecture.
The current directory's free-space figure describes all disks on the machine.
A readable environment report proves that the application is healthy.
```

Press Esc, enter the following **inside vi**, and press Enter:

```text
:wq
```

Expected result: vi saves the file and returns to the shell. Confirm that the starting file was saved:

```bash
cat records/environment-report.md
```

Expected result: the faulty report above. Do not correct it during preparation.

### 4. Create the faulty handover

Open the handover file:

```bash
vi handover.md
```

Press i and enter:

````markdown
# Operator Handover

The environment report is in the current attempt's top-level directory.

From the attempt directory, read the report with:

```bash
cat environment-report.md
```

If reading the report works, the whole application is healthy.
````

Copy the document contents, including its internal command fence, but not the tutorial's outer four-backtick fence. Save with Esc, then the editor command below, then Enter:

```text
:wq
```

Expected result: vi saves and exits. Read the saved file:

```bash
cat handover.md
```

Expected result: the faulty handover above. The report actually resides inside records. Your timed work will repair that mismatch and the unsupported health conclusion.

### 5. Start the assessment

Keep this task page visible. Close worked project solutions. Have a place to retain actual terminal output or screenshots privately.

Capture your start time:

```bash
date -Iseconds
```

Expected result: your current timestamp with a timezone offset. Record it. Start a 40-minute timer on your device now. Continue with the tasks below without following a supplied repair sequence.

## Timed tasks

### Task A, establish the actual environment, 10 minutes

Inspect the actual kernel name, distribution, architecture, installed Bash version, effective user context, working directory, and available space for the current workspace. Record when you made these observations.

You must obtain the values from the system during this attempt. Do not assume that an earlier baseline is still a complete description of the current state.

Observable checkpoint: you can show the relevant command results and distinguish the kernel name from the distribution identity.

### Task B, repair the report, 10 minutes

Update the existing report in records. Replace each missing observation with an accurate result. Correct all four unsupported previous-operator conclusions, giving an evidence-based explanation for each.

Include the scope of the filesystem-space check and at least two things the report does not establish. Preserve a brief record of what was wrong before you changed it. Save the report and verify its contents from the shell.

Observable checkpoint: the saved report agrees with actual system evidence and contains no unchecked fields or unsupported health claims.

### Task C, repair and test the handover, 10 minutes

Follow the original handover from the attempt directory to observe its file-location error. Retain the actual error, inspect your working directory, and identify where the report really exists. Do not create a duplicate report in the wrong location to make the bad instruction appear correct.

Repair the handover so an operator can reach and read the real report from the stated starting location. Explain the intended account, the starting point, the navigation steps, the successful result, and what to do if the file is still missing. Correct the unsupported application-health conclusion.

Leave the attempt directory. Follow your corrected handover from its stated starting point and read the report successfully.

Observable checkpoint: the same saved report can be located and read using your corrected instructions. The original error is explained by evidence, not hidden by a duplicate file.

### Task D, prove the result and hand it over, 10 minutes

Create an evidence file named evidence.md in the attempt directory. Include:

- Start and finish timestamps with timezone offsets, plus elapsed time.
- Relevant actual inspection outputs, with private account details redacted if sharing.
- The original file-location symptom and the working-directory observation that explained it.
- The repair you made and the actual successful read afterward.
- Proof that both edited documents were saved and readable from the shell.
- One remaining limitation or unresolved issue, if any.

Do not replace actual command results with an expected-output example. A self-authored sentence saying everything passed is not a substitute for the relevant observations.

Capture your finish time with the same timestamp command used at the start. Stop your timer. Keep unfinished work and report it honestly.

## Required results

| File within your attempt | Required content |
| --- | --- |
| records/environment-report.md | Actual environment observations, capture time, corrected conclusions, and clear limitations. |
| handover.md | Usable navigation to the original report, expected result, stop conditions, and accurate interpretation. |
| evidence.md | Your observed results, original error, diagnosis, verified recovery, and timing. |

Keep these files in your private assessment workspace. Public portfolio publication is separate from the timed assessment and requires a redaction review. Your earlier lab baseline and portfolio files must remain intact.

## Scoring rubric

Use this after stopping the timer. A reviewer must compare the files with actual terminal evidence rather than awarding marks for headings alone.

| Area | Marks | Evidence required |
| --- | --- | --- |
| Environment inspection | 25 | Kernel, distribution, architecture, Bash version, user context, directory, and filesystem-space observations agree with the actual run. Award 3 each for the first six and 7 for a correctly scoped space observation. |
| Report correction | 25 | Each of the four unsupported conclusions is corrected with a valid explanation, 5 each. The saved report includes an observation time and explicit limits, 5. |
| Incident diagnosis and handover | 30 | Actual original error retained, 5. Location-based diagnosis, 5. Correct instructions reach the original file, 10. Successful read after leaving and returning, 10. |
| Evidence and timing | 20 | Relevant actual outputs retained, 10. Start, finish, and elapsed time recorded honestly, 5. A final concise handover explains the result and limits, 5. |

Mandatory completion checks, regardless of score:

- Work used the intended regular account and stayed within the authorized lab scope.
- The original report remains inside records and is successfully read after the repair.
- The corrected handover works from its stated starting point.
- Results are genuine and the earlier lab and portfolio files are preserved.

Pass: at least 80 marks, all mandatory checks satisfied, and completed within 40 minutes. If correctness passes but the time is longer, record it as completed outside the time target and attempt a fresh timed run after practice. An interruption should be recorded as an interrupted attempt, not as an uninterrupted timed pass.

## Short debrief

After grading, explain these aloud or in your private notes:

1. Which observation changed your understanding of the environment?
2. Why did the original report read fail even though the report existed?
3. Which claim needed stronger evidence than a single successful command?
4. Which step would you improve on a retake?

Keep the attempt as evidence. No service or cloud resource was created, so no infrastructure teardown is required.

[Review the notes](../01%20Notes/README.md) · [Troubleshooting](../06%20Troubleshooting/README.md) · [Day 01](../README.md)
