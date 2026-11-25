# AETHERION 2.0 Architecture

## Request flow
1. Browser interface accepts files and natural-language questions.
2. Flask validates file types and size, then calls format-specific extraction.
3. Extracted content is segmented into source-linked knowledge units with page/slide metadata.
4. The query processor applies deterministic tokenisation, stop-word removal, light morphology normalisation, aliases and intent rules.
5. The retrieval engine computes BM25-style lexical relevance, direct-term coverage and phrase/alias boosts.
6. Evidence selection removes duplicate passages and preserves source diversity.
7. Explicit reasoning rules may handle supported symbolic/domain patterns.
8. Fixed answer templates compose overviews, explanations, comparisons, lists and direct evidence responses.
9. The API returns the answer, supporting passages, confidence indicator and inspectable trace.

## Components
- `app.py`: Flask routes, in-memory workspace, validation, API and exports.
- `src/engine.py`: extraction, tokenisation, BM25-style ranking, intent classification, evidence selection and answer composition.
- `src/question_processor.py`: deterministic query processing.
- `src/reasoning_engine.py` and `src/reasoning_rules.py`: explicit symbolic rules.
- `src/knowledge_base.py`: structured knowledge representation.
- `templates/index.html`: interface structure.
- `static/style.css`: responsive visual system, interaction states and motion design.
- `static/script.js`: upload, navigation, processing states, questions, evidence, batch and export interactions.

## Retrieval design
BM25-style scoring uses term frequency, inverse document frequency and document-length normalisation. Query aliases and deterministic suffix normalisation broaden matching without a learned semantic model. Ranking scores are calibrated so a weak single-term match does not automatically become a perfect score merely because it is the best available candidate. Intent-specific selection handles broad overviews separately from focused questions.

## Design principle
A cinematic editorial research desk with a mineral-green/charcoal foundation, antique-gold accents, an animated astrolabe core, active ingestion and analysis states, progressive evidence reveals and responsive transitions. Motion is informative and respects `prefers-reduced-motion`.

## Limitations and deployment
This is a classical lexical and rule-based system, not a generative language model. It cannot guarantee robust interpretation of every paraphrase, deceptive premise, implicit multi-hop question or visual-only content. The active workspace is process-local memory; server restarts clear it. Multi-worker deployments require durable storage and session isolation. Configure `SECRET_KEY` outside source control.
