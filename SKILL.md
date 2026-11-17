---
name: neverhash
description: "Use when an agent creates, edits, reviews, or organizes a software repository. Apply to READMEs, documentation, contributor instructions, PR descriptions, filenames, and proposed commits. Keep prose direct, documents self-contained, and committed files necessary and portable."
---

# Neverhash

## Purpose

Make a repository understandable to a reader who has never seen it. The reader should learn what the project does, how to use it, and where to find each important fact. Every sentence must help the reader understand, decide, or act.

This skill draws on the clarity and controlled wording of ASD-STE100. It is an independent writing and repository policy, not a claim of compliance with the official standard.

## Decision order

1. Preserve factual correctness, essential conditions, safety information, and explicit user requirements.
2. Communicate the main idea without interruption.
3. Remove low-value detail, repetition, and unnecessary files.
4. Prefer the smallest coherent change to the existing repository.

**Flow over incidental precision:** Keep the claims correct. Move secondary measurements, hashes, environment details, and provenance into the appropriate evidence record when readers do not need them to understand the main point. Never remove a detail that changes a conclusion or makes an instruction unusable.

## Write for the reader

- **Lead with intent.** Say what a component does, why an action matters, or what result the reader should expect. Give the central claim before its supporting detail.
- **Use short, direct sentences.** Prefer a named subject and an active verb. Put one main idea in each sentence. Reduce length only while clarity improves.
- **Keep paragraphs compact.** Group two to four related sentences when practical. Start a new paragraph when the subject changes. Avoid both walls of text and one-sentence-per-line formatting.
- **Make every sentence earn its place.** Keep it only if it states a fact, explains a decision, enables an action, or supplies a necessary condition. Delete filler, repeated claims, self-congratulation, and generic introductions.
- **Prefer affirmative statements.** State what the code does and what the evidence shows. Use a negative statement when a real limitation, prohibition, or distinction depends on it.
- **State uncertainty precisely.** Separate observed behavior, inference, and plans. Use a concrete scope such as "tested on Linux" instead of vague reassurance or defensive qualifications.
- **Avoid speculative detours.** State assumptions only when they change the answer. Treat hypotheticals as examples and label them clearly.
- **Use consistent terms.** Give each important concept one name within a document. Replace needless synonym rotation and abstract jargon with familiar, exact words.
- **Show a concrete case.** Use a small example to explain an unfamiliar process before adding general theory. Give exact commands and expected behavior when they help the reader act.
- **Separate different cases.** Give each condition its own explanation or compact comparison. Do not mix unrelated branches of behavior in a long sentence.

Write instructions in the order the reader will execute them. Use lists for procedures and parallel items, and prose for connected reasoning. Keep essential warnings close to the actions they govern.

## Give each document one job

Start with the existing repository. Read the relevant files and decide what each document already covers. Extend an appropriate document before creating a new one.

The README is the entry point: explain the project's purpose, its main capability, and the shortest useful way to start. A specialized document must answer a distinct reader question or serve a distinct audience. Give each topic one authoritative location.

Keep related information together. Split a document only when the new document has a clear independent purpose and materially improves navigation. Merge overlapping guides and remove copied sections. Avoid redirect chains and sections that merely say "see another file."

Use a link only when the destination adds necessary information. Say what the reader will find there and why it matters. Prefer a brief local explanation to an external link for information needed to understand the current document. Keep citations beside the claims they support.

Organize explanations around the reader's path: purpose, use, behavior, constraints, then verification. Omit sections that have nothing useful to say.

## Commit durable repository content

Commit source code, required configuration, portable scripts, maintainable tests, small test fixtures, and documentation that helps users or contributors. Include generated content only when it is an intentional, necessary project artifact.

Unless the user explicitly asks for them, exclude:

- Agent-specific directories such as `.claude/` and `.codex/`.
- Scripts that depend on one author's machine, private paths, or undocumented local state.
- Console output, temporary logs, caches, and one-off execution dumps.
- Large experimental datasets and intermediate results that the project does not need to build or test.
- Local machine specifications, environment snapshots, and execution histories that do not affect usage or reproducibility.

Keep provenance in Git history, commits, issues, or a designated research record. Put a benchmark's method and relevant conditions beside the benchmark when those details are necessary to interpret it. Do not fill the README with commit hashes, run identifiers, or incidental experimental details.

Choose descriptive, purpose-based filenames. Use `evaluation-method.md` or `data-format.md` rather than `notes-final.md`, `test-2.md`, or date-stamped filenames. Never add a date or timestamp to a new filename. Keep established filenames when changing them would break public interfaces or required tooling.

## Edit and review

1. Identify the intended reader, the document's single purpose, and the facts that must survive.
2. Inspect existing documentation and files. Choose one canonical home for each topic.
3. Write the main claim and reader action first. Add only the explanation needed to use or assess them.
4. Remove repeated, defensive, speculative, and off-topic sentences. Merge fragments that belong together.
5. Review every link, filename, script, dataset, and generated file proposed for commit.
6. Verify commands and claims where possible. State what was checked and what remains unverified.

Before finishing, ask: Can a newcomer understand the purpose? Does each section answer a real question? Does any sentence interrupt the narrative without changing the reader's understanding? Are necessary conditions accurate? Could the same information live in one document? Does every committed file have a durable purpose?

Report substantive changes and verification results directly. Do not add a long account of the editing process unless the user asks for one.

## Example

**Before:** "For additional information about the writing rules, please refer to [this page](SKILL.md). It should be noted that individual situations might require additional consideration."

**After:** "The [Neverhash policy](SKILL.md) defines writing, documentation, and commit rules."

The revised sentence gives the link a purpose and removes an undefined warning. State a real exception when it affects the reader's action.
