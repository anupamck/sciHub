---

## title: "From Technical Debt to Cognitive and Intent Debt: Rethinking Software Health in the Age of AI"
summary: "Proposes a triple debt model for software health — technical debt (in code), cognitive debt (in people's understanding), and intent debt (in missing rationale artifacts) — arguing that generative AI may reduce technical debt while silently accelerating the other two."
year: 2026
link: "[https://arxiv.org/abs/2603.22106v2](https://arxiv.org/abs/2603.22106v2)"
subjects: ["software-engineering", "ai"]
tags: ["technical-debt", "cognitive-debt", "intent-debt", "cognitive-surrender", "shared-understanding", "ai-assisted-coding", "software-maintenance"]
---

## Why I saved this

- Provides a structured framework (Triple Debt Model) for reasoning about the non-code risks of AI-assisted development — cognitive debt and intent debt — which are harder to detect and may matter more than technical debt in the AI era.

## Key points

- **Triple Debt Model**: software health depends on three interacting layers — technical debt (lives in code, limits changeability), cognitive debt (lives in people, limits ability to reason about change), and intent debt (lives in artifacts, limits whether the system reflects what was meant to be built).
  - **Cognitive debt** refers to inadequate shared mental models that allow developers across a team to reason about a
system and what they need to understand to change it safely and confidently.
  - **Intent debt** refers to the absence or erosion of explicit rationale, goals, and constraints that guide how a system evolves
- AI may *reduce* technical debt through automated refactoring, test generation, and code review, while simultaneously *accelerating* cognitive and intent debt — the code improves but the team's understanding and captured rationale erode.
- **Cognitive surrender** (Shaw & Nave 2026) is distinct from cognitive offloading: offloading is strategically delegating a task to a tool (linter, type checker), while surrender means adopting AI outputs with minimal scrutiny, bypassing both intuitive and deliberate reasoning. Surrender also inflates confidence even when the AI is wrong.
- When a developer writes code from scratch, even messy code, the friction builds at least a partial mental model. When AI generates the same code, the developer may accept it without building that understanding — at scale across a team, this creates an accumulation of "not knowing."
- **Intent debt** is not just missing documentation — it accumulates when goals, constraints, and specifications guiding a system are unclear or uncaptured. What practitioners call "context debt" (missing info AI agents need) is largely a symptom of intent debt.
- Intent is best captured at the moment key decisions are made — unlike technical debt, recovering intent later can be impossible.
- The three debts reinforce each other: intent debt causes cognitive debt (unclear purpose prevents accurate mental models), cognitive debt causes technical debt (poor understanding leads to poor implementation), and technical debt amplifies cognitive debt (messy code is harder to reason about).
- Diagnosing cognitive debt: resistance to change, unexpected results from modifications, low bus factor, burnout from review pace mismatch, slow onboarding despite documentation.
- Diagnosing intent debt: behaviour drift from stakeholder expectations, AI agents struggling or requiring extensive clarification, loss of articulated non-functional requirements.
- Practical recommendations: treat shared understanding as a first-class deliverable, adopt intent-first workflows (ADRs, specs, domain modelling before code), resist automating understanding (AI-generated docs without human cognitive work just masks the debt), monitor all three layers in tandem.
- Reimplementation as a cognitive debt repair strategy: since code generation cost is now low, having an agent reimplement a feature with different tests or design elements can help rebuild the team's understanding.

## Notes

- Directly extends and provides the theoretical framework for the comprehension debt article (Addy Osmani, 2026) already in this vault — that article names the phenomenon at the individual/team level, while this paper provides the three-layer model and connects it to intent artifacts and organizational practices.
- The concept of "cognitive surrender" cited here (Shaw & Nave 2026) provides the psychological mechanism behind the comprehension test score findings referenced in the Osmani article (developers using AI for delegation scoring below 40% on comprehension tests).
- Connects to the software maintenance cost paper (2025) in our vault — if maintenance is 50-80% of lifetime cost, cognitive and intent debt compound it because fewer people can diagnose problems *and* the rationale for design decisions is lost.
- The paper's framing of intent debt as critical for AI agents is particularly relevant: AI coding agents need to understand what the system is *for*, not just what it currently does, making captured intent (specs, ADRs, domain models) essential infrastructure for agentic development.
- Reviewed by Kent Beck, Adam Tornhill, Mary Shaw, and Marian Petre among others — draws on Naur's "Programming as Theory Building" (1985) as foundational framing.

