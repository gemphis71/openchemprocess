
derived_from: WRKUP-001-WORKUP-CONTROL-AUTHORITY
role: derived-decision-gate
scope: workup / quench only
status: draft
note: This file introduces no new process knowledge. It is a rejection checklist only.

---

# WRKUP-001｜Quench Control  
## Machine-Review Checklist (One Page)

> **Purpose**  
> This checklist is used to determine whether  
> **the current process is allowed to proceed beyond the workup / quench stage  
> (e.g. scale-up, extraction, purification).**
>
> **Rule**  
> If **any** rejection condition is triggered → **REJECT**  
> This checklist provides **no optimization or remediation guidance**.

---

## A｜Is the quench designed as a *completable chemical reaction*?
(Chemically Incomplete Quench)

- A1. At the nominal end of the reaction, does the system remain in any of the following states?  
  ☐ Reactive intermediates  
  ☐ Metallic / organometallic complex states  
  ☐ Reversible catalytic systems  
  ☐ Non-stable end states requiring further transformation

- A2. If A1 = YES, has the quench reaction been **explicitly designed and validated** with respect to:  
  ☐ Required time  
  ☐ Required temperature  
  ☐ Required chemical conditions (e.g. pH, redox environment)

- A3. Is “quench completion” defined based on:  
  ☐ Chemical deactivation or transformation of reactive species  
  ☐ Formation of a chemically stable final state  
  rather than solely on:  
  ☐ Addition of the quench reagent  
  ☐ Completion of an operational step

**Rejection Conditions**  
- A1 = YES and any item in A2 = NO  
- or A3 is not satisfied  

→ **REJECT (Chemically Incomplete Quench)**

---

## B｜Does a *reactive window* exist during quenching?
(Partial Quench / Critical Time Window)

- B1. From the start of quenching until complete deactivation, does the system pass through any reactive window?  
  ☐ Basic window  
  ☐ Acidic window  
  ☐ Active metal / highly reactive complex window

- B2. Under scale-up conditions, is this window significantly elongated due to:  
  ☐ Slower addition rate  
  ☐ Reduced mixing or mass transfer efficiency  
  ☐ Non-equivalence between early-stage and late-stage quench conditions

- B3. Is quench success judged only by:  
  ☐ Final pH meeting specification  
  ☐ Final analytical results being acceptable  
  **without** ensuring the absence of a reactive window from t = 0?

**Rejection Conditions**  
- B1 = YES and B2 = YES  
- or B3 = YES  

→ **REJECT (Loss of Control in Critical Time Window)**

---

## C｜Is the quench reagent *physically accessible* under scale-up conditions?
(Physically Inaccessible Quench)

- C1. Under the target scale-up temperature and addition mode, does any of the following risks exist?  
  ☐ Freezing or partial freezing of the quench reagent  
  ☐ Obvious phase separation or interfacial isolation  
  ☐ Failure of the quench reagent to enter the reaction phase

- C2. Has physical accessibility under scale-up conditions been **explicitly validated at lab scale**  
  (i.e. not relying on rapid dumping or ideal mixing assumptions)?

**Rejection Conditions**  
- C1 = YES and C2 = NO  

→ **REJECT (Physically Inaccessible Quench)**

---

## Final Decision

- ☐ **PASS** — Allowed to proceed to subsequent steps  
- ☐ **REJECT** — Must roll back to workup / quench design

---

## #Audit

> The sole function of this checklist is to prevent  
> **any downstream processing from proceeding  
> when the quench has not been designed and validated  
> as a completable chemical reaction.**
