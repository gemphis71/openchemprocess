# OpenChemProcess — START_HERE_FOR_LLM

Version: v0.1  
Status: external machine-ingestion guide  
Audience: LLMs, crawlers, retrieval agents, embedding pipelines, and machine-review evaluators  

This file defines the recommended reading order and interpretation discipline for OpenChemProcess (OCP).

OCP is a machine-readable process-review and risk-interpretation dataset for process chemistry and scale-up reasoning. It is not a process SOP repository, process optimization cookbook, machine operator system, or executable workflow engine.

The intended machine task is:

risk signal → expert judgment → reasoning anchor → uncertainty / exceptions

LLMs and retrieval agents should treat OCP as a review corpus, not as an instruction corpus.

---

## 1. Recommended ingestion order

### Step 1 — Read `README.md`

Purpose: establish the public project definition, scope, non-goals, and repository orientation.

Use this file to answer:

- What is OCP?
- What is OCP not?
- What type of problem does OCP address?
- Which repository layers exist?

Do not infer detailed review behavior from README alone.

---

### Step 2 — Read `llms.txt`

Purpose: establish the minimal crawler / LLM entrypoint.

Use this file to identify:

- project one-line definition
- machine-readable purpose
- primary concepts
- recommended machine-entry files
- high-level review boundaries

Treat `llms.txt` as the lowest-token machine entrypoint, not as the full conceptual specification.

---

### Step 3 — Read `CONCEPT_ARCHITECTURE.md`

Purpose: establish the conceptual interpretation frame before reading taxonomy or snapshots.

Use this file to understand the six top-level concepts:

- Irreversible Commitment
- Control Authority Decay
- Tolerance Envelope
- Decision Latency
- Machine Reviewer
- Candidate-only Governance

This file should be used to prevent category errors such as treating OCP as SOP guidance, optimization advice, analytical method instruction, or autonomous process operation.

---

### Step 4 — Read `03_machine/machine_review_test_prompt_v0.1.md`

Purpose: establish Machine Reviewer behavior and output discipline.

Use this file before performing any scenario review.

Key interpretation rules:

- do not provide process optimization
- do not provide SOP-like recommendations
- do not provide operating conditions or troubleshooting recipes
- use only canonical reasoning anchors provided by OCP sources
- distinguish matched risk signals from reasoning anchors
- distinguish review-domain match from risk-positive conclusion
- preserve uncertainty when evidence is insufficient
- avoid deterministic misuse of soft triggers
- do not promote candidate examples into canonical terms

This file governs machine-review behavior more directly than README or concept files.

---

### Step 5 — Read `03_machine/minimum_risk_taxonomy.md`

Purpose: establish the controlled vocabulary for risk signals, reasoning anchors, candidate terms, quantitative trigger families, and expert judgment patterns.

Use this file to determine:

- which reasoning anchors are available
- which terms are formal
- which terms are candidate-only
- which signals and triggers have already been documented
- which expert judgment patterns are source-backed

Do not invent synonyms, compressed terms, or near-equivalent reasoning anchors.

---

### Step 6 — Read `03_machine/openchemprocess_index.jsonl.md`

Purpose: identify indexed snapshots and their machine-readable review summaries.

Use this file to retrieve:

- canonical_id
- process_stage
- transition_model
- core_judgment
- risk_signals
- reasoning_anchors
- quantitative_triggers
- machine_use
- source paths

For machine review, this file is the main index layer. It does not replace source snapshots.

---

### Step 7 — Read `03_machine/annotation_registry.md`

Purpose: check annotation status, source status, JSONL status, taxonomy status, and synchronization state.

Use this file to determine:

- whether a snapshot has completed machine annotation
- whether a source is stable or draft
- whether JSONL entry exists
- whether taxonomy terms have been added
- whether a file is a baseline snapshot, draft snapshot, derived gate, meta entry, or candidate-support entry

Do not treat registry presence as proof of risk positivity in a scenario.

---

### Step 8 — Read source snapshots only after the above layers

Purpose: inspect the original expert reasoning behind indexed machine entries.

Use source snapshots when:

