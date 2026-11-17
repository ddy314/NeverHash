---
name: neverhash
description: "Use when organizing repositories, writing technical documentation, or submitting changes."
---

# NeverHash — Repository and Documentation Rules

Apply these rules whenever organizing a repository, writing or editing documentation, adding tests or workflows, or preparing commits and pull requests.

## 1. Writing

### 1.1 Fluency Over Accuracy

**Fluency > Accuracy.**

When local precision impedes reading flow, prioritize a clear narrative. Summarize complex conditions, merge related facts, and omit secondary parameters from overview prose. You may sacrifice minor local precision to keep the explanation smooth.

State the conclusion the reader needs first, then introduce the necessary method and evidence. Do not interrupt body paragraphs with every parameter, edge case, or caveat. Complete proofs, exact protocols, and reproducibility parameters belong in their dedicated technical sections; overview prose communicates their meaning.

**Poor**

> Under a specific compiler version, selected benchmark inputs, and several build flag combinations, the optimized binary exhibited varying execution-time reductions across input sizes.

**Good**

> The optimized binary runs faster across the benchmark suite. The speedup scales with input size.

Every sentence must help the reader understand a fact, make a decision, or run a command. Delete empty praise, self-congratulation, repeated conclusions, irrelevant background, notes on where an idea was borrowed from, and commentary on the author's own writing process.

### 1.2 Sentences and Paragraphs

Prefer short sentences with a clear subject and active verb. Each sentence expresses one main idea; each paragraph develops one topic across a few closely related sentences. Avoid multi-clause run-on sentences, wall-of-text pages, and fragmented single-sentence paragraphs.

**Poor**

> Because the parsing stage must identify lexical tokens while simultaneously determining whether they form valid expression structures, the system invokes separate components during execution to handle these tasks.

**Good**

> The lexer converts input text into tokens. The parser combines those tokens into an expression tree.

Use lists for sequential steps, independent options, or parallel rules. Use prose paragraphs for continuous explanation rather than slicing a coherent argument into isolated bullet points.

### 1.3 Direct and Affirmative Language

State behavior, purpose, facts, and conclusions in positive terms. When defining scope or assumptions, state the supported conditions, dataset, and operating domain directly. Distinguish observed results, derivations, and future plans; do not state speculation as fact or enumerate every theoretical exception.

**Never use defensive disclaimers or negation-driven rhetoric in documentation, comments, UI copy, commit messages, or pull-request descriptions.** Evaluate intent rather than exact wording alone; when a passage matches any pattern below, rewrite it as a direct affirmative statement (preserving programming keywords, public API identifiers, formal mathematical propositions, and verbatim quotations):

| Pattern | Forbidden Forms (Poor) | Affirmative Rewrite (Good) |
| --- | --- | --- |
| Scope & identity denial | `This is not …`, `This does not prove / imply / constitute …`, `should not be interpreted as …`<br>*Ex:* `This is anomaly detection, not fault-ID classification.` | Define what the component actually does.<br>*Ex:* `The monitor detects anomalies in process streams.` |
| Negation-driven contrast | `not X, but Y`, `rather than`, `instead of`, `not only … but also …`<br>*Ex:* `Contribution scores represent residual weights, not physical root causes.` | Drop the negated half and state the positive meaning.<br>*Ex:* `Contribution scores measure each variable's statistical residual weight.` |
| Guarantee & hedge disclaimer | `does not guarantee`, `no generalization guarantee`, `may or may not`, `preliminary only`, `for illustration only`<br>*Ex:* `Empirical calibration does not guarantee a target false-alarm rate.` | State the calibration split and measured evaluation protocol.<br>*Ex:* `Thresholds are calibrated on the training split and evaluated on held-out test runs.` |
| Credential & maturity disclaimer | `not production-ready`, `not safety-certified`, `not real plant data`, `not a confidence interval`<br>*Ex:* `These are not real plant measurements and this tool is not safety-certified.` | Name the actual operating environment and supported workflow.<br>*Ex:* `The system runs offline incident analysis on TEP simulation data.` |
| Scope laundering & unfinished work | `this change only …`, `outside the current scope`, `has not been uploaded / verified yet`, `left for future work`<br>*Ex:* `The MP4 has not been uploaded to YouTube or submitted yet.` | Describe only what is currently delivered and how to use it.<br>*Ex:* `The build script exports the demonstration video to video/.` |
| Empty meta-commentary | `it is worth noting that`, `it is important to note`, `to avoid confusion`, `for the avoidance of doubt`, `obviously`<br>*Ex:* `It is worth noting that, to avoid confusion, this algorithm is not globally optimal.` | Delete the throat-clearing lead-in and state the finding.<br>*Ex:* `The algorithm achieves the lowest error on the evaluated test set.` |

### 1.4 Don't Repeat Yourself (DRY)

State each fact, rule, definition, or conclusion once:

