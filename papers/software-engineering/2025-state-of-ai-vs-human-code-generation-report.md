---
title: "State of AI vs Human Code Generation Report"
summary: "Analysis of 470 open-source GitHub PRs (320 AI-co-authored, 150 human-only) finding that AI-generated PRs contain ~1.7x more issues overall, with readability problems 3x higher, security issues up to 2.74x higher, and performance regressions (excessive I/O) up to 8x more common."
year: 2025
link: "https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report"
subjects: ["software-engineering", "ai"]
tags: ["ai-generated-code", "code-quality", "pull-requests", "security", "code-review"]
---

## Why I saved this

- Provides concrete, category-level data on where AI-generated code fails compared to human code, useful for calibrating expectations and designing review processes.

## Key points

- AI-authored PRs produced 10.83 issues per PR vs. 6.45 for human-only — a 1.7x increase overall, with high-issue outliers much more common in AI PRs.
- Readability was the single biggest gap: 3x more issues. AI code looks superficially consistent but violates local naming, clarity, and structural patterns.
- Security issues were up to 2.74x higher — improper password handling and insecure object references were the most prominent patterns. No vulnerability type was unique to AI, but nearly all were amplified.
- Logic and correctness errors were 75% more common, including business logic mistakes, flawed control flow, and misconfigurations — the most expensive category to fix post-deployment.
- Error handling gaps were nearly 2x more common: missing null checks, early returns, guardrails, and exception paths tightly tied to real-world outages.
- Performance regressions skewed heavily toward AI — excessive I/O operations were ~8x more common, reflecting AI's tendency to favor simple, clear patterns over resource efficiency.
- No issue category was unique to AI. Humans and AI make the same kinds of mistakes; AI just makes most of them more often and at larger scale.

## Notes

- The methodology has an important limitation: AI authorship was inferred from signals in the PR, not confirmed directly. Some "human-only" PRs may have had undisclosed AI assistance, which would understate the true gap.
- Directly supports the comprehension debt article (Osmani, 2026) in this vault — AI generates syntactically clean code that passes surface-level review, while the real problems (logic, error handling, security) require deep understanding to catch.
- The METR developer productivity paper (2025) in this vault found developers accept less than 44% of AI generations and spend significant time cleaning up accepted code — this report quantifies what goes wrong with the code that does get accepted.
- The 3x readability spike is counterintuitive — AI should excel at consistent formatting. The explanation is that AI follows generic defaults rather than repo-specific idioms, exactly the "implicit repository context" factor identified in the METR study.
- The article is commercially oriented (CodeRabbit is an AI code review product), but the statistical methodology (rate ratios normalized to issues per 100 PRs) is sound and the dataset is drawn from real open-source projects.
- Complements the maintenance cost article (2025, idealink.tech) in this vault: if AI-generated code enters production with 1.7x more issues, the corrective maintenance fraction (20-30% of lifetime cost) will increase proportionally.
