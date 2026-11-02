# Day 01 troubleshooting

![Troubleshooting without guessing](../07%20Images/troubleshooting.svg)

Text equivalent: Preserve the symptom, check relevant context, choose a bounded fix, and verify the result. Stop when evidence is insufficient.

Preserve the exact command and error before changing anything. A difference in wording or a version number is not automatically a failure.

| Symptom | What to inspect | Safe next action | Recovery check |
| --- | --- | --- | --- |
| `uname -s` does not show Linux, or the command is unrecognized. | Confirm which terminal and operating system you opened. | Use the Linux lab terminal. If none exists, arrange the environment first. | Run the kernel check again in the intended environment. |
| `id -u` shows zero. | You are operating with root identity in this context. | Pause and switch to an existing authorized regular lab account. Do not create users or alter shared permissions blindly. | Confirm a nonzero ID before continuing. |
| Bash is unavailable. | Exact error and distribution. | Stop and request a reviewed environment setup. Do not use a remote install script. | Confirm Bash availability and start it. |
| `/etc/os-release` is missing. | Exact path, spelling, and environment type. | Record that the distribution could not be established. Some minimal environments differ. Request an environment-specific check. | Establish distribution evidence before choosing distribution-specific instructions. |
| `mkdir` reports permission denied. | The exact path and whether your home directory is writable. | Stop. Check you used the quoted home path and the correct account. Do not add sudo or use broad permission changes. | Create the intended private workspace with your regular account. |
| `cd` says no such file or directory. | Spelling, capitalization, quotes, and whether directory creation succeeded. | Repeat the workspace creation step only after understanding any earlier error. | `pwd` matches your expected workspace. |
| Your workspace was already present. | Existing files and their purpose. | Reuse the directory carefully and preserve old evidence. Choose a new filename for a separate attempt. | Both original evidence and the new attempt remain identifiable. |
| `df` prints different filesystem names or units. | The row containing the current directory, its columns, and the tool implementation. | Read the meaning of the result rather than copying an example value. | Record the actual available-space value and its scope. |
| You cannot type normally in vi. | You may be in normal mode. | Press Esc, then i, before entering text. | Text appears in the document as intended. |
| vi reports a swap file or another editor session. | Whether the file is open elsewhere or an earlier session ended unexpectedly. | Stop and inspect the warning. Do not delete recovery files or edit concurrently without understanding the situation. | One intended editor session owns the file and saved content is verified. |
| vi cannot write the file. | Exact error, current directory, disk space, and ownership context. | Keep your buffer open while investigating. Do not quit and lose unsaved work. Do not solve it with broad chmod. | Save succeeds and cat shows the intended content. |
| `cat baseline.md` cannot find the file. | Your current location and the exact filename used in vi. | Return to the verified workspace. Check whether you used a retry filename. If nothing was saved, recreate only after confirming that fact. | Read the intended saved file successfully. |
| Placeholder text remains. | The actual saved contents, not what you remember typing. | Replace placeholders with observed values and truthful limitations. | Read the file again and compare it with evidence. |

## If you are still blocked

Record your last successful step, the next command, the exact error, and the environment. Share only the relevant redacted lines. Do not paste a complete system inventory into a public issue.

If a step fails, do not continue to dependent steps and label the day complete. You can pause and resume from the specific unresolved checkpoint.

[Guided lab](../02%20Follow%20Along%20Lab/README.md) · [Lesson overview](../README.md)
