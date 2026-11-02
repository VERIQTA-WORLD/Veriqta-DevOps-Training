# Your lab environment

## Day 001 requirements

Use a personal Linux computer, disposable Linux VM, or Linux shell you are authorized to use. The first lesson uses Bash, vi, `/etc/os-release`, and the commands `uname`, `id`, `pwd`, `cat`, `mkdir`, `ls`, `df`, and `date`. GNU tools are the baseline; other implementations can print different formats.

No installation, administrator access, network connection, cloud account, or service deployment is required after you have a suitable environment. These commands use negligible disk space for a small text record. Later modules will state their own CPU, memory, storage, architecture, and cost requirements.

## Platform boundaries

| Environment | Day 001 guidance | Later considerations |
| --- | --- | --- |
| Personal Linux desktop or Linux VM | Follow the lesson as a regular user in Bash. | Verify distribution-specific packages and service manager before service labs. |
| WSL Linux distribution | Use the Linux distribution's terminal and home directory. | Service management, virtualization, networking, and container behavior need separate checks. |
| Disposable container | Many inspection commands work, but identity may default to root. | Filesystem, kernel, and process views are container-scoped. Not a substitute for all host labs. |
| Remote Linux training machine | Confirm permission and use a private practice directory. | Avoid exposing host details in public evidence. |
| macOS Terminal or Windows PowerShell | Do not use as the Linux lab shell. | Set up a suitable Linux environment first. |

Author validation is limited to individual command and file-persistence checks in a disposable Ubuntu 24.04.3 LTS container running as root, with Bash and GNU utilities. The live learner lab requires a regular user, so that full execution path remains unverified. See [lesson status](../PROGRESS.md). Other environments are documented routes, not claims of successful testing.

## Before system changes

Day 001 performs read-only inspection and creates files under your home directory. If `id -u` returns `0`, pause and switch to an existing regular lab user. Do not create accounts or change permissions on a shared computer just to get past the checkpoint.

If a required tool is missing, record the exact error and distribution. Do not install random packages or run a remote installation script. Your instructor can provide a reviewed, distribution-specific setup step.

## Course files and your output

Keep the repository checkout and `$HOME/veriqta-devops-labs/` separate. Raw output can contain usernames, internal paths, software versions, and filesystem information. Review it before sharing. Never use real business or customer data in exercises.

When cloud work begins, each lab will name the billable resources, region assumptions, estimated cost basis, cleanup steps, and remaining-resource checks. Budget notifications are useful but do not guarantee a spending cap.

[Start here](../START-HERE.md)
