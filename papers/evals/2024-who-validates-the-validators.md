---
title: "Who Validates the Validators? Aligning LLM-Assisted Evaluation of LLM Outputs with Human Preferences"
summary: "Introduces EvalGen, a mixed-initiative interface where humans and LLMs collaborate to create evaluation functions for LLM outputs, revealing that evaluation criteria often emerge through grading rather than being defined upfront (criteria drift)."
year: 2024
link: "https://arxiv.org/pdf/2404.12272"
subjects: ["evals", "ai", "llm-evaluation", "human-ai-interaction"]
tags: ["evals", "llm-as-judge", "criteria-drift", "human-alignment", "evaluation-functions"]
---

## Why I saved this

- Directly addresses the meta-problem of LLM evaluation: when you use LLMs to judge LLM outputs, who validates that the judges are correct? Proposes a practical human-in-the-loop solution.

## Key points

- LLMs used to evaluate other LLM outputs inherit their own biases and limitations, creating a recursive validation problem. Human alignment is essential to ground evaluation.
- EvalGen is a mixed-initiative system that generates candidate evaluation criteria and implementations (code and LLM-based), then uses human feedback on graded examples to select the best-aligned options.
- Key finding: "criteria drift" — evaluation criteria are not static. They often emerge and evolve through the act of grading outputs, rather than being fully specifiable upfront. Some criteria depend on specific outputs rather than being universal.
- The system supports both assertion-based (code) and LLM-based evaluation functions, letting users choose the right tool for each criterion.
- User study with 8 participants showed that the mixed-initiative approach helped users discover criteria they had not initially considered, and that alignment between generated evaluators and human preferences improved through iterative feedback.

## Methodology

- Built EvalGen as a mixed-initiative interface where users define goals, review candidate criteria, and co-develop evaluators with LLM assistance.
- Generated multiple candidate evaluator implementations per criterion, including Python assertion functions and LLM grader prompts.
- Collected human grades on a subset of model outputs and used that feedback signal to rank/select candidate evaluators that best matched user judgments.
- Compared the feedback-driven selection strategy against a baseline approach to test whether human-in-the-loop alignment improved evaluator quality.
- Ran a qualitative user study (8 participants) to analyze workflow fit, perceived usefulness, and how evaluation criteria evolved during use (criteria drift).

## Notes

- Directly complements "Your AI Product Needs Evals" (2024) in this repo. That article's Level 2 (human and model eval with LLM-as-judge alignment) is the problem EvalGen targets with tooling.
- Complements the MT-Bench paper (Zheng et al., 2023) in this repo. MT-Bench analyzes LLM-as-judge agreement with humans at scale, while this paper focuses on creating aligned evaluation functions.
- The criteria drift concept challenges the common assumption that all evaluation criteria can be defined before seeing model outputs, which has implications for continuous eval workflows.
