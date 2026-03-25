---
title: "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena"
summary: "Systematic study of LLM-as-a-judge showing strong GPT-4 agreement with human preferences on open-ended chat evaluation, while analyzing limitations such as position and verbosity biases."
year: 2023
link: "https://arxiv.org/pdf/2306.05685"
subjects: ["evals", "ai", "llm-evaluation", "benchmarking"]
tags: ["mt-bench", "chatbot-arena", "llm-as-a-judge", "bias"]
---

## Why I saved this

- Foundational reference for using LLM judges to scale chatbot evaluation.

## Key points

- Introduces MT-Bench and Chatbot Arena for preference-oriented evaluation of chat assistants.
- Reports high agreement (>80%) between strong LLM judges and human raters in many settings. This exceeded even human-to-human agreement. 
- Documents important judge limitations and mitigation methods (e.g., position swapping, reference-guided grading).

## Methodology

**MT-Bench dataset**
- 80 manually written multi-turn questions across 8 categories (writing, roleplay, extraction, reasoning, math, coding, STEM, humanities), 10 per category.
- Each question has exactly 2 turns; turn 2 requires the model to build on its turn 1 answer.
- 6 models evaluated: GPT-4, GPT-3.5, Claude-v1, Vicuna-13B, Alpaca-13B, LLaMA-13B.

**Judging**
- Three LLM judge modes: pairwise comparison, single-answer grading (1–10), and reference-guided grading (judge's own answer shown as reference before grading).
- For multi-turn questions, both full conversation histories are shown in a single prompt — splitting into two prompts caused the judge to mis-reference prior answers.
- 58 expert human annotators (mostly grad students), paid ~$35/hr, each judged ≥20 randomly assigned questions, yielding ~3K total votes.

**Bias mitigation**
- Position bias: every pairwise comparison is run twice with answer order swapped; a win is only declared if the same model wins both times, otherwise a tie.
- Math/reasoning: reference-guided grading (show the judge's own independently generated answer as a reference) reduces math grading failure from 70% to 15%.

**Agreement metric**
- Defined as the probability that a randomly selected judge of each type agrees on a randomly selected question.
- Reported under two setups: S1 (all votes, ties and inconsistencies both counted as ties; random baseline = 33%) and S2 (only non-tie, consistent votes; random baseline = 50%).

## Noteworthy results

- **GPT-4 vs. human experts on MT-Bench (S2): 85%** — matches or exceeds human-human agreement of 81% on the same questions.
- **Human-human agreement on MT-Bench (S2): 81%** — the practical ceiling for any automated judge, and GPT-4 clears it.
- **GPT-4 vs. crowd humans on Chatbot Arena (S2): 87%** — even higher than the controlled expert setting.
- **Under S1 (all votes included), GPT-4 vs. humans drops to ~66%** — barely above the 33% random baseline. The 85%+ headline depends entirely on filtering out ambiguous cases.
- **Position bias — GPT-4 consistency: 65%** with default prompt, vs. Claude-v1 at 23.8% and GPT-3.5 at 46.2%. GPT-4 is the most robust but still inconsistent on 35% of cases.
- **Verbosity bias — "repetitive list" attack**: Claude-v1 and GPT-3.5 failed 91.3% of the time (preferred a padded, repetitive answer over a clean one). GPT-4 failed only 8.7%.
- **Few-shot prompting** improves GPT-4 consistency from 65% to 77.5%, but adds 4× API cost and showed no clear improvement in human agreement.
- **LLM-LLM agreement is suspiciously high**: GPT-3.5 vs. Claude under S2 = 96% — LLM judges agree with each other more than they agree with humans, suggesting shared systematic biases.
- **Category breakdown**: position bias is worst on open-ended categories — writing (42% consistent) and humanities (36%) — and nearly absent on math (86%) and coding (86%), where answers are more objectively correct.
- **Agreement scales with performance gap**: GPT-4 vs. human agreement goes from ~70% when comparing similarly capable models to ~100% when comparing models with very different ability (e.g., GPT-3.5 vs. LLaMA-13B at 98.8% consistency).
- **Fine-tuned Vicuna-13B as a judge**: trained on 20K arena votes, achieves 85.5% agreement with humans under S2 — nearly matching GPT-4 at a fraction of the cost.

## Notes

- LLMs are susceptible to position bias. They often prefer the first response when provided with two very similar responses.
- Most results here apply to GPT-4 (gpt-4-0314); results for other models are notably worse.
- Safety, honesty, and harmlessness are explicitly out of scope — the benchmark only measures helpfulness.
