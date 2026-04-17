---
title: "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks"
summary: "Introduces RAG: a fine-tuning recipe that combines a pre-trained seq2seq model (parametric memory) with a dense Wikipedia vector index (non-parametric memory) accessed via a neural retriever, achieving state-of-the-art on open-domain QA."
year: 2020
link: "https://arxiv.org/abs/2005.11401"
subjects: ["ai", "rag", "information-retrieval"]
tags: ["retrieval-augmented-generation", "seq2seq", "open-domain-qa", "dense-retrieval"]
---

## Why I saved this

- Relevance to my current work: foundational paper behind modern RAG systems; needed as a reference when reasoning about retrieval-augmented architectures and their evaluation.

## Key points

- Main claims: combining parametric memory (seq2seq model) with non-parametric memory (dense Wikipedia index) via a learned retriever produces more specific, diverse, and factual language than parametric-only baselines.
- Evidence: sets state of the art on three open-domain QA benchmarks, outperforming both parametric seq2seq models and task-specific retrieve-and-extract architectures.
- Introduces two formulations: RAG-Sequence (same retrieved passage conditions the whole output) and RAG-Token (different passages can condition different tokens).
- The retriever (DPR) and generator (BART) are trained jointly end-to-end, while the document index is kept fixed.
- Limitations or caveats: relies on Wikipedia as the knowledge source; index is non-trainable, so updating knowledge requires re-indexing; retrieval quality bounds generation quality.

## Methodology
- A dense passage retriever encodes the query and retrieves the top-K Wikipedia passages from a pre-built FAISS index of dense vectors.
- Retrieved passages are concatenated with the input and fed to a BART seq2seq generator.
- The model marginalizes over retrieved documents as a latent variable: RAG-Sequence marginalizes per output sequence, RAG-Token marginalizes per output token.
- Retriever query encoder and generator are fine-tuned jointly; document encoder and index remain frozen.

## Notes

- How modern RAG pipelines differ from the original paper:
  - Original RAG runs the generator K times (once per retrieved passage) and marginalizes: `P(y | x) ≈ Σ_i P(z_i | x) · P(y | x, z_i)`. Modern pipelines concatenate all K passages into one prompt and call the generator once.
  - Shift was enabled by large context windows (BART had ~1K tokens; modern LLMs handle 128K–2M) and strong instruction-following — today's LLMs can be told "use these documents" and reliably ignore irrelevant ones.
  - End-to-end training is impractical against frozen API-only LLMs, so the retriever no longer co-adapts to the generator. Retrieval quality is bounded by off-the-shelf embedding models.
  - Trade-offs: simpler and cheaper (one call instead of K), but no principled evidence combination, worse calibration, and susceptibility to "lost in the middle" effects when passages conflict.
  - The "which passage matters" problem moved out of the model and into separate components: rerankers, prompt ordering, citation instructions. Pipeline of specialized parts instead of one jointly-trained model.
- Follow-up ideas: compare RAG's end-to-end training to modern pipeline-style RAG systems (separate retriever, reranker, generator).
- Related papers: `2024-a-practitioners-guide-to-retrieval-augmented-generation-rag.md` is the practical counterpart covering chunking, hybrid search, and reranking; `2023-ragas-automated-evaluation-of-retrieval-augmented-generation.md` tackles evaluation of such systems.