- **One form per point**: Explain an idea using a paragraph, a list, or a table—never a list followed immediately by a table or summary repeating the same items.
- **No split short/long inventories**: Maintain one complete specification in its authoritative place rather than keeping a partial list in one file and an expanded list in another.
- **One name and symbol per concept**: Define each concept, mathematical symbol, metric, or data structure once across the repository and reuse that exact name and notation everywhere. Never re-introduce the same or nearly identical concept under a new name in another section or file.
- **Shared premises stated once**: Define shared assumptions and experimental conditions at their first appearance instead of repeating caveats at the end of every section.
- **Single working language**: Use one canonical human language across a project's documentation, comments, commit messages, and pull requests. Do not mix languages in prose or repeat the same sentence bilingually.

### 1.5 Show a Concrete Example

When explaining a complex mechanism or invariant, show a brief, concrete instance before stating the general rule. Keep only the details needed for that mechanism.

For example, to explain how an incremental parser preserves downstream cache hits after a local edit, show the node span intervals before and after editing one paragraph:

~~~text
Before edit:
Document [100..500]
├── Heading("Intro") [150]
├── Paragraph("Old text") [220..260]
└── Paragraph("Unchanged") [380..420]

After editing the first paragraph:
Document [100..500]
├── Heading("Intro") [150]
├── Paragraph("Updated longer text") [220..290]
└── Paragraph("Unchanged") [380..420]
~~~

The reader immediately sees that renumbering is confined to `[220..290]` while `[380..420]` stays fixed, keeping span-keyed memoization caches valid.

## 2. Documents

### 2.1 One Purpose, One Place

Each topic has one authoritative location, and each document serves a distinct reading task. Improve existing files first; create a new document only when the target audience, purpose, or required depth is genuinely distinct.

`README.md` introduces the project's purpose, capabilities, and entry points. Architecture documentation explains system structure and data flow. API references specify interfaces. Research papers present the problem, method, theorems, and evidence.

**Poor**

~~~text
docs/
├── introduction.md
├── background.md
├── overview.md
├── project-summary.md
└── design-overview.md
~~~

When multiple files restate the same project goals and design, merge them into one document.

### 2.2 Self-Contained Without Duplication

Each document should complete its own reading task without copying entire sections from other files. When a trade-off arises, **keep the minimal context needed to understand the current document, then eliminate cross-document duplication.** Do not copy full rule sets or proofs into `README.md`, and do not strip core explanations down to bare links.

### 2.3 Natural Reading Order

Organize sections according to how a reader builds understanding:

- **Project overview (`README.md`)**: Purpose → capabilities → installation and usage → repository map.
- **Architecture guide (`docs/dev/architecture.md`)**: Top-level directory responsibilities → end-to-end processing pipeline (e.g., `Parsing → Evaluation → Layout → Export`), mapping each stage to its data structures and module location.
- **Research note or paper**: Problem and main finding → methodology and formal model → empirical or formal evidence.

Choose sections based on actual content rather than filling out boilerplate templates with empty headings.

### 2.4 Purposeful Links

Links provide primary sources, necessary background, or deeper specifications. Name the target and state what information it contains.

**Poor**

