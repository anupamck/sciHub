---
title: "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena"
summary: "Systematic study of LLM-as-a-judge showing strong GPT-4 agreement with human preferences on open-ended chat evaluation, while analyzing limitations such as position and verbosity biases."
year: 2023
link: "https://arxiv.org/pdf/2306.05685"
subjects: ["ai", "llm-evaluation", "benchmarking"]
tags: ["mt-bench", "chatbot-arena", "llm-as-a-judge", "bias"]
---

## Why I saved this

- Foundational reference for using LLM judges to scale chatbot evaluation.

## Key points

- Introduces MT-Bench and Chatbot Arena for preference-oriented evaluation of chat assistants.
- Reports high agreement (>80%) between strong LLM judges and human raters in many settings. This exceeded even human-to-human agreement. 
- Documents important judge limitations and mitigation methods (e.g., position swapping, reference-guided grading).

## Notes

- LLMs are susceptible to position bias. They often prefer the first response when provided with two very similar responses. 
- Most results here apply to ChatGPT 4.0
