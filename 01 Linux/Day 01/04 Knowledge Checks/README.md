# Day 01 knowledge checks

![Prediction, evidence, and explanation](../07%20Images/knowledge-checks.svg)

Text equivalent: Predict the result, compare actual evidence, then explain what it establishes. Read the answers after attempting the questions.

Try these before reading the answers. You may use the command reference to confirm syntax after making a prediction.

1. `uname -s` prints `Linux`. Does that prove your distribution is Ubuntu? Explain what you still need to inspect.
2. Your prompt ends with `$`, but `id -u` prints `0`. Which evidence determines whether to pause?
3. You create a directory and receive no output. What separate check would establish where you are working before writing a file?
4. What does `.` select in `df -h .`? Does that report every disk's free space?
5. Why are there double quotes around `"$HOME/veriqta-devops-labs/linux/day-01"`?
6. You see text inside vi and close the terminal without saving. Is a file on disk guaranteed to contain those edits?
7. You reopen the baseline successfully. What does that prove, and what does it not prove about an application?
8. Why should a baseline include its capture time and timezone offset?

<details>
<summary>Read the explained answers after attempting the questions</summary>

1. No. The kernel name does not identify the distribution. Inspect `/etc/os-release`, especially its distribution fields.
2. The numeric ID. Zero indicates root in the current context. Prompts are customizable. Pause and use an authorized regular lab account.
3. Change to the intended workspace and run `pwd`. Check the resulting absolute path. Later, verify the file and its contents separately.
4. The filesystem containing the current directory. It does not enumerate or fully assess every disk.
5. Bash expands `$HOME` while preserving the resulting path as one argument, including any spaces. The quotes are shell syntax rather than part of the path.
6. No. Unsaved editor content may not be written to the intended file. Save deliberately, then read the file from the shell.
7. It proves the saved content was readable at that path at the time of the check. It does not prove application health, security, or permanent durability if the environment is deleted.
8. You need to know when the observations were made and relate them to other events. Without an offset or timezone, timestamps from different places can be ambiguous.

</details>

If an answer was uncertain, revisit that explanation and repeat the related small check. You do not need to repeat the whole lesson.

[Independent assessment](../05%20Practical%20Assessment/README.md) · [Lesson overview](../README.md)
