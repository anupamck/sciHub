---
title: "LLM Evals: Everything You Need to Know"
summary: ""
year: 2026
link: "https://hamel.dev/blog/posts/evals-faq/"
subjects: ["evals", "ai", "llm-evaluation"]
tags: ["evals", "error-analysis", "practitioner-guide", "llm-as-judge", "rag", "annotation", "guardrails"]
---

## Why I saved this
- A list of FAQs from people who have been implementing LLM evals from Hamel's course. 

## Key points
- Error analysis is the single most crucial step to building evals that actually matter. It is a bottom-up process that will result in robust evals that are specific to a particular domain and a specific use-case.
- Build evals bottom-up from observed failures, not top-down from imagined ones. Generic metrics, ready-made evaluators, and eval-driven development all fail because LLMs break in unpredictable, domain-specific ways.
- Prefer simple, cheap checks (binary pass/fail, assertions, regex) over expensive ones (LLM-as-Judge, Likert scales). Reserve heavyweight evaluation for subjective qualities that actually need it.
- Keep humans in the loop for the hard parts: one domain expert as 'benevolent dictator' for annotation, manual open coding before automation, prompt writing over auto-optimisation. Outsourcing or automating these too early breaks feedback loops.
- Custom tooling pays off disproportionately. Teams with custom annotation interfaces iterate ~10x faster because they show all relevant context in one place.
- Guardrails and evaluators serve different purposes: guardrails are fast inline checks that block bad outputs in real-time; evaluators run asynchronously to inform improvement cycles.
- For complex systems (multi-turn, multi-agent, RAG), always focus on the first upstream failure. Downstream failures are often cascading consequences, not independent problems.


## Notes

### Getting started & fundamentals
- For a minimum viable eval setup
  - Prioritise error analysis over infrastructure
  - Try and use notebooks to review traces and analyse data
- When building an AI project, 60-80% of development time goes towards error analysis and evaluation
- Eval pass rate shouldn't be too high
  - If you're passing 100% of your evals, you're likely not challenging your system enough
  - A 70% pass rate might indicate a more meaningful evaluation that stress tests your application
- Even with perfect models, you'd still need systematic error analysis, domain-specific testing, and monitoring
  - People need to observe LLM behaviour to properly externalise requirements
- To make the case for evals, don't sell "evals" — show findings
  - Conduct error analysis on 50-100 conversations, document top failure modes, share metrics on error frequency
  - Let results drive the conversation rather than methods

### Error analysis & data collection
- Error analysis and data collection. This process involves
  - Creating a dataset: gathering representative traces of user interactions with the LLM. Generate synthetic data to get started
  - Open coding: annotate traces, noting any issues. A domain expert should perform this step. 
  - Axial coding: categorize the open-ended notes into a failure taxonomy by grouping similar failures into distinct categories. 
  - Iterative refinement: Keep iterating on traces until theoretical saturation is reached, and new traces don't reveal new failure modes or information. As a thumb rule, review at least 100 traces. 
- Error analysis should be rerun whenever significant changes occur: new features, prompt updates, model switches or major bugfixes. A useful heuristic is to review at least 100+ fresh traces.
  - Typical review cycles last 2-4 weeks
  - New systems need weekly analysis till failure patterns stabilise (10-20 traces)
- To surface problematic traces beyond user feedback
  - Start with random sampling and stress testing
  - Use outlier detection (sort by metrics like response length), user feedback signals, metric-based sorting, stratified sampling, embedding clustering
- To generate synthetic data, use structured queries
- Synthetic data may not be reliable for: complex domain-specific content, low-resource languages, high-stakes domains, underrepresented groups, or cases where validation is impossible
- When handling diverse user queries, let error analysis reveal failure patterns rather than building massive predetermined evaluation matrices

### Evaluation design & methodology
- For app centric evals, binary evaluations (pass/fail) are superior to Likert scale 1-5
  - Forces people to make a decision rather than hiding uncertainty
  - You don't waste time debating whether something is 3 or 4
- Eval driven development isn't practical, since LLMs fail in unpredictable ways
  - A better approach is to start with error analysis
- Don't build automated evaluators for every failure mode
  - Focus on persistent failures that survive prompt fixes
  - Many issues stem from unspecified preferences (response length, formatting)
  - Use cheap checks first: assertions, regex, reference-based comparisons
  - Reserve LLM-as-Judge for subjective qualities requiring repeated iteration
- Avoid ready-to-use evaluation metrics — they measure abstract qualities irrelevant to specific use cases
- Similarity metrics (BERTScore, ROUGE) are not useful for most applications
  - Exception: search and recommendation systems where cosine similarity measures semantic closeness
