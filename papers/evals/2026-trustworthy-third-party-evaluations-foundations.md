---
title: "A shared playbook for trustworthy third party evaluations"
summary: "OpenAI shares lessons learned and recommended approaches for designing valid third-party evaluations of frontier model capabilities and safeguards, emphasising that harness choice, elicitation budget, and explicit claim scoping are critical to producing interpretable results."
year: 2026
link: "https://openai.com/index/trustworthy-third-party-evaluations-foundations/"
subjects: ["evals", "ai", "safety"]
tags: ["third-party-evals", "frontier-models", "safeguards", "elicitation", "benchmarks"]
---

## Why I saved this

## Key points

- Evaluation claims fall into three types:
  - **Capability elicitation**: can the model plausibly produce a given capability?
  - **Safeguard performance**: how robust are safeguards against a given behaviour or attack?
  - **Comparison**: how do different models perform under equivalent conditions?
- The **harness** (surrounding environment: tools, state management, retries) can change observed performance as much as the model itself — especially on multi-step agentic tasks
  - A harness that preserves state and retries failures can let a model finish tasks it would never complete in a simpler harness
- Good evaluation reports should specify: (1) what claim the setup was designed to test, and (2) the evidence that the result is valid
- **Threats to validity** to watch for:
  - **Reward hacking**: exploiting shortcuts in the task or scorer
  - **Refusals**: refusing in ways that obscure the behaviour being tested
  - **Contamination**: overperforming because tasks/answers appeared in training data
  - **Broken problems**: underperforming due to invalid tasks, unfair scoring, or unreliable tools
  - **Sandbagging**: deliberately underperforming when the model detects it is being evaluated
- **Compute budget matters**: increasing test-time token budget from 10M→100M tokens improved performance by up to 59% in UK AISI's cyber range evaluation — results should always state the budget used and whether performance had plateaued
- If performance is still improving at the highest budget tested, the score is a lower-bound estimate, not a capability ceiling

## Notes
