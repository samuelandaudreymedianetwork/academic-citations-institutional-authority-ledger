# Data Dictionary: Academic Citations & Institutional Authority Ledger

This document defines the schema for the structural files within this repository, specifically the `.csv` and `.jsonl` formats.

| Column / Field | Type | Description |
| :--- | :--- | :--- |
| `cite_id` | `string` | Stable, unique citation identifier (e.g., `nexus-cite-edgeworth`). |
| `record_key` | `string` | Short normalized key used for internal grouping and database indexing. |
| `title` | `string` | The primary entity, institution, or publisher granting the citation. |
| `headline` | `string` | The specific headline, item title, or paper name where the citation occurs. |
| `publisher` | `string/null` | The parent publisher or outlet name (if distinct from the title). |
| `canonical_url` | `string` | The primary, click-verifiable source link for the record. |
| `evidence_url` | `string/null` | An optional secondary verification link or archive URL. |
| `meta` | `string/null` | Short metadata string captured from the citation block. |
| `badge` | `string/null` | On-page categorization marker (e.g., "Economic Theory Citation"). |
| `date_published` | `string/null` | ISO-8601 formatted date if present on the source document. |
| `commentary_label` | `string/null` | Optional categorization label for the commentary segment. |
| `commentary_text` | `string/null` | Curated editorial commentary providing context for the citation's E-E-A-T value. |
| `section_titles` | `string/null` | The specific ledger section heading where the record is categorized. |
| `nexus_texts` | `string` | The main descriptive narrative explaining the citation and its relevance. |
| `data` | `string/null` | A JSON-formatted string containing key/value metadata specific to the block. |
| `jsonld_type` | `string/null` | The inferred or extracted Schema.org type (e.g., `Report`, `ItemList`, `ScholarlyArticle`). |

*Note: Null values indicate that the specific metadata field was not applicable or not present in the original source block.*
