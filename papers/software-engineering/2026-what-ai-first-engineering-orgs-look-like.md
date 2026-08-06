---
title: "What AI-First Engineering Orgs Look Like"
type: "article"
summary: "Argues that AI-assisted coding shifts the engineering bottleneck from writing code to verification, review, and security, and lays out concrete changes to planning, information-seeking, code review, team composition, and org principles that follow from that shift."
year: 2026
link: "https://arpitbhayani.me/blogs/ai-first-org"
subjects: ["software-engineering", "ai"]
tags: ["ai-assisted-coding", "code-review", "engineering-process", "org-design", "team-composition"]
---

## Why I saved this

- Relevance to my current work
- Relevant to my AI first vision
- Crisp article that is laid out well

## Key points

- Every process a software team runs was built to manage a scarce resource. For twenty years, that resource was engineering time. 
- Writing code was expensive, so it was protected with a process
- With AI first, writing code, tests and refactoring aren't the bottleneck anymore
  - The bottleneck shifts to verification, code review and security
- AI first orgs plan Just In Time (JIT)
  - Do the minimum planning needed, right before you need it
  - Skip design docs for most features. Build prototype first and write down what you learnt
  - Get prototype in front of five or ten internal users within 1 or two days, replacing a formal beta cycle
  - Reserve a full design doc for rare, expensive decisions that are hard to reverse. E.g. data model change or public API contract
  - "Can this decision be undone with one more prototype iteration"? Then no need for the doc
- Context ownership
  - Formerly, the author of code held context nobody else had
  - Today, this context can be synthesized by the model via a series of questions
    - Who caused this regression? When? Walk through the git history to find out.
    - Who is the domain expert on this subsystem? Ask the model to infer from commit activity. 
    - Why was this decision made? Ask model to pull PR description and linked discussion
  - Prerequisite: Clean commit discipline and PR documentation
- Automate
  - Questions that repeat at least thrice a month
  - Status report meetings that should be a memo
- Code review: Trust but verify
  - The model owns
    - Iterating on a PR until comments are resolved
    - Catching and fixing bugs before a commit lands
    - Writing and updating tests for the change
  - Humans stay in the loop where domain judgement cannot be automated:
    - Legal review for anything touching data handling, licensing, compliance
    - Security review for trust boundaries, auth flows, anything crossing a privilege level
    - Product and design reviews for taste; validation of whether a user problem is actually solved
    - Tests before assigning a human reviewer: 
      - Would a wrong call here be expensive to reverse? 
      - Does it require judgement about risk tolerance rather than correctness? 
    - This decision isn't static. It keeps moving as models improve
  - Roles blur. AI first orgs hire for
    - Creative builders with product sense
      - Prototype rapidly 
      - Care if it actually solves a real problem
    - Engineers with deep systems expertise
      - People who understand hard constraints like distributed state, latency budgets or security boundaries
    - Scarce skill: knowing where a human still needs to make the call
  - A flat org with highly autonomous teams is non negotiable
    - Anyone can question and kill a process that no longer serves its purpose, without needing permission from above
  - Useful metrics
    - Onboarding ramp time: How fast does a new team member ship real work? Should drop down to a few hours or a couple of days. 
    - PR cycle time: helps identify bottlenecks for shipping code
    - Percentage of AI assisted commits: should be 100%
  - The last throughput metric should be coupled with a metric that actually solves the problem: customer retention, incident rate, feature adoption etc. 
  - Continually audit your noisiest workflow
    - Find out where the workflow bottleneck is
    - Question whether it is still needed 
    - If yes, can it be automated
  - 


## Methodology
- Brief and easy to understand description of the methodology used in the paper.

## Notes

- Follow-up ideas:
- Related papers:

## FAQ
