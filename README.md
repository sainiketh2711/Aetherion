# AETHERION 2.0 — Document Intelligence Workstation

Aetherion is a browser-based, evidence-first document research assistant built with deterministic classical-AI and information-retrieval techniques. It extracts readable content from supported files, preserves source locations, indexes passages, retrieves candidate evidence and composes structured answers from those passages.

## Capabilities
- Multi-file upload: PDF, DOCX, PPTX and TXT (30 MB request limit).
- Page/slide provenance, Word tables and headers/footers, PowerPoint tables, grouped-shape text and speaker notes where available.
- Sentence/line knowledge units with searchable source archive.
- BM25-style lexical retrieval, deterministic morphology normalisation, fixed synonym/alias expansion, intent classification and source-diverse evidence selection.
- Evidence-backed explanations, overviews, comparisons, lists, follow-ups and batch questions.
- Source trail, matched terms and inspectable reasoning trace.
- Document briefing, question matrix (up to 50 questions), file removal and workspace clearing.
- PDF, DOCX, TXT and CSV exports.
- Command palette (Ctrl/Cmd + K), keyboard navigation and copy actions.
- Cinematic motion system with animated ingestion, processing stages, evidence reveals, orbiting core, layered transitions and reduced-motion support.

## Classical-AI boundary
Aetherion uses deterministic tokenisation, a fixed stop-word list, explicit synonym rules, BM25-style lexical ranking, hand-authored intent rules, symbolic patterns and extractive answer templates. It does **not** use LLM APIs, generative models, learned embeddings, vector databases, RAG frameworks or learned NLP pipelines.

This design is inspectable and source-grounded, but it is not equivalent to a generative assistant. Unseen synonyms, complex implicit references, images, charts, scanned pages and ambiguous questions can still require user clarification or remain unsupported. Aetherion should abstain when it cannot find adequate evidence.

## Run locally
Python 3.10 or newer is recommended.

```bash
python -m venv .venv
# Windows PowerShell
.venv\Scripts\Activate.ps1
# macOS / Linux
source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

Open http://127.0.0.1:5000.

## Tests
```bash
python -m unittest discover -s tests -v
```

The included automated suite currently contains 29 passing tests for retrieval, paraphrases covered by the explicit synonym rules, follow-ups, overviews, source provenance, unknown questions and existing rule-based workflows. These tests are not a guarantee of correctness for every document or every possible question. A representative external-document benchmark and browser-level testing are still required.

## Deployment notes
The demo workspace is process-local memory. Restarting the server clears it. A public multi-worker deployment needs durable per-user storage, a production secret key, secure session handling, authentication, rate limiting and privacy controls. Set `SECRET_KEY` in the deployment environment.

## Extraction limitations
Scanned/image-only PDFs are not OCR-processed. Text contained only in images, diagrams or charts is not interpreted. PDF extraction depends on embedded text; PowerPoint notes and grouped shapes are extracted where supported by the file structure. Always inspect the Source archive after ingestion.
