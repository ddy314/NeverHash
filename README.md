# NeverHash

NeverHash is a skill for AI agents that governs how repositories are organized, how technical documentation is written, and how changes are delivered.

AI agents often generate overlapping notes, one-off scripts, dated reports, and defensive disclaimers for simple tasks. This clutter obscures working results and increases maintenance cost. NeverHash requires every document to serve a distinct reader task and every file to earn its permanent place.

## What Changes

Without discipline, a research or engineering repository accumulates process artifacts alongside actual work:

~~~text
study/
├── README.md
├── project-overview.md
├── results-final-v2.md
├── audit-report.md
├── experiment-2026-11-17.py
├── run-output.txt
└── paper/
~~~

With NeverHash, the repository is organized around durable results and responsibilities:

~~~text
study/
├── README.md
├── pyproject.toml
├── paper/
├── proofs/
├── benchmarks/
└── tests/
~~~

The `README.md` states the problem, core findings, and entry points. The paper, formal proofs, benchmark runner, and tests each have a single home. Transient run logs stay out of version control, and overlapping summaries are merged or deleted.

NeverHash enforces **Fluency > Accuracy** as its primary writing rule: lead with clear conclusions and affirmative statements rather than burying meaning under defensive qualifiers.

## Usage

Install with an Agent Skills client:

~~~bash
npx skills add ddy314/NeverHash
~~~

Or instruct the agent directly:

> Apply NeverHash to this repository. Make the README useful to a new reader, consolidate overlapping documentation, enforce semantic filenames, and submit the changes through a pull request.

See [SKILL.md](SKILL.md) for the complete rules, examples, and pull-request workflow.

## License

[MIT](LICENSE)
