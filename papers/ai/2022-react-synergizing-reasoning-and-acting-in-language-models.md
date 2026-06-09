---
title: "ReAct: Synergizing Reasoning and Acting in Language Models"
summary: "Introduces ReAct, a prompting framework that interleaves chain-of-thought reasoning traces with task-specific actions, enabling LLMs to ground their reasoning in external information (e.g., Wikipedia) and plan dynamically in interactive environments."
year: 2022
link: "https://arxiv.org/abs/2210.03629"
subjects: ["ai", "agents", "reasoning"]
tags: ["react", "chain-of-thought", "tool-use", "language-agents", "prompting"]
---

## Why I saved this

- Foundational paper for LLM-based agents that reason and act; defines the pattern behind most modern agentic frameworks (LangChain, AutoGPT, etc.).

## What is ReAct

Prior to ReAct, reasoning (chain-of-thought) and acting (tool use) were studied separately. Chain-of-thought lets a model think step-by-step but has no way to check facts — it hallucinates when its internal knowledge is wrong. Act-only agents can call tools but have no explicit reasoning about *why* they're taking an action or *what* to do next — they lose track of multi-step plans.

ReAct unifies both in a single prompt-based loop: **Thought → Action → Observation → Thought → ...**. At each step the model either produces a thought (free-form reasoning in natural language) or an action (a call to an external tool). Thoughts don't go to the environment — they stay in the model's context as a scratchpad for decomposing goals, tracking progress, handling exceptions, and deciding the next action. Actions hit the environment (e.g., a Wikipedia search API) and return an observation that feeds into the next thought.

Concretely, a ReAct trajectory on a multi-hop question might look like: *Thought: I need to find when X was born → Action: search[X] → Observation: X was born in 1990... → Thought: Now I need to find Y → Action: search[Y] → ... → Action: finish[answer]*.

The key insight is that this interleaving is synergistic: reasoning helps the agent plan which actions to take and interpret their results, while actions ground the reasoning in real information and prevent hallucination.

## Key points

- ReAct expands the action space from task-specific actions (A) to A ∪ L, where L is natural language. Thoughts don't produce environment feedback but update the agent's context for future reasoning and acting.
- On HotpotQA, ReAct alone (27.4% EM) underperforms CoT-SC with 21 samples (33.4%), but a hybrid ReAct → CoT-SC strategy reaches 35.1% — matching CoT-SC's accuracy with only 3-5 samples instead of 21.
- On FEVER fact verification, ReAct (60.9%) outperforms all CoT variants because grounding claims against Wikipedia is more reliable than closed-book reasoning.
- On ALFWorld (text-based household tasks), ReAct achieves 71% success vs. 45% for act-only and 37% for the trained BUTLER baseline — a 26 percentage point gain from adding sparse reasoning traces.
- On WebShop, ReAct reaches 40% success rate, a 10 percentage point absolute improvement over act-only and outperforming imitation learning + RL baselines.
- Error analysis on HotpotQA: CoT's dominant failure mode is hallucination (56% of errors), while ReAct's dominant failure mode is reasoning errors and search failures (47% + 23%) — different and more debuggable failure modes.
- ReAct's false positive rate in correct answers is 6% vs. CoT's 14%, making it more trustworthy even when both get the right answer.
- Fine-tuning with just 3,000 ReAct trajectories on PaLM-8B outperforms all PaLM-62B prompting methods; on PaLM-62B it outperforms all PaLM-540B prompting methods.
- ReAct enables human-in-the-loop correction by editing thoughts mid-trajectory — something infeasible with RL-trained policies.

## Methodology

- Few-shot prompting with human-annotated trajectories containing interleaved thought-action-observation triples. Knowledge tasks use 3-6 examples with dense thoughts; decision-making tasks use sparse thoughts at key decision points.
- Knowledge-intensive tasks (HotpotQA, FEVER): action space is search[entity], lookup[string], finish[answer] against a Wikipedia API. Model alternates between reasoning about what to search and acting on search results.
- Decision-making tasks (ALFWorld, WebShop): action spaces are environment-specific (navigate, interact, search, buy). Thoughts appear at subgoal boundaries rather than every step.
- Primary model: PaLM-540B. Cross-validated on GPT-3, where results were comparable or better (e.g., ALFWorld 78.4% vs. 70.9%).
- Baselines: standard prompting, chain-of-thought (CoT), CoT with self-consistency (CoT-SC), and act-only (actions without reasoning traces).

## Notes

- The hybrid strategies (ReAct → CoT-SC and CoT-SC → ReAct) are the most practical finding: use ReAct first, fall back to CoT-SC when ReAct's search fails, or vice versa. This pattern of switching between grounded retrieval and internal reasoning based on confidence appears in most production agent architectures today.
- ReAct's failure modes (bad searches, reasoning loops) are observable and correctable — unlike CoT hallucinations, which are confidently wrong. This interpretability advantage matters more in practice than raw accuracy numbers.
- The fine-tuning results hint that small models + ReAct training data can punch far above their weight class, a pattern later confirmed by tool-use fine-tuning in models like Toolformer.

### Related papers
- `2020-retrieval-augmented-generation-for-knowledge-intensive-nlp-tasks.md` — RAG grounds generation in retrieved documents; ReAct generalizes this to arbitrary action spaces with explicit reasoning.
- `2025-why-language-models-hallucinate.md` — ReAct's error analysis directly shows the hallucination reduction: 6% false positive rate vs. CoT's 14%, achieved by grounding in external sources.
- `2025-context-rot.md` — ReAct retrieves passages on-demand rather than stuffing context, naturally avoiding the context rot problem of long-context RAG pipelines.
