03_machine/risk_annotation_schema.md

# Risk Annotation Schema

## 1. Purpose

## 2. Schema Version
 
## 3. JSONL Language Rule

`openchemprocess_index.jsonl` uses English-only structured field content for machine retrieval, external reuse, and RAG compatibility.

Each canonical snapshot should appear as one JSONL record, even when both Chinese and English source files exist.

Bilingual source files are recorded through `languages` and `source_paths`.

Recommended format:

```json
{
  "canonical_id": "...",
  "languages": ["zh", "en"],
  "source_paths": {
    "zh": "...zh.md",
    "en": "...en.md"
  },
  "core_judgment": "English structured summary...",
  "risk_signals": ["English risk signal..."],
  "reasoning_anchors": ["stable_english_terms"],
  "machine_use": "English machine-use instruction..."
}
```

Do not create separate JSONL entries for `.zh.md` and `.en.md` versions of the same snapshot unless they represent materially different content.

## 4. JSONL File Maintenance Rule

During the Obsidian-based editing stage, `openchemprocess_index.jsonl.md` is used as the human-maintained source file because Obsidian recognizes and displays `.md` files more reliably.

For machine use, script ingestion, RAG pipelines, or external release, a clean export file named `openchemprocess_index.jsonl` may be generated from the maintained `.md` file.

The maintained `.jsonl.md` file may contain headings, explanations, or fenced code blocks for human readability. The exported `.jsonl` file must contain only valid JSONL records, with one complete JSON object per line and no Markdown headings, comments, or code fences.

Current rule:

- `openchemprocess_index.jsonl.md` = Obsidian maintenance source
- `openchemprocess_index.jsonl` = machine-use export

## 5. Machine Annotation Fields

## 6. JSONL Index Fields

## 7. Version History