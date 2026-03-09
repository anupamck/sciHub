---
title: "Why Language Models Hallucinate"
summary: "Argues that hallucinations are a natural statistical consequence of pretraining (reducible to binary classification errors on an Is-It-Valid problem) and persist because benchmark grading penalizes uncertainty — binary 0-1 scoring makes guessing optimal over abstaining, creating a socio-technical feedback loop that reinforces hallucination."
year: 2025
link: "https://arxiv.org/pdf/2509.04664"
subjects: ["ai", "language-models"]
tags: ["hallucination", "llm-foundations", "evaluation", "calibration", "computational-learning-theory"]
---

## Why I saved this

- Provides a formal, learning-theoretic explanation of why hallucinations emerge and why they persist despite post-training, rather than treating them as a mysterious failure mode.

## Key points

- Hallucinations need not be mysterious — they reduce to errors in binary classification.
- Even optimally pretrained, calibrated base models will hallucinate on underrepresented facts. 
- Hallucinations survive post-training because the vast majority of benchmarks use binary 0-1 grading. Under binary scoring, abstaining ("I don't know") always scores 0, making guessing strictly optimal — LLMs are always in "test-taking" mode.
- The fix must be socio-technical: modifying scoring of existing dominant benchmarks to stop penalizing abstention, rather than adding more hallucination-specific evaluations that get drowned out by the leaderboards.
- The analysis is architecture-agnostic — it applies to any density estimation model, not just Transformers or next-token predictors.

## Notes

- Implies that hallucination-specific benchmarks (e.g., TruthfulQA) are insufficient on their own. If the dominant leaderboards (MMLU, HumanEval, etc.) still use binary scoring, models will keep being optimized for confident guessing over honest uncertainty.
- GPT-4 calibration data shows base models are well-calibrated but calibration degrades after RLHF, suggesting post-training actively trades honesty for benchmark performance. This tension is central to the alignment problem.
- Connects to the MT-Bench / LLM-as-a-judge line of work: those benchmarks use richer grading, but still rarely reward abstention or hedging. The paper's argument implies that even preference-based evaluation may not fully solve the problem.
- Reasoning models (e.g., DeepSeek-R1) can fix "poor model" errors like letter counting through explicit chain-of-thought, but cannot fix "arbitrary fact" errors where the knowledge simply is not in the training data — a useful distinction for deciding where to invest in model improvements vs. retrieval augmentation.
