---
title: "LLM Evals: Everything You Need to Know"
summary: ""
year: 2026
link: "https://hamel.dev/blog/posts/evals-faq/"
subjects: ["evals", "ai", "llm-evaluation"]
tags: []
---

## Why I saved this
- A list of FAQs from people who have been implementing LLM evals from Hamel's course. 

## Key points
- Error analysis is the single most crucial steps to building evals that actually matter. It is a bottom-up process that will result in robust evals that are specific to a particular domain and a specific use-case.  


## Notes
- For a minimum viable eval setup
  - Prioritise error analysis over infrastructure
  - Try and use notebooks to review traces and analyse data
- When building an AI project, 60-80% of development time goes towards error analysis and evaluation
- Eval pass rate shouldn't be too high
  - If you're passing 100% of your evals, you're likely not challenging your system enough
  - A 70% pass rate might indicate a more meaningful evaluation that stress tests your application
- Error analysis and data collection. This process involves
  - Creating a dataset: gathering representative traces of user interactions with the LLM. Generate synthetic data to get started
  - Open coding: annotate traces, noting any issues. A domain expert should perform this step. 
  - Axial coding: categorize the open-ended notes into a failure taxonomy by grouping similar failures into distinct categories. 