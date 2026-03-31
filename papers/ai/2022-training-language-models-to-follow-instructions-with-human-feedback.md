---
title: "Training Language Models to Follow Instructions with Human Feedback"
summary: "Introduces InstructGPT, showing that fine-tuning with human feedback (RLHF) makes a 1.3B parameter model preferred over a 175B GPT-3 by human evaluators."
year: 2022
link: "https://arxiv.org/abs/2203.02155"
subjects: ["ai", "nlp", "alignment"]
tags: ["rlhf", "instruction-tuning", "foundational"]
---

## Why I saved this

- Foundational paper for aligning language models with human intent via RLHF.

## Key points

- Main claims:
  - Making LLMs bigger does not inherently make them more helpful, truthful, or harmless.
  - A 1.3B parameter InstructGPT model outperformed the 175B parameter GPT-3 in human evaluations — 100x fewer parameters.
- Evidence:
  - Human evaluators preferred InstructGPT outputs over GPT-3 outputs.
  - Improved truthfulness (TruthfulQA) and reduced toxic output generation.
  - Minimal degradation on standard NLP benchmarks.
- Limitations or caveats:
  - Relies on quality and biases of human labelers.
  - RLHF can overfit to labeler preferences rather than true user intent.

## Methodology

- Three-stage process: (1) collect demonstration data and fine-tune GPT-3 with supervised learning, (2) collect comparison data and train a reward model to rank outputs, (3) optimize the policy against the reward model using PPO (Proximal Policy Optimization).

## Notes

- Follow-up ideas:
  - This is the paper behind the shift from base models to instruction-following models (GPT-3 → GPT-3.5/ChatGPT lineage).
- Related papers:
  - Key precursor to the RLHF techniques now standard across the industry.
