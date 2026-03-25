---
title: "Your AI Product Needs Evals"
summary: "Practitioner's guide to building domain-specific LLM evaluation systems, arguing that the root cause of failed AI products is almost always a failure to create robust evals, and proposing a three-level framework: unit tests (assertions), human & model eval (trace inspection + LLM-as-judge alignment), and A/B testing."
year: 2024
link: "https://hamel.dev/blog/posts/evals/"
subjects: ["evals", "ai", "llm-evaluation"]
tags: ["evals", "llm-ops", "fine-tuning", "debugging", "rag", "practitioner-guide"]
---

## Why I saved this

- The most practical, experience-grounded guide to building eval systems for LLM products — directly applicable to anyone shipping AI features.

## Key points

- The root cause of unsuccessful AI products is almost always a failure to create robust evaluation systems. Success with AI hinges on how fast you can iterate, and iteration speed is gated by eval quality.
- Three levels of evaluation, ordered by cost: Level 1 (unit tests — fast assertions run on every code change), Level 2 (human & model eval — trace inspection, LLM-as-judge aligned to human labels), Level 3 (A/B testing — only for mature products).
- You must remove all friction from looking at data. Build domain-specific trace viewers rather than relying on generic tools. If you aren't looking at lots of data, you're doing it wrong.
- LLM-as-judge requires continuous alignment with human evaluators. Track agreement over time, collect human critiques explaining decisions, and iterate on the judge prompt. Use the most powerful model you can afford for critiquing.
- Eval infrastructure is not a sunk cost — it directly unlocks fine-tuning (curated traces become training data), synthetic data generation (test case prompts double as data synthesis prompts), and debugging (trace search + assertions flag root causes).
- Don't rely on generic evaluation frameworks. Create evaluation systems specific to your problem. 

## Notes

- Connects to the RAGAS paper (2023) in this vault — RAGAS provides reference-free metrics for RAG evaluation, which maps to Level 1 (automated assertions) in this framework. This article argues you need all three levels, not just automated metrics.
- The LLM-as-judge alignment process described here (spreadsheet iteration, tracking agreement, prompt engineering the critic) is a pragmatic, low-tech version of what the MT-Bench paper (Zheng et al., 2023) in this vault studied formally — both converge on the same conclusion that judge-human agreement must be continuously monitored.
- The "Why Language Models Hallucinate" paper (Kalai et al., 2025) in this vault argues that binary benchmark scoring reinforces hallucination. This article's Level 1 tests are binary by design, but the author explicitly notes you don't need 100% pass rate — the pass rate is a product decision, which sidesteps the binary scoring trap.
- The case study (Rechat's Lucy) illustrates the plateau pattern: rapid progress with prompt engineering, then a whack-a-mole phase where fixing one failure mode creates others. The eval system is what breaks through that plateau.
- Author is Hamel Husain, who led the team that created CodeSearchNet (precursor to GitHub Copilot). The advice comes from consulting across many AI product teams.
