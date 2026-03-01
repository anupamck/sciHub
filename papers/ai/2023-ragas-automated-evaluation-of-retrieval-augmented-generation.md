---
title: "RAGAS: Automated Evaluation of Retrieval Augmented Generation"
summary: "Introduces a reference-free evaluation framework for RAG pipelines with metrics for retrieval quality, answer faithfulness, and generation quality, enabling faster iteration without extensive human labels."
year: 2023
link: "https://arxiv.org/pdf/2309.15217"
subjects: ["ai", "rag", "llm-evaluation"]
tags: ["ragas", "evaluation", "faithfulness", "retrieval-metrics"]
---

## Why I saved this

- Core paper for evaluating RAG systems systematically beyond ad-hoc manual checks.

## Key points

- Proposes automated metrics for critical RAG dimensions without requiring gold reference answers.
- Separates retrieval and generation quality signals, making failures easier to diagnose.
- Enables faster and more consistent model/pipeline comparisons during RAG development.

## Notes

- Useful baseline before designing custom evaluation rubrics for domain-specific RAG use cases.
