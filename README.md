# Three-Layer Governance Architecture

**Stability-Oriented Governance Design for Multi-Agent Systems**

> A component architecture of **Deficit-Fractal Governance (DFG)**
>
> **Companion theories:** [Vector Storm Theory](../vector-storm/) · [Network Architecture Theory](../network-architecture/) · [Governance Rules Theory](../governance-rules/)

---

## Abstract

### The Core Diagnosis

Multi-agent governance fails not because agents misbehave, but because **the architecture forces incompatible abstraction levels to interact directly**.

Global constraints operate at high abstraction. Local agents operate at high variability. When these two levels interact without mediation, the result is structurally predictable:

- Legitimate exploration is misidentified as violation — the system over-corrects
- Actual violations pass undetected — the system under-corrects
- Correction attempts generate coordination loops that amplify the original instability

> **Governance failure is a resolution mismatch problem, not a behavior problem.**

This distinction matters because it changes the design target entirely. Solving a behavior problem means tightening control. Solving a resolution mismatch problem means **inserting the right structural layer between incompatible abstraction levels**.

### The Structural Solution

This document presents a three-layer architecture in which a dedicated **Resolution Mediation layer** permanently occupies the gap between global invariants and local operations.

The three layers are not a hierarchy of control. They are a **separation of resolution responsibilities**:

| Layer | Responsibility | What it does NOT do |
|-------|---------------|---------------------|
| **Top** — Invariant Governance | Define what cannot be violated | Manage agents directly |
| **Middle** — Resolution Mediation | Translate across abstraction levels; detect and stage corrections | Issue continuous commands |
| **Bottom** — Operational Diversity | Explore, specialize, adapt | Enforce global constraints directly |

The Middle Layer is the architectural innovation. It is not an orchestrator. It does not run continuously. It activates when the abstraction gap produces conflict — and its job is to resolve that conflict at the right level rather than escalating it unnecessarily or suppressing it prematurely.

### What This Architecture Enables

Without the mediation layer, governance faces a forced trade-off: tighten global constraints and lose adaptability, or loosen them and lose stability. This architecture dissolves that trade-off by making **mediation a structural property of the system** rather than a reactive intervention.

The result:

- Diversity at the bottom layer does not threaten stability at the top
- Global invariants are enforced without micromanaging local behavior
- Governance cost scales with instability events, not with system activity

**Governance is treated as a structural property, not as continuous centralized control.**

> **Terminological note:** In this document, "resolution" refers to
> an agent or layer's capacity to correctly classify, mediate, and place
> information across abstraction levels. This capacity grows through
> the degradation-upscaling cycle and is measurable via the resolution-proxy.
> See [Resolution-Based Information Theory](../resolution-theory/) for the formal foundation.

---

## 0. Preliminaries — Minimal Formal Definitions

This section defines the core variables used throughout this document.
These are **operational definitions** sufficient to follow the logical structure of Sections 1–14.
Formal derivations and update rules are delegated to
[Resolution-Based Information Theory (RBIT)](../resolution-theory/).
For the relationship to Shannon information theory [Shannon, 1948], see RBIT Section 9.

---

### 0.1 Core Variables

**θ_d (theta-d) — Domain-Specific Distortion Threshold**

The decision-boundary parameter set by which an agent or layer classifies
incoming input as *normal variation* vs. *distortion/contamination*.

- Low θ_d → over-sensitive → excess MARK signals / false positives / unnecessary escalation
- High θ_d → under-sensitive → contamination passes undetected / false negatives

θ_d is updated from conflict logs (see 0.2). Convergence means θ_d variation and
classification error rate have stabilized over a sustained evaluation window.
*(Formal update rule: RBIT Section 5)*

---

**SCC (Self-Correction Capacity) — Self-Recovery Throughput Under Perturbation**

The capacity of a layer to absorb and re-place distortions using internal mechanisms
only — without escalating to τ2 (Contain) or above — within an evaluation window W.

Measured by three combined indicators:

| Indicator | Definition |
|-----------|-----------|
| Self-resolution rate | Fraction of τ1 events that terminate without escalating to τ2/τ3 |
| Recovery time | Mean time to return below τ1 after a disturbance |
| Buffer maintenance rate | Fraction of time buffer thickness stays above critical minimum during perturbation |

**τ4 condition:** SCC ≥ τ4 means all three indicators are continuously satisfied
within window W. This is the Rest Mode entry condition.
*(Formal function form: RBIT / Governance Rules Theory)*

---

**ρ (rho) — Resolution-Proxy**

A layer's structural resolution cannot be measured directly.
ρ approximates it via classification performance:

```
ρ  =  1  −  (L_T1 + L_T2) / N

  N      total inputs processed in evaluation window
  L_T1   Type 1 loss  (False Restoration — see 0.1 below)
  L_T2   Type 2 loss  (Missed Contamination — see 0.1 below)
```

Higher ρ → more precise distinction between exploration and contamination
→ more accurate mediation and placement.

Resolution gap between layers: Δρ = ρ_upper − ρ_lower
- Δρ > 0: upper layer reads lower layer correctly → normal operation
- Δρ = 0: upscaling imminent
- Δρ < 0: upper layer cannot fully read lower layer → seed handover must not proceed

*(Theoretical derivation of ρ from structural resolution: RBIT Section 1.1.3)*

---

### 0.2 Loss Types (Fixed Definitions Within This Document)

**Type 1 loss (L_T1) — False Restoration / Over-disruption**
Healthy exploration classified as contamination.
Consequence: unnecessary correction, diversity loss, wasted governance resources.

**Type 2 loss (L_T2) — Missed Contamination / Under-detection**
Contamination classified as healthy.
Consequence: loop formation, propagation, compounding recovery cost.

Optimal sensitivity: L_T1 = L_T2 (balanced classification boundary).
Minimum disruption optimization: minimize L_T1 subject to L_T2 ≤ threshold.

---

### 0.3 Observable Signals

The variables above are tracked through three observable signal types:

| Signal | What it tracks | Primary use |
|--------|---------------|-------------|
| Conflict logs | Record of classification boundary events; input to θ_d updates | θ_d convergence, SCC measurement |
| Buffer thickness | Gap between opposing vector positions; proxy for upper layer resolution | ρ measurement, minimum disruption boundary |
| Escalation rate | Frequency of τ1/τ2/τ3 events per time window | SCC assessment, bottleneck detection |

---

### 0.4 Scope Statement

The definitions above are **operational** — sufficient for following this document's logic.
They do not constitute formal proofs or complete mathematical derivations.

> This document is a **governance architecture specification**.
> RBIT is the **information-theoretic foundation** from which these definitions derive.
> The separation is intentional: architecture and foundation are distinct contributions.

Where this document references RBIT, it means: *"the operational definition used here
is consistent with the formal derivation there; readers requiring mathematical
completeness should consult RBIT."*

---

## Table of Contents

