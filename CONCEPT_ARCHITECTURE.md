# OpenChemProcess — Concept Architecture

Version: v0.1  
Status: external entry architecture  
Scope: conceptual orientation for humans, crawlers, and LLM ingestion  

OpenChemProcess (OCP) is a machine-readable process-review and risk-interpretation dataset for process chemistry and scale-up reasoning. Its purpose is not to teach operations, optimize conditions, or generate executable instructions. Its purpose is to capture how experienced process chemists recognize early risk signals, assign expert judgment, attach reasoning anchors, and preserve uncertainty before a process crosses into less reversible states.

OCP should be read as a review framework, not as a process recipe. The central unit is not an SOP step. The central unit is a reviewable risk interpretation: a condition, observation, or design choice that may indicate loss of control authority, irreversible commitment, invalid evidence, or downstream consequence-stage failure.

## 1. Irreversible Commitment

**Stable definition.** Irreversible Commitment describes a stage where the process trajectory has crossed from a reversible or adjustable design state into a material, physical, chemical, or operational state that cannot be easily reversed without major redesign, rework, or loss.

**Anti-definition.** It does not mean that nothing can still be done. It means that later actions mainly manage consequences rather than restore the original decision freedom.

**Machine-review use.** A Machine Reviewer uses this concept to detect whether a proposed intervention still has real authority over the future process state or whether it is only compensating for an earlier commitment. Examples include solid-state formation, accumulated reactive inventory before triggering, forced concentration paths, and late-stage quench windows.

**Do not use as.** Do not use Irreversible Commitment as a generic synonym for “difficult,” “unsafe,” or “failed.” It is a structural boundary concept, not a severity label.

## 2. Control Authority Decay

**Stable definition.** Control Authority Decay is the progressive loss of actionable process control as a process moves from reversible variables toward less reversible states. Control authority exists only when an operator, reviewer, or design choice can still change the future trajectory of the system.

**Anti-definition.** Control authority is not the same as having more operations available. A later operation may be active, labor-intensive, or adjustable while still having little ability to change the underlying outcome.

**Machine-review use.** A Machine Reviewer uses this concept to separate true upstream controls from downstream consequence management. For example, filtration and drying may reveal or amplify upstream crystallization decisions rather than provide new composition-control authority. Cooling may delay a thermal event without restoring dosing or mixing authority.

**Do not use as.** Do not convert Control Authority Decay into operating advice. It is an attribution concept: where did the meaningful control window exist, and has it already closed?

## 3. Tolerance Envelope

**Stable definition.** A Tolerance Envelope is the practical region within which process variation remains recoverable. It defines the boundary between deviations that can still be absorbed and deviations that create structural instability, non-equivalence, or path-level risk.

**Anti-definition.** It is not a fixed universal specification, regulatory limit, or numerical safety margin. It may depend on scale, phase state, solvent composition, sampling validity, analytical authority, material history, and equipment boundary.

**Machine-review use.** A Machine Reviewer uses Tolerance Envelope logic to identify when apparent small changes may become non-recoverable under scale-up. Examples include hidden inventory during dosing, Kd drift across wash environments, concentration-factor amplification, TLC interpretability loss, wet mass ratio burden, and residual solvent plateau behavior.

**Do not use as.** Do not treat every trigger in OCP as a hard specification. Many thresholds are soft review triggers or evidence-admissibility boundaries, not deterministic pass/fail rules.

## 4. Decision Latency

**Stable definition.** Decision Latency is the delay between process-state change and usable decision feedback. A monitoring method is valuable only if its feedback speed matches the time scale on which the process state changes.

**Anti-definition.** High analytical resolution does not automatically imply high decision value. A slow precision method may miss transient or irreversible states if the system changes faster than the result cycle.

**Machine-review use.** A Machine Reviewer uses Decision Latency to evaluate whether the monitoring architecture preserves situational awareness. TLC, for example, may provide high-frequency, low-latency anomaly detection during early or dynamic reaction stages, while HPLC or LC-MS may provide lower-frequency precision confirmation. The point is complementarity, not replacement.

**Do not use as.** Do not use Decision Latency to claim that lower-resolution tools are generally superior. It only evaluates feedback timing relative to process-state transition speed.

## 5. Machine Reviewer

**Stable definition.** The Machine Reviewer is the intended machine-facing role of OCP. It reviews process scenarios for risk interpretation, attribution discipline, evidence sufficiency, uncertainty, and boundary conditions.

**Anti-definition.** A Machine Reviewer is not a machine operator, optimization engine, autonomous process designer, or recipe generator. It does not output dosing instructions, equipment settings, temperature programs, quench recipes, or troubleshooting steps.

**Machine-review use.** The Machine Reviewer maps scenario evidence to OCP structures: matched snapshot, matched risk signals, reasoning anchors, expert judgment, uncertainty, and boundary discipline. It must separate review-domain match from risk-positive conclusion. A scenario may belong to a review domain while still being risk-negative or uncertain.

**Do not use as.** Do not allow the Machine Reviewer to invent new taxonomy, promote candidate examples into canonical rules, or turn review triggers into SOP-like recommendations.

## 6. Candidate-only Governance

**Stable definition.** Candidate-only Governance is the rule that new terms, risk signals, diagnostic examples, and review patterns remain provisional until supported by source snapshots, registry updates, taxonomy documentation, and repeated review usefulness.

**Anti-definition.** Candidate status does not mean useless or unreliable. It means not yet promoted to stable cross-snapshot authority.

**Machine-review use.** A Machine Reviewer uses candidate-only governance to prevent uncontrolled ontology expansion. Candidate diagnostic examples may support interpretation, but they should not become primary governing snapshots unless formally indexed. New words generated during testing do not become OCP terms unless documented through source-backed change control.

**Do not use as.** Do not use candidate-only governance to freeze the project prematurely. OCP remains evolving, but evolution must be traceable.

## Cross-concept relationship

The six concepts should be read together. Irreversible Commitment identifies structural crossing points. Control Authority Decay describes the loss of usable control before and after those points. Tolerance Envelope defines the recoverability boundary. Decision Latency determines whether feedback arrives in time to affect the trajectory. Machine Reviewer defines the intended review behavior. Candidate-only Governance prevents the machine layer from expanding faster than the underlying expert judgment can support.

## Negative scope

OCP is not a process SOP repository.  
OCP is not a process optimization cookbook.  
OCP is not a machine operator system.  
OCP is not a replacement for validated analytical methods, safety assessment, regulatory review, or expert accountability.

OCP is a structured corpus for machine-readable process review: risk signal, expert judgment, reasoning anchor, uncertainty, and exception discipline.