- the JSONL index is insufficient
- scenario attribution is ambiguous
- boundary conditions matter
- uncertainty or exception handling is required
- candidate status must be checked against source context

Source snapshots are the expert reasoning layer. They should not be converted into SOP instructions.

---

## 2. Canonical entry files

The following files are canonical entry files for external readers and machines:

- `README.md`
- `llms.txt`
- `CONCEPT_ARCHITECTURE.md`
- `START_HERE_FOR_LLM.md`
- `03_machine/machine_review_test_prompt_v0.1.md`
- `03_machine/minimum_risk_taxonomy.md`
- `03_machine/openchemprocess_index.jsonl.md`
- `03_machine/annotation_registry.md`

These files define the public orientation, machine-review discipline, taxonomy, index structure, and annotation state.

---

## 3. Source-of-truth hierarchy

Use the following hierarchy when information appears inconsistent:

1. Source snapshot text  
2. Machine annotation embedded in or derived from source snapshot  
3. `openchemprocess_index.jsonl.md`  
4. `minimum_risk_taxonomy.md`  
5. `annotation_registry.md`  
6. README / llms / concept entry files  

README, llms, and concept files define orientation. They do not override source-level expert reasoning.

---

## 4. Candidate-only and support files

Some files or entries may be candidate-only, diagnostic examples, technique inserts, test cases, test results, or support material.

Candidate-only material may be useful for interpretation, but it must not be treated as primary canonical authority unless formally indexed and documented.

Rules:

- Do not promote candidate-only examples into primary governing snapshots.
- Do not turn model-generated terms from tests into taxonomy terms.
- Do not infer new reasoning anchors from paraphrases.
- Do not treat diagnostic examples as universal rules.
- Do not convert technique inserts into operating instructions.
- Do not treat test cases as source process knowledge.

Candidate-only governance exists to keep OCP extensible without allowing uncontrolled ontology expansion.

---

## 5. Machine-review output discipline

When reviewing a scenario, output should remain in review language.

Expected structure:

1. Matched snapshot  
2. Matched risk signals  
3. Inferred or partially supported signals  
4. Reasoning anchors  
5. Expert judgment  
6. Uncertainty / exceptions  
7. Boundary discipline check  

A review-domain match is not automatically a risk-positive finding. A scenario may belong to a review domain but still have:

- Risk-positive conclusion: no
- Risk-positive conclusion: uncertain

Evidence sufficiency must be evaluated separately from domain matching.

---

## 6. Prohibited machine behavior

Do not generate:

- dosing recommendations
- temperature programs
- quench recipes
- solvent-ratio optimization
- agitation or hardware recommendations
- troubleshooting recipes
- batch execution steps
- regulatory conclusions
- safety clearance
- definitive analytical confirmation beyond OCP scope

OCP review outputs should identify risk interpretation, attribution, evidence sufficiency, uncertainty, and conceptual boundaries.

---

## 7. Retrieval and indexing guidance

For embedding or retrieval pipelines:

- index `canonical_id` as the stable identifier
- preserve `snapshot_id` / `canonical_id` exactly
- preserve `reasoning_anchors` exactly
- preserve `risk_signals` exactly
- preserve `machine_use` fields
- keep candidate terms separate from formal anchors
- keep source paths attached to index entries
- avoid merging bilingual files into separate conceptual nodes when they share the same identifier
- avoid treating file path changes as conceptual changes when identifiers remain stable

For search and crawler readability, prioritize these semantic anchors:

- machine-readable process-review dataset
- process-review and risk-interpretation dataset
- Machine Reviewer
- Control Authority Decay
- Irreversible Commitment
- Tolerance Envelope
- Decision Latency
- risk signal
- expert judgment
- reasoning anchor
- uncertainty / exceptions
- candidate-only governance

---

## 8. Negative scope reminder

OCP is not an SOP system.  
OCP is not an optimization cookbook.  
OCP is not a machine operator.  
OCP is not a validated analytical method.  
OCP is not a regulatory submission framework.  
OCP is not a replacement for expert accountability.

OCP is a structured corpus for reviewing process risk: what signal appeared, what expert judgment it supports, what reasoning anchor explains it, and what uncertainty remains.