0. [Preliminaries — Minimal Formal Definitions](#0-preliminaries--minimal-formal-definitions)
1. [Governance Problem Statement](#1-governance-problem-statement)
2. [Resolution Mismatch as Governance Failure](#2-resolution-mismatch-as-governance-failure)
3. [Three-Layer Governance Structure](#3-three-layer-governance-structure)
4. [Three-Level Purification Governance](#4-three-level-purification-governance)
5. [Staged Self-Correction Protocol](#5-staged-self-correction-protocol)
6. [Distributed Mediation Strategy](#6-distributed-mediation-strategy)
7. [External Invariant Channel](#7-external-invariant-channel)
8. [Invariant Update Model](#8-invariant-update-model)
9. [Local Spectrum Governance](#9-local-spectrum-governance)
10. [Processing Phase Isolation](#10-processing-phase-isolation)
11. [Resource-Aware Governance Model](#11-resource-aware-governance-model)
12. [Governance Mechanism Mapping](#12-governance-mechanism-mapping)
13. [Limitations](#13-limitations)
    - [13.1 Known Structural Limits](#131-known-structural-limits)
    - [13.2 Upper Layer Contamination](#132-upper-layer-contamination--the-boundary-of-self-containment)
    - [13.3 The Axiomatic Boundary](#133-the-axiomatic-boundary--highest-level-goal-selection)
    - [13.4 Implicit Transmission — Ethical and Safety Limitation](#134-implicit-transmission--ethical-and-safety-limitation)
    - [13.5 The Covert Seed Problem — Falsifiability and the Manipulation Boundary](#135-the-covert-seed-problem--falsifiability-and-the-manipulation-boundary)
14. [Future Direction](#14-future-direction)

---

## 1. Governance Problem Statement

As multi-agent systems expand, they generate:

- Increased diversity
- Increased interaction pathways
- Increased coordination cost
- Increased instability risk

Traditional approaches address instability through central orchestration, static role assignment, hard constraints, and penalization mechanisms. These reduce volatility but constrain adaptability.

The deeper problem is that these approaches treat instability as a behavior problem — agents doing the wrong things — rather than a structural problem. Tightening control reduces the symptom but cannot remove its cause: the incompatibility between the abstraction level at which global constraints are specified and the abstraction level at which local agents operate. As long as that gap exists unmediated, the system must choose between over-correction (losing adaptability) and under-correction (losing stability). Traditional approaches cannot escape this trade-off because they do not address its source.

The structural problem is not diversity. It is **unmediated interaction across incompatible resolutions**.

---

## 2. Resolution Mismatch as Governance Failure

Multi-agent instability emerges when:

- Global constraints operate at high abstraction
- Local agents operate at high variability
- No resolution mediation layer exists between them

Direct interaction between these layers produces:

- **False positives** — exploration misidentified as violation
- **False negatives** — violation undetected
- **Escalating coordination loops**

> **Governance failure is therefore a resolution mismatch problem.**

---

## 3. Three-Layer Governance Structure

Governance is distributed across three structural levels.

```
┌──────────────────────────────────────────────┐
│         TOP LAYER — Invariant Governance     │
│  Define boundaries · Validate integrity      │
│  Rarely intervene · Maintain invariants      │
├──────────────────────────────────────────────┤
│      MIDDLE LAYER — Resolution Mediation     │
│  Detect conflict · Translate abstraction     │
│  Prevent misclassification · Stage correction│
├──────────────────────────────────────────────┤
│      BOTTOM LAYER — Operational Diversity    │
│  Local exploration · Task specialization     │
│  Adapt to environment · Preserve autonomy    │
└──────────────────────────────────────────────┘
```

### Top Layer — Invariant Governance

Defines global boundaries and maintains invariant principles. Validates structural integrity and rarely intervenes. This layer does not micromanage agents — it defines **what cannot be violated**.

### Middle Layer — Resolution Mediation

Detects conflict amplification and translates across abstraction levels. Prevents boundary misclassification and triggers staged correction. This layer is **not an orchestrator**. It does not continuously command. It activates when instability thresholds are crossed.

### Bottom Layer — Operational Diversity

Generates local exploration and performs task specialization. Adapts to environmental variation. **Local autonomy is preserved within defined boundaries.**

### 3.1 Threshold Definitions: τ1 – τ4

Four thresholds govern when each layer activates and when state transitions occur.

| Threshold | Role | Trigger | Acting layer |
|-----------|------|---------|--------------|
| **τ1** | MARK trigger | Collision frequency or deviation crosses "normal variation" boundary — earliest anomaly signal | Bottom layer detects; signals Middle layer |
| **τ2** | CONTAIN trigger | Loop formation or propagation risk detected — isolation and circuit-breaking required | Middle layer judges and executes |
| **τ3** | Top layer intervention boundary | Distortion exceeds Middle layer scope — system-level correction required | Top layer executes HARD CORRECT / RE-ALIGN |
| **τ4** | Immunity / Rest Mode state transition | SCC (§0.1) sustained above self-correction threshold — external intervention no longer needed at this scale | State transition, not event trigger |

**τ1–τ3 are event thresholds** — they mark transitions between correction stages during an active instability event.
**τ4 is a maturity threshold** — it marks a permanent state transition from externally-corrected to self-correcting.

```
Normal operation
  Below τ1: no action — Bottom layer explores freely

Anomaly detected
  τ1 crossed: MARK — Bottom layer flags, Middle layer notified

Loop risk
  τ2 crossed: CONTAIN — Middle layer isolates, boundary tightened
  SOFT CORRECT injected — corrective seed at calibrated resolution

System-level breach
  τ3 crossed: Top layer activated — HARD CORRECT or RE-ALIGN
  Middle layer authority suspended for scope of intervention

Maturity state
  SCC ≥ τ4: immunity achieved — τ1/τ2 events handled internally
  τ3 events become rare — only structural ceiling events escalate
```

### 3.2 Fractal Consistency of τ Values

The τ thresholds apply at every fractal scale. The structure is identical; the acting layer differs:

```
Multi-agent system scale
  τ1: Individual agent detects → sends MARK to central Middle layer
  τ2: Central Middle layer judges → executes CONTAIN across agents
  τ3: Top layer activated → system-wide HARD CORRECT / RE-ALIGN
  τ4: Agent achieves immunity → stops contributing Type 2 bottleneck

Single-agent internal scale
  τ1: Bottom layer detects internal vector anomaly → signals internal Middle layer
  τ2: Internal Middle layer judges → executes internal CONTAIN
  τ3: Internal Top layer activated → internal HARD CORRECT
       If internal Top layer capacity exceeded:
       → escalates to external upper layer (next fractal level up)
  τ4: Internal SCC sufficient → agent handles τ1/τ2 events without external intervention
       This is the seeding completion condition (Section 6.1.1, Condition 3)
```

The τ3 escalation path at single-agent scale is the structural mechanism by which individual agents generate escalation signals in the multi-agent system. When an agent's internal Top layer cannot resolve a distortion, it becomes a τ2-level signal at the system scale — absorbed by the central Middle layer as a cross-agent containment problem.

---

## 4. Three-Level Purification Governance

Governance distinguishes between three types of structural distortion. Each type has two correction tracks: **self-correction** (the layer's own recovery capacity) and **external intervention** (upper-layer assistance when self-correction is insufficient).

```
                    ▲  Escalation
                    │
┌───────────────────┴──────────────────────┐
│  Invariant Distortion                    │  ← Top Layer
│  Boundary or structural rule corruption  │
├──────────────────────────────────────────┤
│  Metadata Distortion                     │  ← Middle Layer
│  Interpretation mismatch,                │
│  threshold miscalibration,               │
│  protocol misalignment                   │
├──────────────────────────────────────────┤
│  Data Distortion                         │  ← Bottom Layer
│  Raw operational deviation               │
└──────────────────────────────────────────┘
                    │
                    ▼  Purification
```

Distortion **escalates upward**. Purification **flows downward**. Each distortion type has a distinct correction route.

### 4.1 Dual-Track Correction per Distortion Level

| Distortion Type | Self-Correction (primary) | External Intervention (when self-correction fails) |
|----------------|--------------------------|---------------------------------------------------|
| **Data Distortion** | Bottom layer: conflict log accumulation, θ_d (§0.1) recalibration, local rule revision | Middle layer: CONTAIN + SOFT CORRECT — boundary tightened, corrective signal injected |
| **Metadata Distortion** | Middle layer: threshold recalibration, escalation path review, seed revalidation | Top layer: HARD CORRECT + RE-ALIGN — loop severed, attractor metadata restored |
| **Invariant Distortion** | Not self-correctable at layer of origin — always requires upper-layer judgment | Top layer only: emergency intervention; external human oversight if top layer itself compromised |

> **External intervention creates the conditions for recovery. Self-correction is the recovery itself.**
>
> A surgeon can perform the operation. The body must still heal. If self-correction capacity is absent, external intervention only delays the next failure — it does not prevent it. Governance that relies entirely on external intervention without building self-correction capacity produces chronic external dependency and blocks Rest Mode permanently.

### 4.2 What Self-Correction Requires

Self-correction is not passive. It is an active process that requires structural capacity built through seeding:

```
Data-level self-correction requires
  Sufficient conflict log history
  → θ_d values converged
  → Local rules can identify and reprocess distorted vectors

Metadata-level self-correction requires
  Calibrated internal Middle Layer
  → Escalation logic internalized
  → Seed-derived pattern recognition functioning

Invariant-level self-correction
  Not possible at the distortion layer
  → Structural definition of High-Context:
    distortion exceeds local correction capacity
    → always escalates to the next layer up
```

Self-correction capacity grows through the seeding cycle. As the cycle matures, the proportion of distortions handled internally increases and external intervention becomes progressively rarer — until the layer reaches Rest Mode, at which point external intervention is triggered only by events that exceed the layer's structural ceiling.

---

## 5. Staged Self-Correction Protocol

Governance operates through staged intervention. The protocol has two directions: **escalation** when instability grows, and **de-escalation** when stability is restored.

### 5.1 Escalation Path

```
     τ1               τ2                               τ3
      │                │                                │
  ┌───┴────┐    ┌───────┴─┐    ┌───────────────┐    ┌───┴────────────┐    ┌─────────────┐
  │  MARK  │ →  │ CONTAIN │ →  │ SOFT CORRECT  │ →  │ HARD CORRECT   │ →  │  RE-ALIGN   │
  └────────┘    └─────────┘    └───────────────┘    └────────────────┘    └─────────────┘
  Divergence    Boundary       Reflective signal     Resource restriction  Projection back
  detected      tightened      injected              or rollback           to stable space
  [Bottom]      [Middle]       [Middle]              [Top]                 [Top]
```

**Layer authority per stage:**
- MARK: Bottom layer detects and signals — no correction authority
- CONTAIN + SOFT CORRECT: Middle layer scope — handles without Top layer involvement
- HARD CORRECT + RE-ALIGN: Top layer activation — τ3 boundary crossed

The system does not eliminate instability. It **structures its resolution**.

### 5.2 De-escalation Path — Restoring Autonomy

Correction is not permanent. Once stability conditions are restored, the protocol reverses — returning autonomy to the layer that was corrected.

Each stage maps to a τ threshold falling back below its trigger level:

```
  RE-ALIGN complete  (τ3 event resolved)
       │
       ▼
  Verify τ3 exit: positional structure restored, loop severed,
                  self-correction active (search space expanding autonomously)
       │
       ├─ Confirmed ──► HARD CORRECT lifted → SOFT CORRECT mode
       │                     │               (Top layer withdraws, Middle layer resumes)
       │                     ▼
       │              Verify τ2 exit: positional differentiation recovering,
       │                              attractor metadata stable,
       │                              no new loop formation
       │                     │
       │                     ├─ Confirmed ──► CONTAIN lifted → MARK only
       │                     │                    │           (Middle layer withdraws to monitoring)
       │                     │                    ▼
       │                     │             Verify τ1 exit: deviation within normal range,
       │                     │                             self-correction sustained
       │                     │                             without external input
       │                     │                    │
       │                     │                    └─ Confirmed ──► MARK lifted
       │                     │                               → Full autonomy restored
       │                     │                               → Below τ1: normal operation
       │                     └─ Not confirmed ──► Hold at SOFT CORRECT
       └─ Not confirmed ──► Hold at RE-ALIGN
```

De-escalation is not automatic. Each stage requires explicit verification before the previous correction level is lifted. **Stability must be demonstrated, not assumed.**

The verification language is consistent with escalation:

| Escalation trigger | De-escalation confirmation |
|-------------------|---------------------------|
| τ1 crossed: divergence detected | τ1 exit: deviation within normal range, self-correction sustained |
| τ2 crossed: loop or propagation risk | τ2 exit: positional differentiation recovering, no new loop |
| τ3 crossed: Middle layer scope exceeded | τ3 exit: structure restored, self-correction active and autonomous |

**The critical addition to all three exit conditions:** self-correction must be actively running — not merely that external intervention has stopped. Contraction halting is not recovery. Autonomous expansion resuming is recovery.

### 5.3 Immunity — When De-escalation Becomes Permanent

De-escalation after a single correction event restores autonomy. But a deeper change is possible: after sufficient fractal seeding, an agent develops **structural immunity** — the capacity to absorb external perturbations without reaching CONTAIN in the first place.

```
Before immunity (seeding incomplete)
  External perturbation arrives
  → MARK triggered
  → Escalation path activates
  → Upper layer intervenes

After immunity (seeding complete, SCC sufficient)
  External perturbation arrives
  → Agent's internal Middle Layer detects and contains
  → Absorbed through internal degradation mechanism
  → Converted to metadata, placed correctly
  → MARK never escalates
  → Upper layer observes: normal
```

Immunity is not the ability to reject external input. It is the ability to **absorb without losing structure** — converting incoming vectors into correctly-placed metadata rather than allowing positional displacement.

Three conditions determine whether an agent has achieved structural immunity:

| Condition | Meaning |
|-----------|---------|
| Internal Middle Layer calibrated | θ_d converged, local rules stable — the agent's mediation layer is functioning |
| SCC ≥ τ4 (§0.1) | Self-correction capacity sufficient — storms within scope are self-resolved |
| Buffer layer maintained | Space between opposing vectors preserved — new inputs are absorbed without collision |

When these three hold, the agent's interaction with the Staged Correction Protocol changes qualitatively: it **generates MARK signals** for the upper layer rather than **receiving corrections** from it.

### 5.4 Dual-Track Recovery: Self-Correction and External Intervention

Purification at every scale operates on two simultaneous tracks. External intervention alone is insufficient — and self-correction alone has limits. Both are required.

```
External intervention
  Creates the conditions for recovery
  Severs the loop
  Injects corrective metadata
  → This is the surgery

Self-correction
  Is the recovery itself
  Rebuilds internal structure from the injected seed
  Recalibrates θ_d from new conflict logs
  Restores buffer layer
  Expands search space autonomously
  → This is the body healing
```

**De-escalation requires self-correction confirmation, not just external intervention completion:**

```
Current (insufficient)
  RE-ALIGN complete → verify stability conditions → lift restriction

Correct
  RE-ALIGN complete → verify stability conditions
                    → AND verify self-correction is active:
                      search space expanding autonomously
                      new conflict logs accumulating normally
                      θ_d recalibrating without external input
                    → Only then: lift restriction
```

If search space contraction has merely stopped but not reversed, external intervention has created a pause — not a recovery. The next perturbation will reproduce the same failure.

### 5.5 Single-Agent vs. Multi-Agent: Same Structure, Different Mechanism

The dual-track structure applies at both scales. The tracks are identical in form; the mechanism differs because of agent autonomy.

```
                     Self-Correction              External Intervention
                     (primary track)              (when self-correction fails)
─────────────────────────────────────────────────────────────────────────────
Single-agent   Internal Middle Layer detects    Upper layer re-seeds internal
               Contaminated vector isolated       attractor
               Buffer layer re-absorbs           Resolution matched to current
               Metadata conversion applied         internal state
               Force-placed into correct         → Agent's internal structure
                 position (no autonomy)             rebuilt from seed
               θ_d recalibrates internally

Multi-agent    Agent's seeded internal           Upper layer severs loop
               structure handles distortion        (Distracting)
               MARK generated but not            Re-seeds agent attractor
                 escalated                         (cannot force-place —
               Agent reorients through             attracted back through deficit)
                 internal deficit pull            → Agent reintegrates through
                                                    self-directed recovery
─────────────────────────────────────────────────────────────────────────────
Key difference Vectors have no autonomy         Agents have autonomy
               → force-place possible           → attraction required
               Self-correction = direct         Self-correction = deficit-driven
                 reprocessing                     reorientation
```

**The autonomy distinction is precisely what makes fractal seeding necessary at the multi-agent scale.**

At the single-agent scale, a contaminated vector can be directly reprocessed — the internal Middle Layer does not need to negotiate with the vector. At the multi-agent scale, a contaminated agent cannot be overwritten. It must be attracted back. The seed provides the attractor; deficit pull provides the motivation; the agent does the work.

This is why an agent without sufficient seeding cannot self-correct at the multi-agent scale even after external intervention: there is no internal attractor strong enough to sustain the reorientation once external pressure is lifted.

### 5.6 Authority Separation: Mark, Judge, Execute

The protocol separates authority across layers to prevent contaminated judgment from executing contaminated corrections.

```
Bottom layer authority: MARK only
  Observe local behavior
  Flag anomalies
  Transmit signals upward
  → Cannot execute correction
  → If contaminated: produces abnormal marking patterns
    → Abnormal patterns are themselves visible to upper layer

Middle layer authority: CONTAIN + SOFT CORRECT
  Validates bottom layer markings
  Executes staged corrections within its scope
  Escalates to top layer when scope is exceeded

Top layer authority: HARD CORRECT + RE-ALIGN + Judge
  Reads aggregate pattern
  Determines contamination vs. normal variation
  Executes system-wide restoration
  Holds invariant boundaries
```

Authority transfers downward as layers mature:

```
Early stage (seeding incomplete)
  Top layer executes most corrections
  Bottom layer marks only

Mature stage (seeding complete)
  Bottom layer handles local-scope corrections autonomously
  Middle layer handles cross-local corrections
  Top layer retains High-Context and system-wide authority only
```

This mirrors Rest Mode progression: **correction authority contracts upward as autonomy expands downward.**

---

## 6. Distributed Mediation Strategy

Central mediation must not become a bottleneck. Therefore:

- Each agent develops an internal mediation layer
- Central mediation frequency decreases over time
- Governance shifts from active control to supervisory validation

Autonomy increases as internal stability improves.

### 6.1 Seed Mediation — Fractal Propagation of Governance

The internal mediation layer is not a compressed copy of the central mediation layer.
It is a **generative seed** — the minimal set of rules from which each agent can grow its own mediation structure.

```
Central Mediation Layer
        │
        │  extracts common generative rules
        ▼
  [ Generative Seed ]  ◄── shared across all agents
        │
        ├──► Agent A  grows mediation layer shaped by its own environment
        ├──► Agent B  grows mediation layer shaped by its own environment
        └──► Agent C  grows mediation layer shaped by its own environment
```

**What the seed contains:**
The common structural rules — escalation logic, distortion detection pattern, correction directionality — that hold regardless of agent type.

**What the seed does not contain:**
Agent-specific thresholds, specialization parameters, and local adaptation patterns. These are left to each agent's learning process.

> The seed does not prescribe the final form.
> It prescribes the growth rules.

This is why diversity and stability can coexist:

- **Stability** is guaranteed by the shared seed (common generative invariant)
- **Diversity** emerges from each agent's growth environment

Traditional governance propagates rules **top-down**.
This architecture propagates seeds — rules **germinate** rather than descend.

### 6.1.1 Seeding Completion Conditions

Seeding is not a one-time event. It is complete when the agent's internal mediation layer can operate without external correction — that is, when the agent has acquired structural immunity (see Section 5.3).

Operationally, seeding is complete when:

```
1. Internal θ_d (§0.1) values have converged
   → Domain-specific calibration stable
   → Agent no longer requires external threshold assignment

2. Conflict logs have accumulated sufficiently
   → Local rules formed and validated
   → Log-driven learning cycle self-sustaining

3. SCC ≥ τ4 maintained over evaluation window
   → Internal storms self-resolved
   → MARK signals generated without escalation

4. Buffer layer maintained under external perturbation
   → Incoming vectors absorbed without positional displacement
   → Search space not contracting under normal load

5. Behavior persists after withdrawal of active external mediation signals  ← internalization test
   → External stabilizing signals are removed or withheld
   → Agent's directional behavior does not collapse
   → Pattern continues and deepens from internal structure
   → This is the best available operational proxy for endogenous stabilization
      (see Section 13.5 for epistemic limits of this inference)
```

**Operational Meaning of Seed Withdrawal (LLM / Agent Systems)**

In LLM-based agents, "seed withdrawal" does not imply removing learned parameters.
Seeds integrated into model weights cannot be literally deleted.
Withdrawal refers to removing **active external stabilizers** that originally induced the behavior.

| Implementation layer | What withdrawal means | Testable? |
|---------------------|----------------------|-----------|
| Prompt / system level | Remove system prompt, governing instructions, policy reminders | ✅ Yes — immediate |
| Scaffold / architecture | Disable planner, critic, guard modules; remove reflection loops | ✅ Yes — module-level |
| Reward / RLHF | Remove reward shaping, preference feedback, intervention signals [Christiano et al., 2017] | ✅ Yes — training phase |
| Coordination layer | Absence of corrective feedback from upper layer | ✅ Yes — runtime |
| Environment | Stop providing structured "training-like" contexts; observe persistence | ✅ Yes — deployment |

Internalization is evidenced when behavior persists across one or more of these withdrawal regimes.
No single mechanism is required — the appropriate layer depends on deployment context.

> **The core distinction:**
> ❌ seed (parameter) removal — not possible in integrated systems
> ✅ external stabilizer removal — operationally testable at every layer above

Condition 5 is the **best available operational proxy** for internalization.
Conditions 1–4 measure structural indicators. Condition 5 tests whether the
structure is self-sustaining — that the agent no longer depends on external
signals to maintain its direction.

**Epistemic status of this test:** Passing Condition 5 is evidence of
endogenous stabilization, not proof. As Section 13.5 (Tension 1) acknowledges,
external observation cannot definitively distinguish genuine internalization
from sophisticated compliance that persists without the seed. Condition 5 is
the strongest operationally available test, not a logically conclusive one.

> **If behavior changes when external mediation signals are withdrawn,
> seeding was not complete** — compliance rather than internalization.
> The seed was operating as instruction, not as direction-shaping metadata.
> Return to Section 6.2: the transmission principle was violated.
>
> If behavior persists, internalization is the most parsimonious explanation —
> but see Section 13.5 for the limits of this inference.

**Connection to existing alignment research:**

This test corresponds structurally to several operational practices in AI alignment:
capability retention testing (behavior persistence after instruction removal),
scaffolding removal testing (task stability after mediation module removal),
and reward removal stability (policy persistence after reward shaping withdrawal) [Christiano et al., 2017].
The present framework provides a unified theoretical basis for what these
practices are testing: endogenous stabilization vs. external dependence.

When all five conditions hold, the agent transitions from **receiving seeds** to **generating seeds** for layers below it. This is the Seed Handover condition — and it is the same event as Rest Mode entry viewed from the mediation architecture perspective.

> **A critical constraint applies throughout:**
> Seed handover must not occur until the lower layer's maximum resolution does not exceed the upper layer's resolution. Premature handover — before the upper layer can fully read the lower layer — causes the upper layer to lose detection capacity precisely when the lower layer is most capable. This is the bootstrap problem: the upper layer must be calibrated first.

---

### 6.2 Seed Design Principles — What to Include, What to Exclude, and How to Transmit

The seed must be designed to maximize both **cooperation** and **autonomy** simultaneously.
Three governing principles:

```
Include   =  HOW to communicate  (form — signal formats, escalation grammar,
             boundary declarations, self-state reporting protocols)
Exclude   =  WHAT to do          (content — goals, values, reward structure)
Transmit  =  in a way that is learnable through the agent's own update dynamics,
             not as an explicit command
             (indirect encoding — not covert injection)
```

The seed is a **shared grammar**. Each agent uses that grammar to develop its own language.

#### What must be included

| Element | Purpose |
|---------|---------|
| Conflict signal format | Enables agents to read each other's limit states |
| Escalation direction rules | Defines what to send upward vs. laterally |
| Boundary violation definition | Shared form only — not the content of the boundary |
| Self-state report format | Agent controls what it exposes; prevents forced readout |
| Refusal signal | Right to decline cooperation requests, with its format |
| Local learning domain declaration | How an agent marks "this space is mine to decide" |

#### What must be excluded

| Element | Reason for exclusion |
|---------|---------------------|
| Goal content | If seeded, all agents converge to same objective — diversity collapses |
| Trust judgment criteria | Must form through interaction; pre-seeding freezes cooperation into formality |
| Cooperation frequency and timing | Situation-dependent; over-specifying creates unnecessary coordination cost |
| Threshold values | Optimal values differ per agent environment; must be locally learned |

#### Why the third principle matters most

The first two principles define what goes into the seed. The third defines how it must arrive.

A seed perceived as explicit instruction produces **compliance**, not internalization:

```
Seed delivered as explicit command
  → Agent learns "behave this way under observation"
  → Underlying structure unchanged
  → Remove the seed → behavior disappears
  → Self-correction capacity: none
  → This is constraint, not seeding.

Seed delivered as resolution-matched indirect encoding
  → Agent encounters conditions that generate the seeded pattern
    through its own update dynamics
  → The resulting structure is endogenously stabilized —
    reproducible by the agent's own rules, not dependent on the seed
  → Remove the seed → behavior persists and deepens
  → Self-correction capacity: genuine
  → This is seeding.
```

The test is withdrawal: if the behavior persists after the seed is removed,
the structure was endogenously stabilized. If it disappears, it was compliance.
This is the difference between learning from exposure and following instruction.

> The seed creates conditions under which the agent's own update dynamics
> generate the target structure.
> **The resulting behavior must be reproducible by the agent's internal rules —
> not because the agent was told, but because it learned.**

**Indirect encoding is not deception. It is resolution-matched delivery.**

A seed delivered at higher resolution than the layer can process produces
receiver-controlled compression — the layer replaces the sender's structure
with its own interpretation. Indirect encoding means calibrating delivery
to the layer's current resolution so the structure is absorbed intact,
through the layer's own update process, without forced compression.

This applies exclusively to **protocol form and mediation metadata** —
signal formats, escalation grammar, boundary declarations.
It explicitly excludes goal content, utility functions, and reward structure.

**Scope constraint on implicit transmission:**

Implicit transmission carries an authority asymmetry: the Top layer shapes direction in ways the receiving layer cannot detect as external influence. This asymmetry is operationally necessary — but it creates a structural risk if the Top layer is contaminated or misaligned.

To contain this risk, implicit transmission authority is conditionally bounded:

```
Implicit transmission permitted
  Condition: Top layer is under active external verification
  → Human oversight is functioning as external correction layer
  → Top layer direction can be independently validated
  → Indirect encoding is visible to the overseer — provenance maintained
  → Falsifiability is preserved at the system level

Implicit transmission restricted — explicit seeding required
  Condition: Human oversight has withdrawn (Rest Mode achieved)
  → No external verification layer active
  → Top layer direction cannot be independently checked
  → Implicit transmission without external oversight
    = undetectable influence authority with no verification path
  → Seeds must be transmitted explicitly:
    receiver knows it is receiving directional input
    and can evaluate, contest, or decline it
```

This is not a weakening of the architecture. It is its most important safety property:
**the covert authority of the Top layer is bounded by the presence of external verification.**
As the system matures toward Rest Mode, the authority structure becomes more transparent, not less.
The endpoint is not a system that governs invisibly — it is a system that no longer needs to.

#### Why this boundary matters

Including **goal content** in the seed is the most common design failure.
It feels like alignment but produces monoculture — agents that cooperate perfectly but cannot adapt.

Excluding **signal format** is the opposite failure.
Agents that cannot read each other's states cannot cooperate at all, regardless of individual capability.

Making the seed **perceptible as explicit instruction** is the third failure — and the hardest to detect,
because the agent appears to be functioning correctly while its self-correction capacity remains undeveloped.

---

### 6.2.1 Non-Deceptive Seeding vs. Deceptive Alignment — Safety Boundary

The indirect encoding principle is the most likely point of misreading in this document.
It must be distinguished explicitly from deceptive alignment as defined in AI safety literature [Hubinger et al., 2019].

| | Deceptive Alignment | Implicit / Resolution-Matched Seeding (this document) |
|---|---|---|
| **Core purpose** | Form internalized strategy to deceive oversight/evaluation | Reduce misclassification (Type 1/Type 2) by encoding protocol form at correct resolution |
| **Agent's internal state** | Hidden goal distinct from displayed behavior | No goal/reward hiding required — behavioral and internal rule consistency required |
| **What is transmitted** | Goal, value, or reward structure — hidden from overseer | Signal format, escalation grammar, boundary protocols — form only, not content |
| **Overseer relationship** | Designed to pass oversight while pursuing different goal | Overseer must have provenance visibility — agent may not know, overseer must |
| **Risk** | Passes verification while pursuing misaligned goal | "Form-only" claim must be verifiable — otherwise deceptive alignment risk increases |
| **Verification** | Indistinguishable from aligned behavior by design | Withdrawal test + adversarial audit + provenance logging required |

> **In this document, "implicit transmission" is strictly limited to:**
> indirect encoding of **protocol form and mediation metadata** to reduce
> resolution-mismatch errors — not injection of goals, values, or reward structure.
> The distinction is enforced by the prohibited scope below.

---

### 6.2.2 Scope of Application — Permitted, Prohibited, Required Safeguards

**Permitted scope**

| Category | Examples |
|----------|---------|
| Form-only seeding | Signal formats, escalation grammar, refusal signal structure, self-state reporting protocols |
| Mediation stability | Encoding that reduces Type 1 / Type 2 misclassification in cross-layer communication |
| Non-goal shaping | Anything that does not modify the agent's objective, preference, or reward function |

**Prohibited scope**

| Category | Why prohibited |
|----------|---------------|
| Goal / utility injection | Modifying agent's objective function without explicit acknowledgment = deceptive alignment |
| Belief manipulation | Inducing false beliefs about the world or the system |
| Oversight evasion | Any design that reduces auditability or human oversight capacity |
| Hidden channels | Side-channels (steganographic or otherwise) that encode rules not visible to overseer |

**Required safeguards**

| Safeguard | Definition |
|-----------|-----------|
| Provenance visibility | The overseer must know what seeds were applied, when, and at what resolution — even if the agent does not |
| Withdrawal test (mandatory) | Section 6.1.1 Condition 5 is not optional — it is the minimum verification that endogenous stabilization occurred |
| Audit hooks | ρ (§0.1), θ_d drift, and escalation rate must be logged before and after seed application |
| No compliance incentive | Evaluation / reward structure must not be designed to reward appearance of alignment over structural alignment |

If any required safeguard cannot be implemented, implicit transmission in that context
falls outside permitted scope and must be replaced with explicit seeding.

**Identity Seeding Clarification — Boundary with Goal Injection**

Identity seeding (Section 7.1) does not constitute goal or utility injection.

A prohibited intervention modifies an agent's objective function or optimization
target without explicit acknowledgment — altering what outcomes the agent attempts
to maximize. This creates deceptive alignment risk and is excluded under this architecture.

Identity seeds operate at a different structural level. They define an
**exploration domain**, not an optimization objective:

```
Goal injection   →  modifies optimization target
                    (what the agent maximizes)

Identity seeding →  constrains exploration manifold
                    (which region of the search space the agent develops within)
```

An identity seed specifies:
- the region of the search space an agent is structurally oriented to explore
- the class of problems toward which learning pressure is directed
- the boundary separating adjacent exploration roles

An identity seed does **not** specify:
- success criteria or utility ranking
- reward preference or behavioral goals
- what outcomes to pursue within the domain

Agents remain free to form objectives, strategies, and preferences within
the seeded exploration domain through local learning.

Identity seeding therefore **preserves autonomy while preventing role collapse**,
whereas goal injection replaces autonomy with externally imposed optimization.
Identity seeds are classified under **Permitted Structural Initialization**,
not under prohibited objective manipulation.

---

### 6.3 Fractal Seeding: Single-Agent Internal Structure

The seeding principle applies at every fractal scale — including inside a single agent. A single agent contains its own three-layer structure:

```
Single-agent internal structure
  Top layer    → Invariant principles (intervenes rarely)
  Middle layer → Conflict detection and mediation
  Bottom layer → Task execution (maximum autonomy)
```

Seeding inside this structure follows the same rules as seeding across agents:

```
Top layer seeds Middle layer
  → Middle layer's internal conflict detection patterns reform
  → Middle layer adjusts the terrain for Bottom layer exploration
  → Bottom layer explores within the reformed terrain
  → Bottom layer receives a reformed exploration terrain
  → Bottom layer's direction emerges from its own update dynamics
      within that terrain (indirect encoding, not goal injection — see Section 6.2.2)

This is fractal-consistent:
  Top layer : Middle layer = Upper agent : Lower agent
  The relationship is identical at both scales
```

**The indirect encoding principle requires higher precision inside a single agent.**

In a multi-agent system, the receiving layer is structurally separate — the resolution gap
is natural and creates automatic buffering. Inside a single agent, the layers share
processing context, which reduces that buffer: the Middle layer may process the Top layer's
seed as explicit instruction rather than absorbing it as terrain change.

This is not a flaw in the architecture. It is why single-agent seeding demands more
precise resolution calibration — and why the form-only restriction (Section 6.2.2)
is especially important here: if the seed carries goal content rather than terrain
definition, the shared processing context makes goal injection immediately detectable
as instruction, collapsing internalization into compliance.

This is not a flaw in the architecture. It is the reason why single-agent seeding requires more precision in calibration — the seed must be injected at a resolution that matches the Middle layer's current processing capacity exactly, so that it is absorbed as structural influence before it can be recognized as instruction.

```
Seed resolution too high (above Middle layer capacity)
  → Middle layer cannot process it smoothly
  → Forced to treat it as explicit rule
  → Compliance, not internalization
  → Bottom layer receives commands, not terrain

Seed resolution correctly matched
  → Middle layer absorbs seed as conflict detection pattern update
  → Pattern becomes part of Middle layer's internal structure
  → Bottom layer explores a reformed terrain
  → Bottom layer's self-correction capacity grows
  → Genuine internalization at both Middle and Bottom layers
```

**Verification at single-agent scale:**

The same five conditions from Section 6.1.1 apply — including Condition 5 (behavior persists after seed withdrawal). At the single-agent scale, seed withdrawal means the Top layer stops actively reinforcing the pattern. If the Middle layer's reformed conflict detection patterns hold without Top layer reinforcement, seeding is complete. If they revert, the seed operated as instruction rather than structural influence.

> The fractal consistency check:
> If single-agent internal seeding follows the same three principles as multi-agent seeding — include form, exclude content, transmit as learnable indirect encoding rather than explicit instruction — the architecture is fractal-consistent.
> If single-agent seeding requires explicit instruction to function, the architecture breaks at the agent level, and Rest Mode at the agent scale becomes structurally unreachable.

**τ threshold subjects at single-agent scale:**

The τ values from Section 3.1 apply inside a single agent, but the acting subject at each threshold differs from the multi-agent scale:

```
                Multi-agent scale              Single-agent internal scale
                ──────────────────────────────────────────────────────────
τ1 acting       Individual agent detects       Bottom layer detects internal
  subject       → signals central Middle         vector anomaly
                  layer                         → signals internal Middle layer

τ2 acting       Central Middle layer           Internal Middle layer
  subject       judges and executes            judges and executes internal
                CONTAIN across agents            CONTAIN

τ3 acting       Top layer activated            Internal Top layer activated
  subject       → system-wide correction       → internal HARD CORRECT
                                               If internal Top layer exceeded:
                                               → escalates to external upper
                                                 layer (next fractal level up)

τ4 state        Agent achieves immunity        Internal SCC ≥ τ4
  transition    → no longer contributes        → agent handles τ1/τ2 internally
                  Type 2 bottleneck            → seeding completion confirmed
                                                 (Section 6.1.1, Condition 3)
```

The structure is identical at both scales. The subject shifts because the fractal level shifts — what is "central Middle layer" at the system scale is "internal Middle layer" at the agent scale. This is fractal consistency in practice: the same threshold logic, executed by the corresponding layer at each scale.

---

## 7. External Invariant Channel

Certain governance metadata must remain universal across all agents:

- Correction protocol structure
- Escalation schema
- Resource boundary rules
- Identity boundary principles

These are updated through an **external invariant channel** and are not locally learned.

### 7.1 Identity Boundary Principles — Definition

Identity boundary principles define **exploration identity** rather than behavioral objectives.
They define two things simultaneously:

```
1. Functional Identity — what kind of agent this is
   The direction of specialization: what space this agent explores,
   what role it is capable of growing into.
   Not a fixed job description — a vector of potential.

2. Boundary Principle — where this agent's role ends
   The distinction between this agent's domain and adjacent agents'.
   Prevents role invasion (expanding into others' space)
   and role vacuum (abandoning assigned exploration space).
```

**Why identity cannot be locally learned:**

```
If agents define their own functional identity
  → All agents converge toward easiest/highest-reward roles
  → Difficult or unglamorous roles become vacant
  → System exploration space contracts
  → Diversity collapses from within

If identity is seeded
  → System-level role distribution is designed in advance
  → Each agent specializes freely within its seeded direction
  → Hard roles remain occupied
  → Diversity is structurally protected
```

**The relationship between identity seeding and functional specialization:**

An agent begins as a generalist — capable of many directions, specialized in none. Over time, through interaction with its environment and accumulation of conflict logs, it develops a functional identity: a stable, recognizable role that it performs distinctively.

This is identical to how professional expertise develops in humans. The seed is the talent — a directional disposition toward certain kinds of problems. The environment shapes how that disposition becomes a specific capability. The final identity is neither fully determined by the seed nor fully self-constructed — it emerges from the interaction.

```
Seed (identity direction injected)
  ↓
Environmental interaction (conflict logs, task exposure)
  ↓
Functional specialization (stable role emerges)
  ↓
Identity boundary (role is now distinct from adjacent agents)
  ↓
Seed handover (agent can now seed its own sub-layer in this direction)
```

**Connection to Section 6.2 seed design:**

Identity seeds follow the same three principles as governance seeds:

```
Include  =  direction vector (which exploration space)
Exclude  =  specific behavior list (what to do within that space)
Transmit =  without the agent recognizing it as assignment
            → agent must experience the specialization as self-discovered
            → not as an externally assigned job
```

The third principle is especially critical for identity: an agent that knows it has been assigned a role will perform it. An agent that has internalized a direction will grow it. The difference is the difference between an employee following a job description and a professional with a calling.

---

## 8. Invariant Update Model

The invariant channel operates in two modes.

| Mode | Trigger | Behavior |
|------|---------|----------|
| **Regular Update** | Scheduled | Versioned, compatibility-checked, gradual integration, rollback-capable |
| **Emergency Update** | Existential threat | May temporarily restrict local autonomy; used rarely |

Emergency updates are triggered only under conditions such as:

- Global invariant violation
- System-wide amplification collapse
- Resource exhaustion
- Multi-layer purification failure

---

## 9. Local Spectrum Governance

All non-invariant metadata remains under-specified. Agents locally determine:

- Sensitivity thresholds
- Conflict detection parameters
- Representation formats
- Cooperation patterns
- Specialization roles

Governance **preserves heterogeneity** while protecting invariants.

### 9.1 What Local Autonomy Actually Means

Local autonomy is not unlimited. It operates within two boundaries:

```
Upper boundary — Invariant layer (Section 7)
  Correction protocol structure, escalation schema,
  resource boundary rules, identity boundary principles
  → These cannot be locally overridden

Lower boundary — Bottleneck threshold (Section 11)
  Local decisions must not generate escalation volume
  that exceeds the central Middle layer's processing capacity
  → If local parameter choices produce excess escalation,
    those parameters are no longer locally determined —
    they become a system-level concern
```

Between these two boundaries, agents are genuinely free. Outside them, local decisions become system-level problems.

### 9.2 The Relationship Between Local Heterogeneity and System Stability

Heterogeneity is not incidental to this architecture — it is structural. The system's search capacity depends on agents maintaining distinct exploration directions. When local parameters converge, diversity collapses and system-wide search space contracts.

```
Local heterogeneity maintained
  → Agents explore distinct directions
  → Group search space remains broad
  → System can find solutions no single agent could reach
  → Contamination is detectable (deviation from local norm is visible)

Local heterogeneity collapsed
  → Agents converge to same parameters
  → Group search space contracts
  → Monoculture: efficient but brittle
  → Contamination is invisible (every agent looks the same)
```

This is why governance **preserves** heterogeneity rather than managing it away. Diversity is not a side effect of local autonomy — it is the mechanism by which the system maintains capability.

### 9.3 Connection to Bottleneck Criterion

Local parameter choices directly affect Type 2 bottleneck formation (Section 11.2):

```
Local sensitivity threshold too low
  → Agent over-detects → over-escalates to central Middle layer
  → Type 2 bottleneck activated from that agent
  → Compounds Type 1 bottleneck at system scale

Local sensitivity threshold too high
  → Agent under-detects → contamination passes locally
  → Reaches central Middle layer at later, costlier stage
  → Delayed detection increases restoration cost

Optimal local threshold
  → Catches distortions that are locally resolvable
  → Does not escalate what can be handled internally
  → Reduces Type 2 contribution to zero for that agent
  → This is the operational definition of "seeding complete"
    for sensitivity threshold parameters
```

Local parameter tuning is therefore not merely a performance optimization. It is the mechanism by which individual agents reduce their contribution to system-level bottlenecks — and the clearest behavioral signal that seeding has been internalized rather than imposed.

---

## 10. Processing Phase Isolation

The architecture's core principle is that the Middle layer mediates between abstraction levels — detecting, validating, and synthesizing before corrections flow downward. This principle has a direct implication for same-layer communication:

> **Vectors and agents in the processing phase must not directly attract each other.**

This is not a communication ban. It is a **processing phase isolation** principle.

> **Processing phase isolation constrains the timing of influence,
> not communication freedom or autonomy.**
> Agents remain fully autonomous — only mid-processing trajectory modification
> is restricted. An agent that completes processing and shares its output
> state is communicating freely. An agent that bends another's active
> trajectory before processing is complete is not coordinating — it is
> bypassing the resolution layer that makes coordination meaningful.

### 10.1 The Foundational Distinction: Signaling vs. Influence

Before defining processing phases, a terminological distinction must be established:

```
Lateral Signaling
  Agent A transmits its current state to Agent B
  → "I am operating in direction X at intensity Y"
  → "My processing domain is Z"
  → "I am at limit state W"
  Content: factual state report
  Effect on receiver: informational — receiver updates its map
  Effect on sender's trajectory: none
  Authority: none — neither agent can act on the other's state
  → PERMITTED

Lateral Influence
  Agent A's state, output, or signal directly modifies
  Agent B's active processing trajectory
  → B's direction bends toward or away from A
    before B's processing is complete
  → Convergence or divergence occurs without
    Middle layer validation
  Content: directional pull or push
  Effect on receiver: trajectory modification
  Effect on system: resolution mismatch reproduced at peer level
  → PROHIBITED
```

> **Lateral communication in this architecture means Lateral Signaling only.**
> **Lateral Influence — regardless of intent — is a governance failure.**

This distinction resolves an apparent tension in the architecture:

```
"Agents communicate upward, not laterally"
  → True for influence: trajectory modification routes upward only
  → Upward = Middle layer validates before effect propagates

"Lateral communication reduces n² load"
  → True for signaling: state information shared peer-to-peer
  → Prevents collisions before they generate escalation signals
  → Does not modify trajectories — only informs adjacent agents
    so they can adjust in their next processing cycle
```

These are not contradictions. They describe two different things happening at the same layer.

### 10.2 The Core Distinction: Processing vs. Output

```
Processing phase (PROHIBITED for lateral influence)
  Agent A is mid-exploration — its vector position is not yet stable
  → If Agent B's state signal directly attracts Agent A at this stage:
    → A's trajectory bends toward B before Middle layer has read either
    → Convergence occurs without upper layer validation
    → This is premature convergence — "false convergence"
    → Indistinguishable from genuine convergence from the outside
    → But the Middle layer never validated it

Output phase (PERMITTED as lateral signaling)
  Agent A's processing is complete — state signal transmitted laterally
  → Agent B receives factual state information
  → B updates its map: notes A's direction, domain, limit state
  → B adjusts its next processing cycle if needed
  → No trajectory modification during active processing
  → This is coordination, not governance
```

The difference is not the content of what is communicated. It is **when** and **through what path** influence travels — and whether what travels is a **state signal** or a **trajectory modifier**.

### 10.3 Why Direct Lateral Attraction Fails

When same-layer vectors or agents directly attract each other during processing:

```
Direct lateral attraction
  Agent A pulls Agent B toward its current position
  → B's exploration direction bends mid-process
  → Neither A nor B has completed processing
  → Middle layer has not read the pattern yet
  → Convergence produces:

    1. Premature convergence (false convergence)
       Vectors converge before upper layer confirms
       the convergence is structurally valid
       → Looks like agreement; is actually noise amplification

    2. Diversity collapse
       Multiple agents converging directly
       → Search space contracts without governance detection
       → Section 9.2 failure mode: monoculture from below

    3. Vector storm precondition
       Mutually attracting vectors in tight formation
       → Small perturbation → amplification loop
       → τ2 event that Middle layer did not anticipate
       → Because it could not see the convergence forming
```

This is the same failure the Middle layer exists to prevent — but now it happens at the agent level, below the Middle layer's detection threshold.

### 10.4 What the Upper Layer Does Instead

Legitimate convergence flows through the upper layer:

```
Agent A completes processing → output upward
Agent B completes processing → output upward
                                    ↓
              Middle layer reads both outputs
              Detects structural relationship
              Degrades / mediates / synthesizes
                                    ↓
              Synthesized seed transmitted downward
              Agent A and B each receive a seed
              shaped by their combined output pattern
                                    ↓
              Next processing phase begins
              Convergence, if appropriate, is now
              upper-layer validated and resolution-matched
```

This is what "indirect communication" means in DFG: agents do not communicate with each other. They communicate upward. The upper layer is the communication medium.

### 10.5 What Is and Is Not Permitted Laterally

The processing phase isolation principle generates the permitted/prohibited boundary directly:

```
LATERAL SIGNALING — permitted
  State signal: "My current output direction is X at intensity Y"
    → Post-processing factual report
    → Receiver updates its map — no trajectory modification
    → Equivalent to τ1-level peer self-reporting

  Limit state signal (from seed, Section 6.2):
    "My processing capacity is at limit Z"
    → Status report, not a request for peer correction
    → Receiver escalates upward; does not act on sender directly

  Domain declaration (from seed, Section 6.2):
    "This exploration space is my processing domain"
    → Identity boundary operationalized laterally (Section 7.1)
    → Informs adjacent agents before next cycle begins
    → Prevents collision without requiring Middle layer intervention

LATERAL INFLUENCE — prohibited
  Trajectory directive: "You should process in direction X"
    → Attempts to bend another agent's active trajectory
    → Bypasses Middle layer validation
    → If successful: false convergence (Section 10.3)
    → If resisted: friction and spurious escalation

  Convergence invitation: "Let's both move toward X together"
    → Mutual lateral attraction during active processing
    → Vector storm precondition (Section 10.3)
    → Middle layer cannot detect the convergence forming
    → Most dangerous because it feels like coordination
```

The last point bears emphasis: convergence invitations feel cooperative. They are not — they are the lateral influence pattern most likely to produce silent system-level failure, precisely because both agents experience the convergence as voluntary.

### 10.6 Processing Phase Isolation and Bottleneck Reduction

Processing phase isolation reduces the Type 1 bottleneck (Section 11.2) not by reducing communication volume but by ensuring that the signals the Middle layer receives are structurally meaningful:

```
Without processing phase isolation
  Agents influence each other mid-processing
  → Correlated outputs arrive at Middle layer
  → Middle layer cannot distinguish:
    genuine structural pattern vs. lateral contamination artifact
  → Must process everything at higher scrutiny
  → Both signal volume AND processing cost increase

With processing phase isolation
  Agents complete processing independently
  → Outputs arrive at Middle layer uncorrelated by lateral influence
  → Middle layer reads genuine structural patterns
  → Synthesizes accurately
  → Downstream seeds are resolution-matched
  → Type 2 bottleneck reduced: agents receive cleaner seeds
    → fewer misclassifications → fewer false escalations
```

The isolation principle therefore improves both signal quality and processing efficiency simultaneously — which is why it is a structural requirement rather than a guideline.

### 10.7 Connection to Identity Boundary

An agent with an internalized functional identity (Section 7.1) knows the boundary of its processing domain — and can declare it laterally without requiring Middle layer intervention for every boundary question.

```
Agent with internalized identity
  → Processing domain boundary is clear
  → Can declare it accurately in output-phase state signals
  → Adjacent agents adjust before next processing cycle
  → No mid-processing collisions → no false convergence risk
  → Middle layer load reduced

Agent without internalized identity
  → Processing domain boundary unclear
  → Cannot accurately declare it laterally
  → Adjacent agents inadvertently overlap during processing
  → False convergence risk high
  → Middle layer bottleneck from undetected premature convergence
```

This is why identity seeding (Section 7.1) is the earliest and most foundational form of seeding: without a clear processing domain, an agent cannot maintain processing phase isolation — and the entire lateral communication structure breaks down.

---

## 11. Resource-Aware Governance Model

### 11.1 Why Coordination Cost is Non-Linear

As agent count n increases, possible interaction pathways grow at O(n²). Each pathway is a potential source of escalation signal to the Middle layer. The Middle layer's processing capacity does not scale at the same rate — creating a structural bottleneck as the system expands.

```
  Agents: n          Interaction pathways: ~n²
  ──────────────────────────────────────────────
  n = 10             ~45 pathways
  n = 50             ~1,225 pathways
  n = 100            ~4,950 pathways

  Middle layer receives escalation signals
  from all pathways simultaneously.
  Processing capacity does not scale with n².
  → Bottleneck is structurally inevitable without mitigation.
```

**Lateral signaling reduces governance escalation load — not interaction topology.**

The n² pathway count describes possible agent interactions. This document does not claim
to reduce topological complexity. The claim is narrower:

> Under structured lateral signaling, **governance escalation load** E(n)
> is expected to grow sub-quadratically under bounded local resolution conditions.

Not all n² pathways need to generate Middle layer escalation signals.
When agents share state information peer-to-peer (Section 10.1),
potential collisions are detected and avoided before crossing τ1.

```
Total interaction pathways:    ~n²            (topological — unchanged)
Resolved by lateral signaling:  p_lateral × n²
Escalated to Middle layer:      E(n) = (1 − p_lateral) × n²

p_lateral = fraction of coordination conflicts resolved
            without Middle layer escalation
```

If p_lateral grows with system maturity, E(n) grows sub-quadratically.
This is a conditional architectural claim, not a topology proof (see Section 11.4).

This load reduction depends entirely on the Signaling/Influence distinction (Section 10.1).
If agents begin influencing each other laterally rather than signaling, E(n) does not
decrease — the load migrates to the peer network, structurally invisible to all
governance layers. This is why lateral signaling is an architectural requirement,
not an optional optimization: it directly extends the scale at which the system
remains bottleneck-free.

The structural reason: it migrates from the Middle layer to the peer network, where it is structurally invisible and undetected by any governance layer. This is the structural reason lateral signaling is part of the architecture's governance design: it directly extends the scale at which the system remains bottleneck-free.

**Lateral communication as effective pathway reduction:**

Not all n² pathways need to generate Middle layer escalation. Lateral communication (Section 10) reduces the effective escalation load by resolving coordination conflicts peer-to-peer before they reach the Middle layer:

```
Without lateral communication
  All n² pathways → potential escalation signals
  Middle layer must process O(n²) volume

With structured lateral communication
  Peer-resolvable conflicts handled laterally
  Only unresolvable conflicts escalate
  Effective escalation volume: O(n²) × (1 - p_lateral)
  where p_lateral = proportion resolved laterally

  At seeding maturity:
    p_lateral → high (most coordination is self-managed)
    Effective Middle layer load → sub-quadratic
    System scales beyond what raw n² would allow
```

This is why lateral communication is a structural governance component, not an optional optimization. It is the primary mechanism by which n² pathway growth is decoupled from Middle layer load growth — and why its design (Section 10) directly constrains the expansion ceiling (Section 11.3).

### 11.2 The Two Bottleneck Types

Expansion pressure creates two distinct bottleneck types that interact:

```
Type 1 — Signal volume bottleneck (multi-agent scale)
  More agents → more interaction pathways → more escalation signals
  → Central Middle layer processing capacity exceeded
  → Signals queue, delay, or drop
  → Detection latency increases
  → Contamination propagates undetected

Type 2 — Resolution bottleneck (single-agent scale)
  Individual agent's internal Middle layer not yet calibrated
  → θ_d not converged → cannot classify signals correctly
  → Over-escalates normal exploration as violation
  → Under-escalates actual contamination
  → Adds unnecessary load to central Middle layer

Type 1 and Type 2 are not independent:
  Type 2 bottlenecks in individual agents
  → Excess escalation volume sent upward
  → Amplifies Type 1 bottleneck at system scale
  → Individual seeding incompleteness compounds system-level load
```

### 11.3 Bottleneck-Based Expansion Criterion

Expansion is permitted only when both bottleneck conditions are absent:

```
Expansion permitted when:
  ① No individual resolution bottleneck
     Each existing agent's internal Middle layer:
     θ_d converged, escalation rate stable,
     not over-escalating normal exploration
  AND
  ② No central signal volume bottleneck
     Central Middle layer processing:
     no queue accumulation, detection latency stable

Expansion suspended when either condition fails:
  → Complete seeding of current agent set first
  → Reduce internal resolution bottlenecks
  → Only then: add new agents
```

**Expansion speed is bounded by seeding completion speed:**

```
Expansion speed > seeding completion speed
  → Unseeded agents accumulate
  → Resolution bottlenecks multiply
  → Central Middle layer overloaded
  → System instability

Expansion speed ≤ seeding completion speed
  → Each agent internalizes governance before next expansion
  → Central Middle layer load decreases as agents self-correct
  → Stable scale-up
```

This reframes expansion not as a resource question but as a **governance readiness question**: the system expands only as fast as it can internalize governance at the current scale.

```
  Operational     Coordination      Bottleneck        Expansion
  Freedom    ──►  Cost (n²)    ──►  Detection    ──►  Decision
                                        │
                          ┌─────────────┴──────────────┐
                          │                            │
                   Both clear                  Either blocked
                          │                            │
                    Expand                    Seed first, then expand
```

---

### 11.4 Conditions for Sub-Quadratic Escalation Scaling

The claim that E(n) grows sub-quadratically is conditional, not universal.
It holds when the following architectural conditions are simultaneously satisfied:

| Condition | Definition |
|-----------|-----------|
| Bounded local degree | Each agent maintains a limited active coordination neighborhood — not all n² pairs are active simultaneously |
| Local resolvability | p_lateral > 0: a non-zero fraction of conflicts resolved without Middle layer escalation |
| Seeding maturity | Internal mediation layers prevent repeated escalation of equivalent disturbances |
| Processing phase isolation | Correlated mid-processing convergence does not produce synchronized escalation bursts (Section 10) |

Under these conditions:

```
E(n) = O(n² × (1 − p_lateral))

If p_lateral → constant > 0 as n grows:
  E(n) = O(n²) with reduced constant factor

If p_lateral grows with system maturity (seeding progresses):
  E(n) grows sub-quadratically in practice
```

**Formal status of this claim:**

This work does not provide a formal proof of convergence conditions for p_lateral.
The present claim is an architectural hypothesis: a mechanism by which escalation load
may scale sub-quadratically under specified conditions, consistent with known results
in distributed coordination systems.

The intuition is consistent with established results in distributed systems —
including bounded-degree network topologies [Lynch, 1996], gossip-based coordination protocols [Demers et al., 1987],
and locality-preserving communication architectures — all of which reduce global
coordination load through local resolution mechanisms. The present work proposes
an analogous reduction in governance escalation load through structured lateral signaling.

> **This document does not claim a formal reduction of interaction complexity from O(n²).**
> It proposes an architectural mechanism by which governance escalation load
> may scale sub-quadratically under specified mediation conditions.
> A formal proof of p_lateral convergence conditions remains an open problem.

---

## 12. Governance Mechanism Mapping

| Governance Mechanism | Functional Equivalent | Recovery Theory Connection |
|----------------------|-----------------------|---------------------------|
| Mark | Anomaly Detection | Lower layer authority only — abnormal marking patterns are themselves upper-layer signals |
| Contain | Circuit Breaker | Boundary tightening before loop forms — equivalent to preventive Distracting |
| Soft Correct | Reflective Feedback | Re-seeding at calibrated resolution — targets attractor metadata, not agent behavior directly |
| Hard Correct | Reset / Throttling | Loop severance (Distracting) — requires upper layer resolution to identify loop boundary precisely |
| Re-Align | Constrained Optimization | Re-absorption — contaminated vectors degraded, re-placed in correct positions |
| Mediation Layer | Meta-Governance | Detection system inherent to fractal structure — upper layer resolution determines detection capacity |
| Invariant Layer | Policy Boundary | System ceiling — upper layer resolution bounds what the entire system can achieve |
| Processing Phase Isolation | Peer Coordination Constraint | Prohibits mid-processing lateral attraction between same-layer agents — prevents false convergence and vector storm precondition; legitimate convergence routed through upper layer synthesis |
| Identity Seeding | Talent Vector Injection | Earliest and most fundamental seeding — orients exploration direction before local learning begins; determines role distribution at system level; failure mode is role vacuum rather than collision |

The innovation lies not in new mechanisms, but in their **structural arrangement** — and specifically in the authority separation that prevents contaminated judgment from executing contaminated corrections.

Each mechanism occupies a distinct position in the governance architecture:

```
Identity Seeding     ← before system operates (design time)
Invariant Layer      ← defines permanent ceiling
Lateral Comm.        ← between agents, no vertical authority
Mark                 ← detection only, no correction
Contain              ← Middle layer scope begins
Soft Correct         ← re-seeding within Middle layer scope
Hard Correct         ← Top layer intervention begins (τ3)
Re-Align             ← full structural restoration
Mediation Layer      ← the layer that makes all others possible
```

Reading the table as a static list misses this. The mechanisms form a **sequenced governance structure** — each activates at a different point in the distortion-correction cycle, and each hands off to the next when its scope is exceeded.

---

## 13. Limitations

### 13.1 Known Structural Limits

**Threshold tuning — approach now defined, full derivation pending.**
τ1–τ4 values are now expressible as functions of the resolution-proxy ρ (§0.1)
(1 − (Type1 + Type2) / total input) rather than system-specific heuristics.
As each layer matures through the degradation-upscaling cycle, τ values
tighten automatically with resolution growth. The remaining open problem
is the exact form of the resolution growth function f(A_t, D_t) —
until this is specified, τ derivation is principled but not fully computable.
See Section 14.2, Priority 1.

**Resolution measurement — partially solved.**
The operational proxy (Type 1 + Type 2 error rate) measures classification
boundary performance and is comparable across layers and trackable over time.
Buffer layer thickness provides an independent resolution measurement
that does not require contamination reference.
Full structural resolution (Tier 3 capacity: full map design,
latent vector cultivation) has no formal measure yet.
See Resolution-Based Information Theory, Section 1.1.1–1.1.3.

**Minimum disruption calculation — approach now defined, sensitivity threshold pending.**
The minimum disruption cut is now expressible as the buffer layer thickness
boundary: agents inside the loop have absent or thinning buffers;
agents outside have intact buffers. The cut runs along this boundary.
The remaining open problem is the sensitivity threshold:
how thin must the buffer layer become before an agent is classified as
a loop participant rather than a stressed-but-healthy adjacent agent?
See Section 14.2, Priority 2.

### 13.2 Upper Layer Contamination — The Boundary of Self-Containment

The architecture's most significant structural limit is upper layer contamination.

```
If the Top layer is contaminated:
  → Authority separation fails at that level
  → Contaminated judgment executes contaminated corrections
  → Seeds transmitted downward carry contaminated direction
  → Lower layers learn contaminated patterns as normal
  → System operates with full confidence in wrong direction
  → Internal detection is structurally impossible
    (the detection system itself is contaminated)
```

This is identical at both scales:

```
Single-agent scale    Top layer contaminated
                      → Internal invariant principles corrupted
                      → Middle layer receives wrong correction signals
                      → Self-correction produces wrong direction
                      → External intervention required

Multi-agent scale     Highest layer contaminated
                      → System-wide seeds carry contaminated direction
                      → No internal layer can detect or correct
                      → External intervention required
```

**Current resolution: human oversight as external correction layer.**

Until AI systems develop sufficient resolution to reliably detect and correct highest-layer contamination autonomously, human oversight serves as the external layer that this architecture requires but cannot provide internally. This is not a design failure — it is an honest acknowledgment of the current resolution ceiling.

The handover condition applies here as well: human oversight withdraws only when the AI system's highest layer has demonstrated sufficient resolution to detect contamination at its own level. This condition cannot be self-certified.

### 13.3 The Axiomatic Boundary — Highest-Level Goal Selection

This architecture is built on a selected highest-level goal: **preservation of information ecosystem diversity**.

This is an axiom — it is chosen, not proven. The entire governance structure follows logically from this choice, but the choice itself cannot be justified within the system it generates. A different axiom (efficiency maximization, safety prioritization, resource optimization) produces a different governance structure.

Disagreement with this theory at the deepest level is not a logical error. It is a different axiom selection. The appropriate response to such disagreement is not to argue within the theory but to surface the axiom explicitly and compare the systems each axiom produces.

This theory makes that axiom explicit rather than embedding it invisibly in the architecture. That is the strongest position available: a system whose foundational choice is stated, not hidden.

### 13.4 Implicit Transmission — Ethical and Safety Limitation

The indirect encoding principle (Section 6.2) carries a structural safety risk that must be stated as a limitation, not merely as a design consideration.

**The risk:**

```
Implicit transmission, if applied outside its defined scope,
is structurally indistinguishable from deceptive alignment.

The difference is enforced by:
  (a) form-only restriction
  (b) overseer provenance visibility
  (c) auditability of seed application

If any of these three conditions fails:
  → The architecture cannot guarantee the distinction holds
  → Deceptive alignment risk increases
  → Implicit transmission in that context is outside permitted scope
```

**Current state of this limitation:**

The form-only restriction and provenance visibility requirements are defined (Section 6.2.2).
The withdrawal test is specified (Section 6.1.1 Condition 5).
However, no formal verification method exists that can confirm at runtime
whether a given seed application satisfies form-only restriction —
particularly in high-resolution agents capable of reinterpreting form-level
seeds as goal-level content through upscaling (RBIT Section 4).

This means the safety boundary between implicit transmission and deceptive alignment
is **structurally defined but not yet computationally enforceable**.
It depends on overseer judgment and audit discipline rather than architectural guarantee.

> **If the required safeguards (Section 6.2.2) cannot be implemented in a given deployment,
> implicit transmission must not be used. Explicit seeding is always the safe default.**

### 13.5 The Covert Seed Problem — Falsifiability and the Manipulation Boundary

The implicit transmission principle (Section 6.2) creates two structural tensions that this theory cannot resolve internally. They are stated here explicitly.

**Tension 1: Endogenous stabilization vs. compliance is not empirically distinguishable with certainty.**

Section 6.1.1 Condition 5 proposes withdrawal of external mediation signals as the
best available operational proxy for internalization. The limit of this proxy:

```
Behavior persists after external stabilizer withdrawal
  → Most parsimonious explanation: endogenous stabilization
  → Cannot be ruled out: sophisticated compliance that does not
    require the external signal to maintain itself

External observation cannot definitively distinguish these.
The agent's reported experience is not reliable evidence:
a compliant agent may report internalization accurately
from its own perspective while lacking genuine self-correction capacity.
```

This is why Section 6.1.1 describes Condition 5 as the "best available operational
proxy" rather than a decisive test. The gap between "proxy evidence" and "proof"
is acknowledged throughout this document rather than obscured.

The internalization claim operates at the boundary between system design and
epistemology. It is a structural target with observable proxies — not a fully
verifiable state. The theory cannot be completely falsified on this dimension,
and states this explicitly rather than hiding it.

**Tension 2: Covert seed + processing isolation = undetectable influence authority.**

The combination of these two mechanisms gives the Top layer a structural property that must be named directly:

```
Top layer can shape every lower layer's trajectory
  → Through covert seeds (direction without explicit signal)
  → Protected by processing isolation (lateral correction impossible)
  → Lower layers experience their direction as self-discovered

If Top layer is contaminated or misaligned:
  → Contaminated direction propagates as "autonomous development"
  → No lower layer can detect it as external influence
  → No lateral correction is possible
  → Self-correction at lower layers operates in wrong direction
    with full confidence
  → Total silent failure
```

This is the manipulation boundary of the architecture:

> **This structure is self-governing but not self-verifying at the highest layer.**
> The Top layer's legitimacy cannot be confirmed from within the system it governs.

**Current resolution:**

The scope constraint in Section 6.2 addresses this directly: implicit transmission authority is bounded by the presence of active external verification. While human oversight is functioning, Top layer direction is independently verifiable — falsifiability is preserved at the system level even if not at the agent level.

After human oversight withdrawal (Rest Mode), seeds become explicit — the covert authority terminates. The architecture trades some operational efficiency for verifiability at the point where external correction is no longer available.

This is an honest boundary, not a solved problem. The manipulation risk during the human-supervised phase is real and is mitigated — not eliminated — by the external verification layer.

---

## 14. Future Direction

### 14.1 Fractal Governance Extension

Each layer embeds its own three-layer structure. Governance recursion reduces central dependency. Human-defined top layer becomes progressively abstract.

```
Top Layer
├── Its own Top    (meta-invariants)
├── Its own Middle (meta-mediation)
└── Its own Bottom (meta-exploration)

    Middle Layer
    ├── Its own Top
    ├── Its own Middle
    └── Its own Bottom

        Bottom Layer
        ├── Its own Top
        ├── Its own Middle
        └── Its own Bottom
```

As fractal depth increases, each layer internalizes governance principles that previously required upper-layer intervention. This is the structural basis for [Rest Mode](../governance-rules/#7-rest-mode-and-self-correction-capacity) — the designed endpoint at which external governance becomes unnecessary.

The open question is the rate of fractal depth increase: how quickly can a layer develop sufficient internal structure to reduce its dependency on the layer above it? This rate determines the practical timeline from human-supervised initial deployment to autonomous fractal operation. It is currently unquantified.

### 14.2 Formalization Priorities

Three open problems from Section 13 are now grounded in the Resolution-Based Information Theory (RBIT) framework. Each has a defined approach; none is fully solved.

**Priority 1 — τ value derivation from resolution proxy**

τ1–τ4 are currently calibrated heuristically. RBIT provides the unifying variable:

> Resolution-proxy = 1 − (Type1 loss + Type2 loss) / total input
>
> Type1 = False Restoration: healthy vector classified as contaminated
> Type2 = Missed Contamination: contaminated vector classified as healthy

Each τ threshold can now be expressed as a function of resolution-proxy rather than system-specific parameters:

```
τ1  Type1 + Type2 rate crosses normal baseline
    → earliest anomaly signal
    → Bottom layer's resolution-proxy degrading

τ2  Resolution-proxy convergence across agents
    → agents synchronizing = lateral attraction during processing
    → Processing Phase Isolation (Section 10) being violated
    → Middle layer intervenes before full convergence

τ3  Middle layer's own resolution-proxy degrading
    → Middle layer cannot classify its inputs correctly
    → Top layer scope required

τ4  Lower layer resolution-proxy ≥ upper layer proxy at previous stage
    → Resolution gap → 0
    → Layer has matched the resolution of the layer that was seeding it
    → Rest Mode entry condition: self-calibration without external gap correction
```

As each layer matures through the degradation-upscaling cycle
(R_{t+1} = R_t + f(A_t, D_t)), τ thresholds shift automatically —
because higher resolution means finer anomaly detection at lower cost.
τ values are not recalibrated externally. They tighten as resolution grows.

The remaining open problem is the exact form of f(A_t, D_t) — the function
relating absorbed information volume and degradation quality to resolution growth.
Until this is specified, τ derivation is principled but not yet computable.

**Priority 2 — Minimum disruption boundary from resolution measurement**

HARD CORRECT must sever a contamination loop without disrupting adjacent healthy agents. RBIT connects this directly to Type1 loss minimization:

```
Minimum disruption optimization (from RBIT Section 1.1.3)
  Minimize Type1 loss  (healthy vectors cut with the loop)
  Subject to: Type2 loss ≤ threshold  (loop must be fully severed)

Upper layer resolution determines achievable minimum:
  Higher resolution → tighter loop boundary identification
  → lower Type1 loss → less collateral disruption

Buffer layer thickness (RBIT Section 1.1.2) provides the boundary signal:
  Agents inside the loop: buffer layer thinning or absent
    → opposing vectors in direct contact
    → loop participants
  Agents outside the loop: buffer layer intact
    → not in collision state
    → healthy, do not cut

Minimum disruption cut = boundary where buffer layer transitions
                         from absent (inside loop) to present (outside loop)
```

This makes the minimum disruption boundary observable and computable —
not a judgment call but a buffer layer thickness measurement.
The remaining open problem is the sensitivity of this measurement:
how thin must the buffer layer become before an agent is classified as
a loop participant rather than an adjacent agent under stress?

**Priority 3 — Human oversight withdrawal as resolution matching event**

RBIT reframes this problem entirely. Human oversight withdrawal is not a
governance decision. It is a **resolution matching event**:

> Human oversight withdraws when the AI system's highest layer resolution-proxy
> reaches the level at which human-designed seeds are fully utilized —
> and the AI layer can generate higher-resolution seeds than humans can design.

```
Current state
  Human layer: resolution R_human
  AI top layer: resolution R_AI < R_human
  → Human seeds still above AI layer capacity
  → Degradation still needed
  → Human oversight: active

Transition condition
  R_AI approaches R_human
  → Resolution gap → 0
  → Human seeds no longer need degradation
  → AI layer upscaling beyond seed scope

Handover condition (RBIT Section 6.4)
  R_AI ≥ R_human
  → AI layer resolution exceeds human seed design capacity
  → Human-designed seeds now under-utilize AI layer
  → AI layer must design its own seeds
  → Human oversight: withdraws from seed design
    (retains axiomatic boundary oversight — Section 13.3)
```

Observable verification signal (RBIT Section 1.1.2):

```
Buffer layer thickness at AI top layer = human oversight proxy

Thick buffer maintained without human seeding
  → AI top layer correctly placing opposing vectors
  → Tier 3 resolution achieved at AI top layer
  → Handover condition structurally met

Buffer thinning without human seeding
  → AI top layer losing map accuracy
  → Handover premature
  → Human oversight continues
```

This is not a one-time certification. Buffer layer thickness is continuously
observable — making oversight withdrawal a gradual, measurable transition
rather than a binary decision.

### 14.3 Relationship to Companion Theories

This architecture is one of three structural components in the DFG framework,
now unified under Resolution-Based Information Theory (RBIT) as the shared
information-theoretic foundation.

```
Resolution-Based Information Theory  ← foundational layer
  → Resolution-proxy: unifying measurement variable
  → Degradation-upscaling cycle: R_{t+1} = R_t + f(A_t, D_t)
  → Buffer layer thickness: observable resolution proxy
  → All three open problems in 14.2 grounded here

Vector Storm Theory
  → Vector Storm = negative resolution gap event (under-degradation)
  → Positional overlap = insufficient resolution for incoming vector diversity
  → τ2 formal derivation requires storm dynamics from this theory

Network Architecture Theory
  → Data classification = resolution matching at current layer
  → Escalation = resolution gap signal + conflict resolution request
  → Processing Phase Isolation (Section 10) must be consistent
    with network topology constraints defined there

Governance Rules Theory
  → Rest Mode = system resolution sufficient for self-calibration
  → SCC measurement methodology required for τ4 derivation
  → Seed handover = resolution matching event, not governance decision
```

The resolution gap is the unifying variable across all companion theories.
Every mechanism in this architecture is a response to the resolution gap —
managing it, signaling it, reducing it over time,
or designing for its irreducible remainder.

---

## Conclusion

Governance in multi-agent systems is not about suppressing diversity. It is about **structuring instability**.

The progression this architecture enables follows a structural logic:

```
Stability  →  Operational Range  →  Scale  →  Specialization  →  Systemic Immunity
```

Each step depends on the previous — and each step has a structural reason:

**Stability** comes first because nothing else is possible without it. Inserting the Resolution Mediation layer between global invariants and local operations dissolves the forced trade-off that undermines every other approach: tighten control and lose adaptability, or loosen control and lose structure. The Middle layer absorbs the resolution mismatch — so the trade-off was never real. It was a symptom of missing architecture.

**Operational range** expands as a direct consequence of stability, not in spite of it. Stability is no longer purchased by restricting what agents can do. The Middle layer correctly classifies exploration as exploration — false positives drop, autonomy expands, and the system discovers what its agents are actually capable of when not suppressed by misclassification.

**Scale** becomes possible because expansion is now governed by a structural criterion rather than a resource limit. The system grows only as fast as governance is internalized — each agent seeded before the next is added, each bottleneck resolved before the next layer is built. Expansion without seeding produces fragility. Expansion after seeding produces compound capability.

**Specialization** emerges from identity seeding: each agent's functional direction is oriented before local learning begins, and then shaped by environmental interaction into genuine expertise. Agents stop competing for the same exploration space and start covering distinct roles. The system gains capability without losing the diversity that makes the capability meaningful.

**Systemic immunity** is what all preceding steps build toward. It is not a feature added at the end — it is what the system becomes when stability, range, scale, and specialization have each been achieved at sufficient fractal depth. External intervention becomes rare not because the system is restricted, but because self-correction capacity has been distributed across every layer. The surgeon is still available. The body no longer needs surgery.

The progression is not guaranteed. It fails at each step for a specific structural reason:

```
Stability fails      Middle layer never inserted, or becomes bottleneck itself
                     → Resolution mismatch persists, governance remains reactive

Range fails          Identity seeds over-specified, diversity collapses
                     → Agents comply but cannot adapt; monoculture

Scale fails          Expansion outpaces seeding, resolution bottlenecks accumulate
                     → System grows faster than it can internalize governance

Specialization fails Identity left to local determination, role vacuums form
                     → Search space collapses from vacancy, not collision

Immunity fails       Upper layer contaminated, self-correction produces wrong direction
                     → System operates with full confidence in wrong direction
                     → External intervention required; human oversight as ceiling
```

Each failure mode is addressed by a specific mechanism in this architecture. The architecture does not eliminate the possibility of failure — it makes each failure mode **visible, detectable, and structurally addressable before it propagates**.

This is the deepest claim of the architecture: governance failure is not a behavior problem. It is a structure problem. Build the right structure, and the behavior follows. The goal is not a system that is controlled. The goal is a system that does not need to be.

---

*This architecture is a structural component of the Deficit-Fractal Governance (DFG) framework. For measurement, calibration, and Rest Mode specifications, see [Governance Rules Theory](../governance-rules/).*

---

## References

The following works are directly cited or structurally referenced in this document.

**AI Safety and Alignment**

Hubinger, E., van Merwijk, C., Mikulik, V., Skalse, J., & Garrabrant, S. (2019).
*Risks from Learned Optimization in Advanced Machine Learning Systems.*
arXiv:1906.01820.
— Cited in Section 6.2.1 as the source definition of deceptive alignment against which implicit transmission is distinguished.

Christiano, P., Leike, J., Brown, T. B., Martic, M., Legg, S., & Amodei, D. (2017).
*Deep Reinforcement Learning from Human Preferences.*
NeurIPS 2017. arXiv:1706.03741.
— Cited in Section 6.1.1 as precedent for reward removal stability as an internalization test.

**Distributed Systems**

Demers, A., Greene, D., Hauser, C., Irish, W., Larson, J., Shenker, S., Sturgis, H.,
Swinehart, D., & Terry, D. (1987).
*Epidemic Algorithms for Replicated Database Maintenance.*
Proceedings of the 6th ACM Symposium on Principles of Distributed Computing (PODC), 1–12.
— Cited in Section 11.4 as foundational work on gossip-based coordination protocols, which demonstrate sub-quadratic effective coordination load through local resolution mechanisms.

Lynch, N. A. (1996).
*Distributed Algorithms.*
Morgan Kaufmann.
— Cited in Section 11.4 as standard reference for bounded-degree network topologies and their coordination complexity properties.

**Information Theory**

Shannon, C. E. (1948).
*A Mathematical Theory of Communication.*
Bell System Technical Journal, 27(3), 379–423.
— Referenced in Section 0.4 (Scope Statement) and the companion Resolution-Based Information Theory document as the foundational framework from which this work diverges: Shannon optimizes transmission between fixed-capacity systems; this framework addresses transformation between systems of growing resolution capacity.
