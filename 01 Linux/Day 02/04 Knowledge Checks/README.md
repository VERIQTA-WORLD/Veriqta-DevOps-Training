# Day 02 knowledge checks

Predict the result before reading the explanation. You may look up syntax after making your prediction. For practical questions, verify in your disposable Day 02 workspace, not in another system's files.

![Location, operation, and verification form separate reasoning checks.](../07%20Images/checks.svg)

Text equivalent: identify the current directory, predict the selected source and destination, perform a bounded operation, then explain the actual verification result.

## Questions

1. You are in the project root. A file exists in config, but reading its bare filename fails. Does the error prove the file was deleted?
2. A command uses a quoted path containing a space. Why must that remain one argument?
3. A normal directory listing does not show .lab-only. What kind of listing is needed, and does the leading dot protect its contents?
4. You create a file with the timestamp utility. If it already exists, is its content guaranteed to be emptied?
5. You copy a source file to a new destination. Which names should exist afterward? What changes when you move it instead?
6. An interactive copy asks about overwriting an existing destination. What must you inspect before answering?
7. Why is listing two filenames not enough to prove equal content?
8. A byte comparison prints nothing. Which immediate check distinguishes equality from an unexamined assumption?
9. The comparison status is one after the deliberate v002 change. What does that mean? How is a value greater than one different?
10. Why must you establish whether a destination directory exists before a recursive directory copy?
11. An empty-directory removal fails because hidden contents remain. Should you immediately use a recursive deletion command?
12. You restored v001 and verified equal bytes. What remains unproven about the application and the backup strategy?
13. Why are empty local directories missing from a GitHub repository even though the files were published correctly?
14. Your Day 01 and Day 02 folders both have baselines or records. What should determine which one an operator reads?

<details>
<summary>Explained answers</summary>

1. No. The bare name is interpreted from the current directory. Inspect location and the intended child path before concluding that the file is missing.
2. Without grouping, the shell can treat parts as separate arguments. Quoting preserves the intended pathname as one argument.
3. Include hidden entries. A leading dot is a naming convention, not encryption or permission enforcement.
4. No. It creates an empty file only if absent. For an existing file it updates timestamps without emptying its contents.
5. A copy retains the source and adds a destination. A successful move removes the old source name and makes the content available through the destination name.
6. Inspect the current directory, both file paths, existing destination content, and whether a verified recovery source exists. An unexpected prompt is a checkpoint to stop and investigate.
7. Names and sizes are metadata. Different files can have equal sizes, and a filename does not identify a specific content version.
8. Read the exit status immediately after the comparison. Zero means equal for this utility. Do not run another command first.
9. One means content differs. A higher value means comparison trouble, such as an unreadable or missing input. Do not call either state a successful equality check.
10. Copying a directory into an existing directory can create an extra nested level. Rerunning the same command can therefore produce a different layout from the first run.
11. No. Inspect the directory, including hidden entries, and decide whether its contents are approved for removal. Do not destroy unknown files to make a command succeed.
12. Equal file content does not prove service health, metadata equality, durable independent backups, or successful database recovery.
13. Git tracks files rather than empty directories alone. Document the local roles or add purposeful files when needed; do not invent runtime logs to fill a directory.
14. Use the task's explicit starting point, tool, day, and project path. A familiar filename alone is insufficient.

</details>

## Practical recall

Without copying the lab, explain how you would preserve one file, change the active copy, prove the intended difference, and restore it. Then name the evidence required to demonstrate success. If one distinction is unclear, revisit that specific note and repeat a small check.

[Practical Assessment](../05%20Practical%20Assessment/README.md) · [Day 02](../README.md)
