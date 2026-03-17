---
title: "Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity"
summary: "RCT with 16 experienced open-source developers completing 246 real tasks finds that AI tools (primarily Cursor Pro with Claude 3.5/3.7 Sonnet) actually increase completion time by 19% — contradicting developer forecasts of 24% speedup and expert predictions of ~39% speedup. The slowdown is robust across estimators, subsets, and outcome measures."
year: 2025
link: "https://arxiv.org/pdf/2507.09089"
subjects: ["software-engineering", "ai"]
tags: ["developer-productivity", "rct", "ai-assisted-coding", "cursor", "open-source", "metr"]
---

## Why I saved this

- The most methodologically rigorous field experiment on AI coding productivity to date, with a surprising result that directly contradicts lab studies and expert consensus.

## Key points

- AI tools increased task completion time by 19% for experienced developers on mature codebases — developers were slower with AI, not faster.
- Developers forecasted 24% speedup before the study; after completing it, they still estimated 20% speedup. They could not perceive their own slowdown even in retrospect.
- Expert forecasts were even more wrong: economics experts predicted 39% speedup, ML experts predicted 38%. The gap between perceived and actual AI impact is enormous.
- Five factors contributed to slowdown: developer over-optimism about AI usefulness, high developer familiarity with repositories (avg 5 years, 1,500 commits), large/complex codebases (avg 1.1M LoC), low AI reliability (<44% of generations accepted), and implicit repository context that AI cannot access.
- Screen recording analysis shows AI-assisted developers spend less time actively coding and reading, replacing it with prompting, waiting on, and reviewing AI outputs — plus more idle time.
- 75% of developers experienced slowdown. 69% continued using Cursor after the study ended, suggesting they derive perceived value despite measurable productivity loss.

## Methodology

- 16 developers with an average of 5 years experience on their target repositories completed 246 tasks on real open-source projects (avg 23,000 GitHub stars, 1.1M LoC).
- Each task randomly assigned to AI-allowed or AI-disallowed. AI-allowed developers primarily used Cursor Pro with Claude 3.5/3.7 Sonnet; AI-disallowed developers could not use any generative AI.
- Tasks were real issues (bug fixes, features) defined before randomization, with developer time forecasts collected pre-randomization as a difficulty proxy.
- Outcome measure: self-reported implementation time (validated against 143 hours of manually labeled screen recordings showing 25% slowdown, consistent with 19% from self-reports).
- Effect estimated via log-linear regression with AI-disallowed forecast as covariate; robust to ratio estimators, alternative covariates, developer fixed effects, and alternative imputation methods.
- 21 potential contributing factors analyzed via screen recordings, exit interviews, subset analyses, and Cursor analytics data.

## Notes

- Directly contradicts the Anthropic productivity estimates paper (2025) in this vault, which reports ~80% time savings from Claude conversations. The key reconciliation: this study measures experienced developers on familiar, complex codebases, while the Anthropic study measures self-selected tasks where users already expect AI to help. Both can be true simultaneously.
- Strongly reinforces the skill formation paper (Shen & Tamkin, 2026) in this vault: if AI doesn't even speed up experienced developers on familiar codebases, and simultaneously impairs learning on unfamiliar ones, the case for cautious AI adoption in engineering workflows is even stronger.
- The "conceptual inquiry" interaction pattern from the skill formation study maps onto this paper's finding that developer familiarity is the key moderator — AI helps most when developers lack context, and hurts most when they already have it.
- Authors explicitly caution against overgeneralizing: results are consistent with AI providing substantial speedup on greenfield projects, unfamiliar codebases, or less experienced developers. The slowdown is specific to expert developers on mature, complex systems.
