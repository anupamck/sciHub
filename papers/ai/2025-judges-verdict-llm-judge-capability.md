---
title: "Judge's Verdict: A Comprehensive Analysis of LLM Judge Capability Through Human Agreement"
summary: "Evaluates 54 LLMs as judges for answer-accuracy scoring and proposes a two-step benchmark using correlation plus Cohen's kappa-based human-likeness analysis. Finds 27 Tier 1 judges, including human-like and super-consistent categories."
year: 2025
link: "https://arxiv.org/pdf/2510.09738"
subjects: ["ai", "llm-evaluation", "rag"]
tags: ["llm-as-a-judge", "cohens-kappa", "benchmark"]
---

## Why I saved this

- Benchmarks LLM judges against human judges.

## Key points

- Correlation alone is not enough; agreement metrics are needed to detect bias and scoring style differences.
- Introduces a "human-likeness" criterion based on z-scores over Cohen's kappa in mixed human+LLM groups.
- Distinguishes two useful judge behaviors: human-like variation and super-consistent agreement.

## Notes

- The paper reports an open dataset, code, and leaderboard for reproducible judge benchmarking.
