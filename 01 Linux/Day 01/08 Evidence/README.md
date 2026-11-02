# Day 01 evidence

![Honest evidence and safe sharing](../07%20Images/evidence.svg)

Text equivalent: Retain actual output privately, distinguish expected examples from observations, and redact sensitive details before sharing.

Keep your raw evidence privately under your own lab workspace. This directory contains the shared checklist, not another learner's output.

## Retain these results

- Kernel, distribution, architecture, and numeric identity checks.
- Bash version and the verified workspace path.
- The relevant filesystem-space result and timestamp.
- Your saved `baseline.md`, including your observation and limitation.
- Proof that you read the baseline after leaving and returning.
- Your saved independent assessment.
- Your two project deliverables, the updated baseline and environment handover, with verification results.
- Any error you encountered and the evidence that it was resolved.

Text output is useful because it is searchable. Screenshots can show context, but must come from your actual run. Do not manufacture output to resemble an example.

## Label evidence honestly

An expected-output example explains a pattern. An author test describes a specific environment used to check the material. Learner evidence describes your own run. These are three different things.

The command and file-persistence checks for this lesson used an isolated Ubuntu 24.04.3 LTS container running as root, with Bash and GNU utilities. vi saving was checked in noninteractive Ex mode. These checks do not cover the complete regular-user lab, interactive editing, WSL, or other distributions. Verify your own environment and results against the task criteria.

## Before sharing

Review usernames, absolute home paths, filesystem labels, internal host details, and any accidental secrets. Replace sensitive values with explicit labels such as `[redacted username]`; do not replace a failed result with a successful one. Retain the original privately if you need it for diagnosis.

When asking for help, share the relevant redacted output and the exact step. Public portfolio evidence should use reviewed, sanitized material.

[Lesson overview](../README.md)