- You can usually use the same model for both the main task and evaluation
  - The judge performs a different task; what matters is alignment with human judgements
- Add tests that force a model to hallucinate
  - Ask it questions it isn't supposed to know

### Human annotation & process
- How many people should annotate my LLM outputs?
  - Start with 1 domain expert as 'benevolent dictator'
  - In most cases, this should suffice
- PMs and engineers should collaborate initially to establish context
  - Over time, empower a domain expert (often PM) as benevolent dictator
  - Provide custom annotation tools showing system outcomes alongside traces
- Outsourcing error analysis is usually a mistake
  - Breaks the feedback loop between observing failures and understanding improvements
  - Risks superficial labelling and loss of tacit knowledge
- What to automate with LLMs: first-pass axial coding, mapping annotations to failure modes, suggesting prompt improvements
  - Don't automate: initial open coding, validating taxonomies, ground truth labelling, root cause analysis
- Don't stop writing prompts manually
  - Writing prompts forces clarifying assumptions and externalising requirements
  - Automated optimisation hill-climbs predefined metrics, missing new failure modes

### Tools & infrastructure
- Build your own custom annotation tools
  - With AI-assisted development, custom interfaces can be built in hours
  - Teams with custom tools iterate ~10x faster because they show all context in one place
  - Render traces in a domain-specific way (emails like emails, code with syntax highlighting)
  - Support keyboard navigation and trace clustering/filtering/search
- Gaps in eval tooling you'll likely need to fill yourself: error analysis and pattern discovery, AI-powered workflow assistance, custom evaluators, and APIs supporting custom annotation apps
- Store prompts in Git as versioned software artifacts, reviewed atomically with code
  - GitHub's web interface works for non-technical stakeholders

### Production & deployment
- LLM-as-Judge evals come with significant overhead
  - Save them for critical use cases
  - Instead, opt for code-based checks (unit-test evals)
- Generic evaluations waste time and create false confidence
- CI/CD vs production evaluations
  - CI: small purpose-built test datasets (100+ examples), assertions and deterministic checks
  - Production: sampled live traces evaluated asynchronously, relies more on LLM-as-judge since reference outputs are unavailable
- Guardrails vs evaluators
  - Guardrails: inline, fast, deterministic checks in the request/response path (PII leaks, profanity, invalid syntax)
  - Evaluators: asynchronous, measure subjective qualities, feed dashboards and improvement loops
- Using evaluators to auto-fix outputs in production is limited
  - Most guardrails need speed and low false positive rates
  - Consider: cost of blocking good outputs vs letting bad ones through
- Don't prioritise model selection without evidence from error analysis
  - Many issues stem from prompt design or system architecture, not model limitations

### Domain-specific applications
- RAG is not dead
  - Articles claiming so specifically criticise naive vector database retrieval for coding agents
  - The core principle — retrieval providing relevant context — remains essential
  - Modern systems use agentic search rather than sole vector similarity
- Evaluating RAG requires evaluating two distinct components separately
  - Retrieval: information retrieval metrics (Recall@k, Precision@k, MRR)
  - Generation: error analysis, human labels, LLM-as-judge
  - Create synthetic eval datasets by reverse-processing: take documents, extract facts, generate questions those facts answer
- Chunk size depends on task type
  - Fixed-output tasks (extracting numbers, answering specific questions): larger chunks
  - Expansive-output tasks (summarisation, exhaustive extraction): smaller chunks respecting content boundaries
  - Treat chunk size as a hyperparameter to experiment with
- Debugging multi-turn conversations
  - Start simple: did the conversation meet the user's goal (pass/fail)
  - Focus on the first upstream failure — downstream failures often cascade
  - For multi-agent flows, assign session IDs logging every message with source and position
- Evaluating sessions with human handoffs
  - Capture complete user journeys including handoffs in traces
  - Log handoff decisions, context transferred, wait times, human actions, and final resolutions
  - Sometimes the best improvement is reducing handoffs entirely
- Evaluating complex multi-step workflows
  - Log entire workflows from initial trigger to final business outcomes
  - Use outcome metrics (completeness, accuracy, formatting) and process metrics (step count, time, resources)
  - Segment error analysis by workflow stages — early stage failures impact more since errors cascade
  - Use transition failure matrices to reveal failure hotspots
- Evaluating agentic workflows — two phases
  - End-to-end: treat agent as black box, did it meet user goals
  - Step-level diagnostics: score individual components (tool choice, parameter extraction, error handling, context retention)
  - Focus on first upstream failures; use transition failure matrices for error patterns