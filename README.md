# codebase-audit

A skill (best on Claude) for performing structured static audits of any codebase.

## What it does

Drop this skill into your coding agent setup and it will analyze an unfamiliar codebase the way a senior engineer would — starting with high-level structure and context, then drilling into specific problem areas — and produce a formatted HTML report.

The audit covers:

- **Architecture** — current structure, patterns, and a recommended target architecture with a migration path
- **Security hygiene** — hardcoded secrets, unsafe defaults, injection risks
- **Code quality** — god files, SRP violations, duplication, naming
- **Dependency health** — outdated or deprecated packages
- **Test & documentation consistency** — gaps in coverage and missing docstrings

## How it works

1. Agent reads your project's README, config files, and directory structure to establish context
2. It audits modules sequentially, respecting context window limits (large codebases are partially audited with a coverage note)
3. Findings are written to a structured `findings.json`
4. A bundled Python script renders `audit-report.html` in your project root

## Usage

Point coding agent at your repo and run:

```
/codebase-audit
```

Agent will infer project context from existing docs, ask only if something is genuinely ambiguous, and produce the report without further prompting.

## Output

`audit-report.html` — a self-contained report with severity-tagged findings (Confirmed / Likely / Uncertain), architecture notes, and prioritized recommendations.

## Requirements

- Python 3.x (for the report generation script)
