# Agent Usage Guide

## Template
- When adding new papers, always follow the structure in `templates/paper-template.md`.

## How key points and notes are to be written
- In key points, capture facts that are interesting and unique to the paper.
- In notes, capture related ideas and implications. 
- In notes, mention papers already saved that are related to this paper. 
- For both key points and notes, lean on facts that are provided in the abstract and the conclusion. 
- In papers that are technically complex, break down the main findings for easier understanding. 

## Workflow for detailed notes (when the user asks)
When the user asks for "detailed notes" or iterates on a note in conversation, follow this workflow:
1. **Start from the template** and fill in every section — do not skip any.
2. **Make key points specific, not generic.** Each bullet should be a claim, number, or mechanism unique to the paper. Avoid restating the abstract verbatim.
3. **Expand Methodology with concrete detail.** Name the experiments, datasets, benchmarks, or tasks used. If the paper reports degradation or improvement across conditions, list the conditions.
4. **Use the conversation to enrich Notes.** When the user and I discuss the paper (e.g., breaking down a figure, contrasting with modern practice), incorporate those insights into the Notes section — not just summaries of the paper itself.
5. **Stick to what the source says.** Do not add practical takeaways, recommendations, or advice that are interpretations or extrapolations beyond the paper's stated findings. If a takeaway is not directly supported by the source, leave it out.

### Example of a good detailed note
- `papers/ai/2025-context-rot.md` — demonstrates: specific key points (NIAH critique, per-model failure modes), a Methodology section listing all five degradation tasks by name, a Notes section built up from conversation (connection to RAG marginalization), and dense cross-references to related saved papers.
