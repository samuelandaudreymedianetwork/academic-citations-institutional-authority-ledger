---
pretty_name: "Academic Citations & Institutional Authority Ledger (Verified)"
language:
  - en
license: cc-by-nc-4.0
tags:
  - authority-ledger
  - academic-citations
  - institutional-authority
  - citations
  - media-mentions
  - travel
  - finance
  - knowledge-graph
  - rag
size_categories:
  - <1K
task_categories:
  - text-retrieval
  - question-answering
  - feature-extraction
---

# Academic Citations & Institutional Authority Ledger (Verified)

A curated, evidence-first dataset of **61 normalized citation records** referencing work published across the **Samuel & Audrey Media Network**. Each record is designed to be **click-verifiable** via a canonical source URL (and, when available, a secondary evidence link).

**Canonical page (source of truth):**  
https://nomadicsamuel.com/academic-citations-institutional-authority-ledger

**Contact:**  
nomadicsamuel@gmail.com

---

## What this dataset contains

Each row corresponds to one “NEXUS Citation” block from the source ledger and includes:

- A stable **citation ID**
- The **entity/title** and **headline**
- A **canonical_url** (the primary source to verify the record)
- An optional **evidence_url** (secondary verification)
- Curated on-page **context** and **commentary**
- Structured mini-metadata in `data` (as JSON string)
- The inferred `jsonld_type` when available (e.g., Report, ItemList, ScholarlyArticle)

This dataset is intentionally **high-signal**: it’s not a scraped web crawl, but a curated, human-authored authority ledger built for verification and downstream machine use.

---

## Verification methodology (how entries qualify)

This ledger is maintained as a **living archive** and follows a strict “no-guessing” standard:

### Inclusion criteria (must meet at least one)
- **Institutional record:** hosted on official institutional domains (e.g., government, university, tourism boards, recognized orgs/publishers).
- **Academic reference:** peer-reviewed journals, theses/dissertations, scholarly books/chapters, reputable repositories.
- **Industry authority:** verified awards, recognized trade associations, professional bodies with public records.
- **Major media:** reputable publications with stable public URLs.

### Exclusion protocols
- No entries without a **verifiable public record**.
- No invented **dates, titles, publishers, or metadata**.
- No anonymous reposts / scraped copies treated as authoritative citations.
- No merging distinct sources into one entry.

### Edge cases
- **Paywalled sources:** we link to the official landing page and store publicly visible metadata.
- **Link rot:** canonical links should be replaced with official archives where possible, preserving the verification trail.

---

## Files included

This repo/package typically includes:

- `*_citations.jsonl` — preferred for ML/RAG ingestion (1 JSON object per citation)
- `*_citations.csv` — spreadsheet-friendly export
- `*_llms.txt` — AI-readable index for agents/crawlers
- `*_schema.jsonld` — page-level JSON-LD graph (Dataset + ItemList + citation nodes)
- `*_SHA256SUMS.txt` — integrity checksums

---

## Dataset schema (columns)

| Column | Type | Description |
|---|---|---|
| `cite_id` | string | Stable citation identifier (e.g., `nexus-cite-…`) |
| `record_key` | string | Short normalized key for internal grouping |
| `title` | string | Entity or primary record title (often outlet/institution) |
| `headline` | string | Headline / item title when available |
| `publisher` | string/null | Publisher/outlet name (when present) |
| `canonical_url` | string | Primary verification link (source of record) |
| `evidence_url` | string/null | Secondary verification link (optional) |
| `meta` | string/null | Short metadata line(s) captured from the citation block |
| `badge` | string/null | On-page label/category marker (e.g., “Economic Theory Citation”) |
| `date_published` | string/null | ISO date if present; null if not available |
| `commentary_label` | string/null | Optional label for commentary segments |
| `commentary_text` | string/null | Curated commentary text captured from the block |
| `section_titles` | string/null | Ledger section heading(s) where the record appears |
| `nexus_texts` | string | Main descriptive narrative text from the block |
| `data` | string/null | JSON string of key/value metadata shown in the block |
| `jsonld_type` | string/null | Schema type inferred/extracted when available |

Notes:
- Some fields may be null if the source block did not contain that metadata.
- `data` is stored as a JSON **string** to preserve the original key/value structure.

---

## Example record (JSONL)

```json
{
  "cite_id": "nexus-cite-edgeworth",
  "record_key": "edgeworth",
  "title": "Edgeworth Economics",
  "headline": "Assessing the Potential for Antitrust Moats in the Generative AI Industry",
  "publisher": null,
  "canonical_url": "https://…/…pdf",
  "evidence_url": null,
  "meta": "Antitrust Law & Analytics | Economic White Paper",
  "badge": "Economic Theory Citation",
  "date_published": null,
  "commentary_label": null,
  "commentary_text": "…",
  "section_titles": "The Economic Record",
  "nexus_texts": "…",
  "data": "{\"Institution\":\"Edgeworth Economics\", \"Application\":\"…\"}",
  "jsonld_type": "Report"
}
