# Teaching and publication standard

## The way you are taught

Every lesson addresses you directly. It gives you enough context to understand the task, complete it independently, and evaluate the result. Examples remain small enough to explain, and practice advances from guided work to independent decisions.

You use practical analogies with clearly stated limits. You learn why commands and configurations work, what their important arguments mean, and how to interpret output. You can consult documentation during practical work.

Live instruction uses one actionable step followed by evidence review. A complete public lab remains available for independent study. Small scripts are supplied as coherent files, explained, and edited with vi by default.

## Daily files

| File or directory | Its job |
| --- | --- |
| README.md | Scenario, prerequisites, outcomes, learning order, and navigation. |
| notes.md | Concepts, examples, and command reference. |
| lab.md | Guided steps, expected patterns, verification, resumption, and cleanup. |
| project.md | Contribution to the ongoing project and a small independent variation. |
| knowledge-checks.md | Recall, prediction, reasoning, and explained answers. |
| assessment.md | Independent task and observable pass criteria. |
| troubleshooting.md | Symptoms, diagnostic evidence, safe fixes, and recovery checks. |
| evidence/README.md | What to retain, what to redact, and how to label evidence. |
| images/ | Accurate explanatory visuals, accompanied by text equivalents. |
| code/ or manifests/ | Runnable files only when needed. |

Images of actual terminal results must come from actual runs. Teaching diagrams must be labeled as diagrams. Commands, outputs, and the text explanation remain usable without images. Raster publication images use 1080 by 1350 portrait, Arial, small titles, and the unchanged supplied official logo. Do not redraw an unavailable logo. Exact diagrams can use SVG.

## Before a lesson is published

- Confirm its outcome and prerequisite lesson.
- Check current official documentation for the behavior being taught.
- Run the relevant commands or tests in an isolated environment where possible.
- Report what was tested and what remains unverified.
- Check relative links, image rendering, code syntax, placeholders, and cleanup.
- Review public files for secrets and private information.
- Update the canonical [lesson index](../PROGRESS.md).

Published material, author testing, and learner completion are different statuses. Never imply learner completion from author testing. Fix a failed checkpoint before teaching dependent work.

## Continuity and numbering

Use global day numbers and module-local week numbers. Do not publish empty lesson folders or dead links to planned lessons. The [session record](../templates/session-record.md) stores private learner continuity. The public course index stores material availability.

## Progression and judgment

Keep one evolving project. Add small supporting exercises as needed. Teach security, reliability, testing, costs, recovery, and technical communication throughout. Later exercises require decisions with evidence, including architecture tradeoffs, rollout plans, incident analysis, SLOs, and restore tests.

Do not promise equivalent years of experience or guaranteed outcomes. Do not make claims that missing a day destroys knowledge. Resume with a short recall and verification task.

[Course home](../README.md)
