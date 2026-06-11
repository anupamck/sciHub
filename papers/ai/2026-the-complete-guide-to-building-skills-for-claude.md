---
title: "The Complete Guide to Building Skills for Claude"
type: "article"
summary: "Anthropic's official guide to building 'skills' — portable instruction packages (SKILL.md + optional scripts/references/assets) that teach Claude repeatable workflows, using a three-level progressive disclosure system and optional MCP integration."
year: 2026
link: "https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf"
subjects: ["ai", "prompt-engineering", "tooling"]
tags: ["claude", "skills", "mcp", "agent-workflows", "anthropic"]
---

## Why I saved this

- Relevance to my current work: defines the canonical structure for packaging domain knowledge into reusable Claude workflows — directly useful for building custom skills for research, code review, or document generation pipelines.

## Key points

- A skill is a folder containing a required `SKILL.md` file (Markdown with YAML frontmatter) plus optional `scripts/`, `references/`, and `assets/` directories. The same skill works across Claude.ai, Claude Code, and the API without modification.
- Skills use a **three-level progressive disclosure** system to minimize token usage: (1) YAML frontmatter is always loaded in the system prompt, (2) the SKILL.md body is loaded when Claude judges the skill relevant, (3) linked files in `references/` are loaded only on demand.
- The YAML `description` field is the most critical part — it must include both *what the skill does* and *when to use it* (trigger phrases). Claude uses this field alone to decide whether to load the skill. Vague descriptions ("helps with projects") cause under-triggering; overly broad ones cause over-triggering.
- Three common skill categories emerged from early adopters: (1) **Document & Asset Creation** — embedded style guides, templates, quality checklists, no external tools needed; (2) **Workflow Automation** — multi-step processes with validation gates and iterative refinement loops; (3) **MCP Enhancement** — workflow guidance layered on top of MCP tool access, coordinating multiple MCP calls in sequence.
- MCP provides connectivity (what Claude *can* do); skills provide knowledge (how Claude *should* do it). Without skills, each MCP conversation starts from scratch with inconsistent results. With skills, best practices are embedded in every interaction.
- Skills are published as an **open standard** — intended to be portable across AI platforms, not locked to Claude. Anthropic has been collaborating with ecosystem members on adoption.
- Organization admins can deploy skills workspace-wide (shipped December 2025). The API supports skills via `/v1/skills` endpoint and the `container.skills` parameter in the Messages API.
- The guide identifies five workflow patterns: sequential orchestration, multi-MCP coordination, iterative refinement, context-aware tool selection, and domain-specific intelligence (e.g., compliance checks before action).
- For critical validations, the guide recommends bundling executable scripts rather than relying on language instructions alone — "code is deterministic; language interpretation isn't."
- Limitations or caveats: success metrics are described as "aspirational targets" with "an element of vibes-based assessment." Anthropic states they are "actively developing more robust measurement guidance and tooling." The skill-creator tool helps design skills but does not execute automated test suites.

## Methodology

- The document is a practitioner's guide, not a research paper. No experiments or formal evaluation.
- Patterns and best practices are drawn from early adopters and Anthropic's internal teams.
- The recommended testing approach covers three areas:
  - **Triggering tests**: run 10–20 queries that should trigger the skill, plus negative cases that should not. Target: 90% correct triggering rate.
  - **Functional tests**: verify correct outputs, successful API calls, error handling, and edge cases. Run the same request 3–5 times for consistency.
  - **Performance comparison**: compare task completion with and without the skill — measure back-and-forth messages, failed API calls, and token consumption.
- Iteration strategy: start by perfecting a single challenging task until Claude succeeds, extract the winning approach into a skill, then expand to multiple test cases.
- The `skill-creator` skill (built into Claude.ai) can generate skills from natural language descriptions, review existing skills, and suggest improvements — positioned as a 15–30 minute path to a first working skill.

## Notes

- The progressive disclosure architecture mirrors a broader pattern in context engineering: minimizing what's loaded into the context window to avoid the degradation effects documented in context rot research. The three-level system is essentially a retrieval strategy — frontmatter as metadata index, SKILL.md as the primary document, references as on-demand expansion.
- The "kitchen analogy" (MCP = professional kitchen, skills = recipes) frames a clean separation of concerns that maps well to software architecture: MCP handles the I/O layer, skills handle the business logic layer. This is the same split that makes well-designed APIs useful — raw endpoint access is necessary but not sufficient without workflow knowledge.
- The five workflow patterns (sequential, multi-MCP coordination, iterative refinement, context-aware selection, domain-specific intelligence) are essentially design patterns for agent orchestration. The iterative refinement pattern with explicit "know when to stop" criteria is notable — it addresses the common failure mode of agents looping indefinitely.
- The troubleshooting section reveals practical failure modes: model "laziness" (skipping validation steps), instructions getting buried in verbose skill files, and large-context degradation when too many skills are loaded simultaneously. The recommendation to keep SKILL.md under 5,000 words and limit simultaneous skills to 20–50 is a concrete operational constraint.
- The emphasis on executable scripts for critical validations over natural language instructions is a pragmatic acknowledgment of LLM reliability limits — deterministic code gates prevent the model from "interpreting" its way past safety checks.
- Distribution is currently manual (download folder, zip, upload) with GitHub hosting as the recommended approach. The API path (`/v1/skills` endpoint, Agent SDK integration) points toward programmatic skill management at scale.

### Related papers
- `2025-context-rot.md` — the progressive disclosure design in skills directly addresses context rot: only load what's needed to avoid degradation from irrelevant content.
- `2022-react-synergizing-reasoning-and-acting-in-language-models.md` — skills formalize the interleaving of reasoning and tool use that ReAct introduced, packaging it into reusable workflow templates.
