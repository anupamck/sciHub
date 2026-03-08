---
title: "Language Models are Unsupervised Multitask Learners"
summary: "Introduces GPT-2, a 1.5B parameter Transformer that learns to perform NLP tasks (QA, translation, summarization) without task-specific supervision, trained on a curated web corpus (WebText), demonstrating that language model capacity is key to zero-shot task transfer."
year: 2019
link: "https://cdn.openai.com/better-language-models/language_models_are_unsupervised_multitask_learners.pdf"
subjects: ["ai", "language-models"]
tags: ["gpt-2", "zero-shot-learning", "transformers", "unsupervised-learning", "llm-foundations"]
---

## Why I saved this

- Foundational paper for the GPT lineage; establishes the paradigm that scaling unsupervised language models leads to emergent task-solving ability without explicit supervision.

## Key points

- Trained on WebText, a dataset of ~8 million web pages (40 GB of text) filtered for quality via Reddit link karma (≥3 upvotes).
- GPT-2 (1.5B params) achieves state-of-the-art on 7 of 8 language modelling benchmarks in zero-shot — no fine-tuning, no task-specific data.
- On CoQA (conversational QA), zero-shot GPT-2 reaches 55 F1, matching or beating 3 of 4 supervised baselines that used 127K+ training examples.

## Notes

- This paper demonstrates that an LLM can achieve state-of-the-art performance even with unsupervised learning. 
- It describes the foundational model GPT-2. Models that came later built upon the same mechanisms with larger scale. 
