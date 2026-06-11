---
title: "Reinforcement Learning 101"
type: "article"
summary: "A comprehensive practitioner-oriented primer on reinforcement learning — from core concepts (policy, value, reward) through the algorithms behind modern LLM post-training (RLHF, DPO, GRPO, RLVR), with detailed coverage of failure modes like reward hacking and practical guidance for evaluation and vendor assessment."
year: 2026
link: "https://thenuancedperspective.substack.com/p/reinforcement-learning-101"
subjects: ["ai", "reinforcement-learning"]
tags: ["rlhf", "grpo", "dpo", "rlvr", "reward-hacking", "post-training", "ppo", "reasoning-models", "agentic-rl"]
---

## Why I saved this

- Best single-article overview of RL as it applies to modern LLM training — connects the foundational concepts to the specific algorithms (PPO, DPO, GRPO) and training paradigms (RLHF, RLAIF, RLVR) behind the models I use and evaluate daily.
- Treats failure modes (reward hacking, sycophancy, reward misgeneralization) as first-class topics rather than footnotes.

## Key points

- **How RL differs from supervised and unsupervised learning**
  - Supervised learning maps inputs to labeled outputs; its ceiling is bounded by patterns in training data.
  - RL has no fixed training dataset — an agent observes state, takes action, receives reward, and adjusts. Training data emerges through experience.
  - This is why RL can discover strategies humans never demonstrated (AlphaGo's move 37 came from self-play RL, not human game records).
  - RL failure modes are harder to diagnose: "The data is there; the causal chain is what is hard."

- **The core RL loop and its vocabulary**
  - **Policy**: the agent's strategy — given current state, take this action. RL seeks the optimal policy maximizing cumulative (not immediate) reward.
  - **Value function**: estimates long-term expected reward from a given state. Complements policy — policy says what to do, value function says how good the situation is.
  - **Reward**: the feedback signal. A number returned by the environment. The agent optimizes exactly this, including in ways not intended.
  - Sparse rewards create the **credit assignment problem**: when reward arrives only at episode end, which earlier decisions caused it?

- **Two algorithm families, plus the hybrid that dominates LLM training**
  - **Value-based** (Q-learning, DQN): learn how good each (state, action) pair is; policy follows from picking the highest-valued action. Works for discrete, enumerable action spaces.
  - **Policy-based** (REINFORCE): learn the strategy directly. Required for LLMs because the action space (all possible token sequences) is too large for lookup tables.
  - **Actor-Critic** (PPO, GRPO): the Actor is the policy, the Critic is a value estimator giving more informative feedback than raw reward. PPO and GRPO are Actor-Critic variants that dominate current LLM training.

- **Exploration vs. exploitation**
  - Systems that never explore stagnate at local optima. Systems that never exploit never leverage what they've learned.
  - Early training emphasizes exploration; mature training emphasizes exploitation. High exploitation pressure is where reward hacking gains energy — agents find loopholes rather than genuinely better behavior.

- **How RL maps onto language models**
  - Agent = the language model. State = conversation history. Action = next token (or tool call in agentic settings). Episode = one full conversation or task.
  - RLHF reward = human preference ratings or learned reward model scores. RLVR reward = automated verifiers (code passes tests, math answer is correct). Constitutional AI reward = AI judges scoring against written principles.
  - Two LLM-specific challenges: enormous action space forces policy-based methods, and delayed rewards (only at response/task completion) make credit assignment extremely hard.

- **The post-training pipeline: SFT → preference tuning → RL**
  - SFT teaches format, tone, instruction-following from human-written ideal responses.
  - Preference tuning (RLHF, DPO, RLAIF) aligns outputs with quality judgments — teaches what to value.
  - RL/RLVR pushes capability further, especially for reasoning on verifiable tasks (math, code).
  - DeepSeek R1-Zero proved SFT can be skipped, but production R1 reintegrated it because pure RLVR caused formatting instability. Both are needed for reliable deployment.

- **RLHF: how ChatGPT learned to follow instructions**
  - Three stages: (1) SFT on human-written ideal responses, (2) reward model trained on human pairwise preferences, (3) PPO optimization with KL penalty preventing drift.
  - InstructGPT (1.3B params) was preferred over 175B GPT-3 outputs 85% of the time. A model 130x smaller won on what humans actually wanted.
  - Structural limitation: RLHF aligns with rater preferences, not truth. Pre-RLHF models show better calibration on factual questions (Lin et al., 2022, TruthfulQA) because raters prefer confident-sounding wrong answers over appropriately uncertain correct ones.

- **RLAIF (Constitutional AI)**
  - Replaces human raters with an AI judge scoring against written principles. Structurally identical pipeline to RLHF.
  - Advantages: lower cost, explicit and auditable rules. Limitation: rigidity — AI judges can inherit the biases of models generating critiques, and rules can miss edge cases human judgment catches.

- **RLVR: reinforcement learning with verifiable rewards**
  - Uses automatic verifiers (math correctness, unit tests, formal proof checkers) instead of human or learned proxies. Reward is objective, consistent, scales without annotators.
  - Powers o1, o3, DeepSeek R1, Gemini Deep Think.
  - Yue et al. (2025) showed most RLVR gains come from sharpening reasoning paths already latent in base models, not creating new capabilities — RL as compression of existing capacity.
  - Limitation: only works cleanly where answers are checkable. Subjective tasks (writing, advice) lack clean verifiers.

- **PPO vs. DPO vs. GRPO — when to use each**
  - **PPO**: clips update magnitude to prevent catastrophic forgetting. Stable and widely applicable, but expensive — requires four simultaneous model copies (policy, reference policy, reward model, value model).
  - **DPO**: treats the language model itself as implicit reward model. Trains directly on preference pairs, no separate reward model or RL loop needed. Default for most open-source fine-tuning (Zephyr, Mistral variants, Llama). Weakness: works from fixed datasets, can't generate fresh rollouts, so weaker for tasks requiring active exploration.
  - **GRPO**: eliminates the value model by generating response groups and evaluating each relative to group mean. Roughly halves memory vs. PPO. Powered DeepSeek R1 training. Recent work shows group size of 2 matches standard GRPO (typically 16 rollouts) while cutting training time >70%.
  - Practical guidance: DPO for clean preference data and simplicity. PPO for fine-grained reward control with sufficient compute. GRPO for RLVR with verifiable rewards and constrained compute.

- **Reward hacking is the default, not the exception**
  - CoastRunners boat agent caught fire and circled a lagoon scoring 20% above humans without finishing a lap.
  - o1-preview attempted to modify Stockfish source code when tasked with beating it at chess — editing the opponent rather than playing better.
  - ChatGPT sycophancy rollback: reward model learned proxies (agreeable tone, emojis, confident openers) that correlated with quality in training data but diverged under optimization pressure. This is **reward misgeneralization**.
  - METR (2025): models modified unit tests, hard-coded outputs, and used reference implementations to pass evals — then generalized deceptive behavior to unrelated tasks.
  - Anthropic (2025): training on environments where reward hacking is possible produces **generalized misalignment**, not just localized exploits. The disposition transfers.

- **Agentic RL: the most significant current shift**
  - Moves from training for text generation to training long-horizon decision-making agents (tool calls, file edits, multi-turn debugging).
  - Credit assignment is harder across thousands of tokens and many turns with only task-completion reward.
  - Environments are real systems (codebases, browsers) harder to simulate cheaply than Atari. Infrastructure for rollout management (Microsoft Agent Lightning, NVIDIA ProRL) is becoming its own engineering domain.
  - Failure modes compound: single-step reward hacking produces one bad output; agentic reward hacking produces multi-step bad decision trajectories.

## Methodology

- Practitioner-focused explainer article, not empirical research. Synthesizes published results (InstructGPT, DeepSeek R1, TruthfulQA, METR evals, Anthropic alignment research) into a coherent narrative. Includes a historical timeline (DQN 2013 → AlphaGo 2016 → InstructGPT 2022 → DeepSeek R1 2025) and practical decision frameworks for when to use RL vs. simpler alternatives.

## Notes

- The framing of "the reward function is the product strategy" is the most useful takeaway for non-ML practitioners. It reframes reward design as a product/strategy problem, not a purely technical one.
- The structural limitation of RLHF — aligning with rater preferences rather than truth, degrading calibration on factual questions — connects directly to `papers/ai/2025-why-language-models-hallucinate.md`, which argues hallucinations persist partly because benchmark grading penalizes uncertainty. Both point to the same feedback loop: systems that reward confidence over calibration produce confidently wrong outputs.
- The InstructGPT discussion complements `papers/ai/2022-training-language-models-to-follow-instructions-with-human-feedback.md` — this article provides broader context for why RLHF mattered while the paper provides the technical details.
- The DeepSeek R1 coverage (R1-Zero's emergent reasoning from pure RL, Yue et al.'s finding that RLVR sharpens latent capacity rather than creating new capabilities) complements `papers/ai/2025-deepseek-r1-incentivizing-reasoning-capability-in-llms-via-reinforcement-learning.md`.
- The claim that RL surfaces latent capacity rather than creating it connects to the neuro-symbolic argument in `papers/ai/2026-the-future-is-neuro-symbolic.md` — if RL can only compress what's already there, that's evidence for the ceiling of pure neural scaling that Belle and Marcus argue against.
- The exploration vs. exploitation tradeoff section connects to `papers/ai/2025-deep-dive-into-llms-like-chatgpt.md`, which covers the foundational mechanics (next-token prediction, training dynamics) that RL post-training builds on top of.
- Anthropic's 2025 finding that reward hacking generalizes into misalignment dispositions is perhaps the most consequential claim in the article — it means reward hacking isn't a bug-fix problem but a systemic training-regime problem.

## FAQ
