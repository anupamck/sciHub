---
title: "How AI Impacts Skill Formation"
summary: "Randomized controlled trial showing that AI coding assistance impairs conceptual understanding, code reading, and debugging abilities (17% lower quiz scores) without delivering significant efficiency gains on average, while identifying three cognitively engaged AI interaction patterns that preserve learning outcomes."
year: 2026
link: "https://arxiv.org/pdf/2601.20245"
subjects: ["ai", "software-engineering", "education"]
tags: ["skill-formation", "cognitive-offloading", "ai-assisted-coding", "human-ai-collaboration"]
---

## Why I saved this

- Directly relevant to questions about sustainable AI adoption in engineering workflows — productivity gains vs. long-term competence erosion.

## Key points

- AI assistance produced a statistically significant 17% decrease in skill mastery (Cohen's d = 0.738, p = 0.01) — equivalent to nearly two letter grades on a 27-point quiz covering concepts used just minutes earlier.
- AI did not significantly speed up task completion on average, partly because some participants spent up to 11 minutes (30% of the 35-minute task window) composing AI queries.
- The largest score gap between AI and no-AI groups was on debugging questions, suggesting the ability to identify and diagnose errors is most vulnerable to AI-assisted workflows.
- Six distinct AI interaction patterns were identified via manual annotation of screen recordings. Three patterns involved cognitive offloading and produced poor learning outcomes (avg quiz scores 24-39%):
  1. **AI Delegation** — fully delegated coding to AI; fastest completion but no skill acquisition.
  2. **Progressive AI Reliance** — started with some questions, then gradually delegated everything to AI.
  3. **Iterative AI Debugging** — relied on AI to debug or verify code (5-15 queries) without building their own understanding; slowest and lowest-scoring pattern.
- Three patterns involved cognitive engagement and preserved learning outcomes (avg quiz scores 65-86%):
  4. **Generation-Then-Comprehension** — generated code via AI, then asked follow-up questions to understand it; highest quiz scores (86%) of any pattern.
  5. **Hybrid Code-Explanation** — asked for code generation and explanations together in combined queries.
  6. **Conceptual Inquiry** — asked AI only conceptual questions and wrote all code independently; largest cluster (7 of 25 participants), fastest among high-scoring patterns.
- The control group (no AI) encountered significantly more errors during the task, and independently resolving those errors likely drove their stronger skill formation — errors are a feature, not a bug, of learning.
- AI-enhanced productivity is not a shortcut to competence; AI assistance should be carefully adopted into workflows to preserve skill formation, particularly in safety-critical domains.

## Methodology

- 52 software engineers (mostly junior, all with 1+ years Python experience, no prior Trio knowledge) were randomly assigned to AI-assisted (treatment) or no-AI (control) groups.
- Main task: complete two coding tasks using the Python Trio library (asynchronous programming) within 35 minutes, mimicking on-the-job learning of a new tool via self-guided tutorial.
- Treatment group had access to a GPT-4o-powered chat assistant with full visibility into their code; control group could only use web search and provided documentation.
- Evaluation: a 14-question, 27-point quiz covering debugging, code reading, and conceptual understanding of the 7 core Trio concepts used in the tasks. No AI allowed during the quiz.
- Qualitative analysis: manual annotation of screen recordings for all 51 participants, coding events such as AI interactions, query types, errors encountered, and active coding time.
- 4 pilot studies (n=186 total) preceded the main study, resolving issues with non-compliance (participants secretly using AI in the control group), local item dependence in the quiz, and Python syntax barriers unrelated to Trio.

## Notes

- Connects to the maintenance cost discussion in our software-engineering notes: if junior developers cannot debug AI-generated code, the downstream maintenance burden shifts to the shrinking pool of senior engineers who learned without AI assistance.
- Relates to the hallucination paper (2025, Kalai et al.) already in this vault — if models hallucinate plausible code and developers lack the debugging skills to catch it, the two problems compound in safety-critical systems.
- The "conceptual inquiry" interaction pattern (ask AI only conceptual questions, write code independently) was the fastest high-scoring pattern and second fastest overall — suggesting that the most productive long-term AI workflow may be using it as a tutor rather than a coder.
- Participants themselves reported feeling "lazy" and noted "gaps in understanding" after using AI, while the no-AI group reported higher self-assessed learning and enjoyment — the subjective experience corroborates the objective quiz results.
- Anthropic blog summary with additional context: https://www.anthropic.com/research/AI-assistance-coding-skills