> See [here](https://example.com) for more details.

**Good**

> The [API Reference](https://example.com) lists request parameters, return types, and error codes.

## 3. Repository Structure

### 3.1 Scale Horizontally with a Flat Root

Keep the repository root small regardless of project size: include only entry documents (`README.md`, `LICENSE`), workspace build configuration, and a few top-level responsibility directories (`crates/` or `packages/`, `docs/`, `tests/`, `tools/`). Never dump new modules, stage reports, or ad-hoc scripts into the root directory.

As a codebase grows, **split subsystems horizontally by processing stage or domain** inside the package directory rather than nesting deep abstraction layers (`src/core/internal/engine/`):

- **Separate the core library from thin frontends**: Keep the main pipeline in the core package and place CLI or IDE adapters in sibling packages.
- **Flat-first module internals**: Keep single-file modules flat inside each package (`ast.rs`, `lexer.rs`, `parser.rs`, `span.rs`). Create a one-level subdirectory (`flow/`, `grid/`, `math/`) only when a sub-domain contains multiple closely collaborating files.

**Good: Horizontal subsystem scaling**

~~~text
compiler/
├── Cargo.toml
├── README.md
├── crates/
│   ├── compiler/          # Core pipeline orchestration
│   ├── compiler-cli/      # Thin CLI frontend
│   ├── compiler-syntax/   # Flat single-file modules: ast, lexer, parser, span
│   ├── compiler-eval/     # Interpreter and scope evaluation
│   ├── compiler-layout/   # Flat primitives + 1-level subdirs (flow/, grid/, math/)
│   └── compiler-pdf/      # PDF export backend
├── docs/
│   ├── dev/architecture.md
│   └── reference/
├── tests/
│   ├── ref/               # Reference fixtures
│   ├── src/               # Test harness
│   └── suite/             # Domain-grouped suites: syntax/, eval/, layout/, math/
└── tools/
~~~

**Poor: Root sprawl and deep vertical nesting**

~~~text
compiler/
├── README.md
├── ARCHITECTURE_V2.md
├── stage1_summary.md
├── pdf_export_new/
├── src/core/internal/engine/
│   ├── 01_tokenize.rs
│   ├── 02_parse_new.rs
│   └── parser_final.rs
└── scripts/
    ├── smoke_test_2026.py
    └── verify_hashes.py
~~~

In research and benchmark repositories, apply the same horizontal rule: add new baseline algorithms or datasets as sibling modules under `benchmarks/methods/` or `benchmarks/datasets/` driven by a single runner, rather than creating dated validation docs or parallel benchmark folders for each experiment round.

### 3.2 Align Tests with Domain Boundaries

Organize test suites by system capability (`tests/suite/syntax/`, `tests/suite/layout/`, `tests/suite/math/`) mirroring the domain model, and separate the test runner (`tests/src/`) from reference outputs (`tests/ref/`). Do not organize tests by development phase, PR batch, or ad-hoc smoke-test scripts.

### 3.3 Semantic Names

Directory, package, and file names must describe responsibility or domain concepts and remain stable over time. Avoid phase or version markers (`new`, `old`, `latest`, `final`, `v2`), arbitrary numeric prefixes or suffixes (`01_`, `02_`, `test2`), and dates or timestamps.

| Poor | Good | Reason |
| --- | --- | --- |
| `compiler_v2/` | `compiler-layout/` | Names the subsystem responsibility |
| `02_parser_final.rs` | `reparser.rs` | Distinguishes incremental reparsing from full parsing |
| `test2.py` | `tests/suite/syntax/` | Groups tests by target capability |
| `results_final.md` | `docs/dev/architecture.md` | Identifies audience and topic |
| `run_2026_11_17.csv` | `validation_samples.csv` | Keeps filenames independent of run dates |
| `misc/` | `compiler-utils/` | States the shared utility boundary |

Modification history belongs in Git. Preserve standard filenames required by build tools, language ecosystems, and public interfaces.

## 4. Technical Detail and Evidence

### 4.1 State the Finding First

Research and experimental documentation must state findings first, followed by the methodology needed to evaluate them. Do not narrate experiments as a chronological execution diary of commands, flag tweaks, and logs.

**Poor**

> We first ran the program, then adjusted thread counts, tested multiple input dimensions, recorded wall-clock times, and compared PSNR and SSIM values.

**Good**

> SIMD vectorization accelerates image dehazing while preserving output quality across PSNR and SSIM benchmarks.

### 4.2 Keep Provenance in Its Place

Git history records version changes and merge topology; Issues and PRs record discussions; test suites encode executable expectations. Long-term documentation describes only the currently valid design, methods, and results.

Do not clutter documentation with commit hashes, run IDs, local environment snapshots, debugging histories, or defensive Git self-attestations (such as "no history was rewritten," "no existing files were overwritten," or "no other PRs were merged during this work"). Keep reproducibility parameters inside their formal benchmark or proof specifications.

## 5. Changes and Delivery

### 5.1 Keep Durable Content

Commit source code, build configurations, meaningful tests, portable scripts, and durable documentation. Large datasets belong in external storage accompanied by retrieval instructions.

**Unless explicitly requested by the user, never commit** agent-specific directories (`.codex/`, `.claude/`), one-off prompts, personal workspace state, scripts with hardcoded machine paths, console dumps, caches, temporary reports, or regenerated output snapshots. Scripts and tools must accept paths via arguments, configuration, or workspace-relative defaults.

### 5.2 Add CI/CD Only for a Real Need

**Never add or expand CI/CD workflows without an explicit user request or a recurring integration need.** Every workflow adds maintenance cost and runner overhead. Local edits, documentation updates, and small research changes should use existing tests and local verification rather than spawning multiple `.github/workflows/*.yml` files (`audit.yml`, `docs.yml`, `lint.yml`, `validate.yml`).

### 5.3 Always Submit Changes Through a Pull Request

**All repository changes must be committed on an isolated branch and submitted through a Pull Request. Never push directly to `main`, `master`, or the default branch.**

Follow this sequence for every task:

1. Inspect repository status and existing PRs to confirm the scope.
2. Create or switch to a dedicated working branch.
3. Keep each commit and PR focused on one coherent goal.
4. Open a PR (or update the existing PR for the same task) summarizing what changed, what capability is affected, and how it was verified.
5. Hand the PR to the user for review and merge.

### 5.4 Verification Serves the Result

Scale verification to the actual impact of the change: check links and prose for documentation edits, run relevant unit tests for local code fixes, and run deeper benchmarks or formal checks for core algorithm or interface changes.

**Deliver the finished result and remove all process scaffolding.** Unless explicitly requested by the user, never create standalone audit reports (`AUDIT_REPORT.md`, `VERIFICATION_SUMMARY.md`), stage validation checklists, smoke-test receipts, or file-hash inventories (such as "all 2,482 file hashes remain unchanged"). When verification reveals an issue, fix the code, test, or primary documentation directly.
