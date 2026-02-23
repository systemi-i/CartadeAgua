# ACCT Protocol Viewer/Editor — UI/UX Specification

**Version:** 0.1  
**Date:** February 2026  
**Purpose:** Spec for the visual surface that renders, inspects, and refines ACCT protocols.  
**Audience:** UI/UX designers, frontend engineers  

---

## 1. PRODUCT CONTEXT

### What This Tool Is

ACCT protocols are authored through AI-guided conversation. A human describes their institutional process by answering constitutional questions ("What decisions does this process make? Who has the authority? What evidence is needed? What happens when someone disagrees?"). The AI structures the answers into a formal ACCT protocol definition (YAML).

This tool is the **visual counterpart** to that conversational authoring. It takes the protocol definition that emerged from the conversation and renders it as an interactive, inspectable, editable surface.

It serves three modes of use:

1. **Viewing** — "Show me what this protocol looks like." Inspect the commitment topology, understand relationships, trace paths. Used by protocol owners, administrators, Board members, auditors, and anyone who needs to understand the process.

2. **Verifying** — "Is this correct and complete?" Check that the protocol captures institutional reality. Identify gaps — a commitment point with no evidence requirements, an adverse outcome with no recourse, an authority gate with no role assigned. The proof contracts (ACCT's compiler) surface these automatically.

3. **Editing** — "I need to change this specific thing." Targeted, structured modifications to an existing protocol. Not free-form YAML editing — contextual forms that modify the protocol and produce diffs. Edits feed into the governed change process (CP_EVOLVE).

### What This Tool Is Not

It is **not** the primary authoring surface. Protocols are created through conversation with the AI, not by dragging shapes onto a canvas. The tool does not have a "blank canvas" state. It always starts from an existing protocol definition.

It is **not** BPMN. There are no sequence arrows to draw, no swimlanes to assign, no task boxes to place. The topology is generated from the constitutional relationships in the protocol, not drawn by the user.

It is **not** domain-specific. The same tool renders a water utility protocol, a permit processing protocol, a procurement protocol, or any other ACCT-structured process. All domain specifics come from the protocol data, not from the viewer code.

### Design Principles

1. **The protocol is the content.** Every label, every category, every piece of text on screen comes from the protocol data. The viewer is a lens, not a container.

2. **Progressive disclosure.** Level 1 shows the topology and commitment point names. Level 2 shows constitutional signatures and evidence. Level 3 shows full detail including exception spaces, recourse architecture, and proof contracts. The user drills down, never scrolls through everything at once.

3. **Constitutional clarity over process flow.** The visual hierarchy emphasizes *what must be true* at each commitment point, not *what happens in what order*. The topology shows dependencies and relationships, not sequence.

4. **Gaps are visible.** If a commitment point is missing evidence requirements, if an adverse outcome has no recourse, if an authority gate is undefined — the viewer shows this explicitly. Red, not hidden. The proof contracts are surfaced as a living checklist, not buried in a log.

5. **Every edit produces a diff.** Changes to the protocol are never silent. The editor shows exactly what changed, and those changes accumulate as a governed change dossier for CP_EVOLVE.

---

## 2. INFORMATION ARCHITECTURE

### The Three Layers

The viewer has three conceptual layers, organized as a spatial hierarchy:

```
LAYER 1: TOPOLOGY (the map)
  The commitment topology rendered as an interactive graph.
  This is the home view — always accessible, always orientating.
  
LAYER 2: COMMITMENT DETAIL (the constitution of a single point)
  When you select a commitment point, its full constitutional
  signature opens. Evidence, authority, reasoning, outcomes,
  exceptions, recourse, artefacts.
  
LAYER 3: CROSS-CUTTING VIEWS (the system-wide registries)
  Evidence type catalog, exception taxonomy, role registry,
  artefact inventory, proof contracts, protocol metadata.
  These are reference views that cut across commitment points.
```

### Navigation Model

The topology is always the anchor. You never lose sight of where you are in the protocol. Detail views open as overlays or side panels, never replacing the topology entirely.

Cross-cutting views are accessible from a navigation rail (not tabs — the viewer should not feel like a tabbed application where you lose context when switching).

---

## 3. SCREEN SPECIFICATIONS

### 3.1 THE TOPOLOGY VIEW (Home)

**Purpose:** Show the entire commitment topology at a glance. Orient the user. Let them see the shape of the protocol — how many commitment points, how they relate, where the central decisions are, where recourse flows.

**Layout:**

The topology occupies the main canvas area. Commitment points are rendered as nodes. Relationships are rendered as edges. The layout is automatic (not user-positioned), organized in tiers that reflect the constitutional structure:

```
TIER 1 (top):      Entry points — where cases begin
                    (ATTEST: submissions, initial attestations)

TIER 2 (middle):   Verification and assessment
                    (ATTEST: verifications, inspections, technical assessments)

TIER 3 (center):   Core decisions — where the institution binds itself
                    (DECIDE: the central commitments of the protocol)
                    VISUALLY PROMINENT — larger, bolder, different treatment

TIER 4 (below):    Outputs and consequences
                    (DECIDE: issuances; CLOSE: case closures)

TIER 5 (lateral):  Recourse and exceptions
                    (APPEAL, REMEDY, OVERRIDE — visually connected
                    back to the decisions they contest or deviate from)

TIER 6 (meta):     Protocol evolution
                    (EVOLVE — governs all other commitment points)
```

**Node Design:**

Each commitment point is a node. The node communicates four things at a glance:

1. **Commitment type** — through color and a small type badge. The eight ACCT types each have a distinct color. The type badge uses the ACCT name (DECIDE, ATTEST, APPEAL, etc.) because this is precise vocabulary that protocol owners need to learn. But the badge is secondary to the name.

2. **Name** — the human-readable name of the commitment point, drawn from the protocol. This is the largest text on the node. It's in the protocol owner's language, not ACCT jargon. Example: "Availability Decision" not "CP_AVAILABILITY_DECISION."

3. **Constitutional completeness** — a subtle indicator showing whether all constitutional requirements are defined. A small dot or ring: green = all gates defined, amber = partially defined, red = missing required gates. This makes gaps visible without being aggressive.

4. **Delegation status** — if the commitment point has been delegated (to an AI agent or another role), a small delegation indicator appears. This surfaces the automation dial visually.

**Node sizing:** DECIDE commitment points are visually larger than ATTEST points. The central DECIDE of the protocol (every protocol has one — the highest-stakes decision) gets additional visual prominence: a double border, slightly larger, positioned at the gravitational center of the topology.

**Edge Design:**

Edges represent the five ACCT relationship types. Each type has a distinct visual treatment:

- **DEPENDS_ON** — solid line, flowing downward (or toward the dependent point). This is the most common relationship. It means "B cannot happen until A is satisfied." Muted color — these are structural, not dramatic.

- **CREATES_RECOURSE** — dashed line, a distinct color (suggest purple or a warm contrast to the dependency gray), flowing from the adverse outcome back toward the APPEAL commitment point. This is the contestation path. It should be visually distinct because recourse is constitutionally significant.

- **CREATES_OBLIGATION** — dotted line with a small clock or obligation icon. Flows from the creating commitment to the obligated one. Communicates "A generates a future duty at B."

- **SUPERSEDES** — bold line with a direction indicator, connecting the replacement to the original. Example: REMEDY supersedes the original DECIDE. This is rare but constitutionally important.

- **GOVERNED_BY** — very subtle connection (perhaps a thin dotted line or just an implied relationship) from all operational commitment points to the EVOLVE commitment. This communicates that the entire protocol is changeable through governed evolution. It should not dominate the visual but should be discoverable.

**Interaction on the Topology:**

- **Hover a node:** The node's immediate connections highlight. Upstream dependencies light up in one color, downstream dependents in another, recourse connections in a third. Everything else dims slightly. This lets you instantly see "what does this commitment point depend on" and "what depends on it."

- **Click a node:** Opens the Commitment Detail panel (Layer 2). The node stays highlighted on the topology. The user has not "left" the topology — they've drilled into a specific point while maintaining spatial context.

- **Hover an edge:** A small tooltip shows the relationship type and condition. Example: "DEPENDS_ON: Admissibility must be ADMISSIBLE."

- **Click an edge:** Opens an edge detail showing the full relationship definition — type, condition, and the ability to edit the condition.

**Topology Controls:**

- **Zoom and pan** — standard canvas navigation. The topology should be zoomable for large protocols with many commitment points.
- **Filter by type** — toggle visibility of commitment types. Example: show only DECIDE points to see just the decision architecture. Show only APPEAL/REMEDY to see just the recourse architecture.
- **Filter by completeness** — show only commitment points that have constitutional gaps (missing evidence, undefined authority, etc.). This is the verification mode.

---

### 3.2 THE COMMITMENT DETAIL PANEL (Layer 2)

**Purpose:** Show everything about a single commitment point. This is the constitutional X-ray — it reveals the full signature that must be satisfied for this commitment to be legitimate.

**Position:** Opens as a side panel (right side, ~40% of viewport width) when a commitment point is selected. The topology remains visible on the left, with the selected node highlighted. The panel does not float or overlay the topology — it compresses it.

**Structure:**

The panel has a fixed header and a scrollable body organized into sections. The sections correspond to the constitutional signature, not to arbitrary UI categories.

**Panel Header:**

```
[Type badge: DECIDE]  [Completeness indicator: ●●●○ 3/4 gates defined]

Availability Decision
Decisión de Disponibilidad

"The Junta Directiva determines whether the ASADA commits to
providing water service to the proposed project."

[Edit description]
```

The header shows: type, completeness at a glance, name (with localized name beneath), and the description. The description is editable — clicking "edit" opens an inline editor.

**Panel Body — Sections:**

Each section represents one gate of the constitutional signature. Sections are collapsible. Their header shows a status indicator (satisfied/incomplete/undefined).

**Section A: Authority**

```
AUTHORITY                                          [defined ✓]

Who commits:     Board (Junta Directiva)
Quorum:          Simple majority (4 of 7)
Recording actor: Administrator
Delegation:      Not delegable

[Edit authority]
```

Shows the authority gate in plain language. The "edit" action opens a structured form: role selector, quorum field, delegation toggle. If delegation is possible, shows to whom and under what conditions.

If authority is undefined, this section shows a prominent prompt: "Who has the authority to make this commitment? [Define authority]"

**Section B: Evidence**

```
EVIDENCE                                           [5 items defined]

┌─────────────────────────────────────────────────┐
│ ◆ Technical Assessment          Verified    [!] │
│   Required: always                              │
│   Source: Operator (official)                   │
│   Also required at: [none — unique to this CP]  │
├─────────────────────────────────────────────────┤
│ ◆ Demand Estimate               Asserted        │
│   Required: always                              │
│   Source: Platform (machine)                    │
│   ⚠ Machine-attested — cannot be sole basis     │
│     for adverse decision                        │
├─────────────────────────────────────────────────┤
│ ◆ Financial Standing            Observed        │
│   Required: always                              │
│   Source: Billing system lookup                 │
│   From: CP_MOROSIDAD                           │
├─────────────────────────────────────────────────┤
│ ◆ Complete Application Package  Per type        │
│   Required: always                              │
│   From: CP_ADMISSIBILITY                       │
├─────────────────────────────────────────────────┤
│ ◆ Board Minutes Reference       Verified        │
│   Required: always                              │
│   Source: Secretary (official)                  │
└─────────────────────────────────────────────────┘

[Add evidence requirement]
```

Each evidence item shows: name, attestation level (with color coding: Verified=green, Observed=blue, Asserted=amber), condition, source class, and cross-references (where else this evidence type appears in the protocol, and whether it flows from an upstream commitment point).

The attestation level badge is important — it communicates the constitutional weight of the evidence. Machine-attested evidence gets an automatic warning if it's relied upon for an adverse determination.

"Add evidence requirement" opens a structured form that walks through the evidence type properties: what does it prove, who provides it, what level of attestation, validity window, substitution rules.

**Section C: Reasoning**

```
REASONING                                          [defined ✓]

Required:  Yes
Minimum:   Technical basis, regulatory basis,
           conditions, community impact
Format:    Structured slot + free text

[Edit reasoning requirements]
```

Simple section. Shows whether reasoning is required and what the minimum standard is.

**Section D: Outcomes**

```
OUTCOMES                                           [4 defined]

  ✓ APPROVED
    "SÍ HAY DISPONIBILIDAD"
    Adverse: No
    Leads to: Constancia Issuance
    Artefacts: Decision notice

  ✓ APPROVED_CONDITIONAL
    "SÍ HAY DISPONIBILIDAD CON CONDICIONES"
    Adverse: No
    Leads to: Constancia Issuance
    Artefacts: Conditional approval notice

  ✗ DENIED                                        [adverse]
    "NO HAY DISPONIBILIDAD"
    Adverse: Yes → Recourse required
    Recourse: 3-path architecture (see below)
    Leads to: Denial Issuance
    Artefacts: Denial notice with recourse options

  ○ DEFERRED
    "Decision deferred — more information needed"
    Adverse: No
    Creates obligation: Board must revisit
    Artefacts: Deferral notice

[Add outcome]
```

Each outcome shows its key, description, whether it's adverse, what it leads to (downstream commitment points), and what artefacts it generates.

Adverse outcomes get special visual treatment — they're marked clearly and show whether recourse is defined. If an outcome is adverse and no recourse is defined, this is a **proof contract violation** and it's shown in red with an explicit "Recourse required — not yet defined" warning.

**Section E: Recourse Architecture**

```
RECOURSE                                           [defined ✓]

For outcome: DENIED

  Path 1: Internal Reconsideration
    Authority:  Board (Junta Directiva)
    Mechanism:  Written request from applicant
    Deadline:   Next regular Board meeting
    Produces:   Written response with reasoning

  Path 2: Assembly Elevation
    Authority:  Asamblea General
    Mechanism:  Request to include in Assembly agenda
    When:       Reconsideration unsatisfactory

  Path 3: External Appeal (AyA)
    Authority:  AyA regional office
    Mechanism:  Formal appeal
    When:       Denial perceived as arbitrary
    Possible:   AyA mandates reconsideration or
                issues direct determination

[Add recourse path]
```

Recourse is shown as a structured list of paths. Each path has an authority, mechanism, deadline, and possible outcomes. This section only appears if the commitment point has adverse outcomes.

**Section F: Exception Space**

```
EXCEPTIONS                                         [5 named + UNCLASSIFIED]

  ▲ System-wide Moratorium              CRITICAL
    Override: Not possible
    Effect: All applications denied with moratorium as basis

  ▲ Board Conflict of Interest          CRITICAL
    Override: Not possible (must recuse)
    Control: Recusal recorded in acta, quorum reassessed

  ● Suspected Project Splitting         WARNING
    Override: Possible
    Control: Applications combined for aggregate assessment

  ● System Under Capacity Stress        WARNING
    Override: Possible
    Control: Approval limited to low-demand projects

  ○ External Political Pressure         CRITICAL
    Override: Not possible
    Control: Pressure disclosed in acta, decision on
             technical/regulatory grounds only

  ◇ Unclassified                        (catch-all)
    Override: Possible
    Control: Justification required, mandatory review

[Add exception type]
```

Exception types that apply at this commitment point, with severity, override possibility, and compensating controls. The UNCLASSIFIED type is always present and visually distinct (it's the evolution bootstrap — every unclassified exception is data for protocol improvement).

**Section G: Artefacts**

```
ARTEFACTS GENERATED                                [1 defined]

  📄 Decision notice
     Format:     WhatsApp + Email
     Recipients: Applicant
     Includes:   Decision, justification, conditions,
                 recourse options (if adverse)
     Bilingual:  Yes

[Add artefact]
```

What the commitment point produces as institutional outputs.

---

### 3.3 THE CROSS-CUTTING VIEWS (Layer 3)

These views are accessible from the left navigation rail. They show protocol-wide registries and metadata. Each view is a reference surface — primarily for inspection and verification, with targeted editing.

**Navigation Rail Items:**

```
◈  Topology          (the map — always home)
📋  Evidence Catalog   (all evidence types in the protocol)
⚡  Exception Catalog  (the full exception taxonomy)
👤  Roles & Authority  (who participates and what they can do)
📄  Artefacts          (everything the protocol produces)
✓  Proof Contracts    (the compiler — is this protocol valid?)
⚙  Protocol Meta      (version, status, institution, regulatory basis)
🔗  Cross-Protocol     (events emitted/consumed, shared registries)
```

**3.3.1 Evidence Catalog**

Shows all evidence types defined in the protocol as cards. Each card shows: name, ID, purpose, source class (with color coding: official=blue, self=amber, machine=teal, third_party=purple), attestation level, validity window, substitution rules, cross-protocol reusability.

Critical feature: **where used.** Each evidence type card shows which commitment points require it. This is the cross-reference that the earlier prototype was missing. You can see at a glance that EV_MOROSIDAD is required at CP_MOROSIDAD and relied upon at CP_AVAILABILITY_DECISION.

Filtering: by source class, by attestation level, by validity (permanent vs. time-limited), by reusability.

**3.3.2 Exception Catalog**

Shows the full exception taxonomy. Each exception shows: name, severity, which commitment points it applies at, whether override is possible, compensating controls.

Critical feature: **UNCLASSIFIED count.** If the protocol is live and accumulating real data, the exception catalog should show how many UNCLASSIFIED exceptions have been invoked, their justifications, and cluster analysis suggesting new named types. This is the evolution bootstrap made visible.

**3.3.3 Roles & Authority**

Shows all roles in the protocol and their authority mapping. For each role: which commitment points they can commit at, which they can delegate, what their scope is.

Critical feature: **authority coverage matrix.** A simple grid: commitment points on one axis, roles on the other. Each cell shows whether that role has authority at that commitment point (and what kind — primary, delegate, recording actor). Gaps in the matrix are immediately visible.

**3.3.4 Artefacts**

Shows everything the protocol produces: documents, notices, receipts. Each artefact shows: which commitment point generates it, who receives it, format, template structure.

**3.3.5 Proof Contracts**

This is the compiler view. Shows each proof contract (every commitment point has authority, every adverse outcome has recourse, closure is reachable, EVOLVE exists, etc.) with its status: PASS or FAIL with specific reason.

This is the most important verification surface. A protocol with failing proof contracts cannot go LIVE. The proof contract view should feel like a pre-flight checklist — clear, binary, no ambiguity.

```
PROOF CONTRACTS                               4/6 PASSING

  ✓ PC_AUTHORITY
    Every commitment point has its authority gate defined.

  ✓ PC_EVIDENCE
    Every commitment point has satisfiable evidence requirements.

  ✗ PC_RECOURSE                                    FAILING
    Every adverse outcome must have recourse defined.
    ISSUE: CP_RENEWAL outcome RENEWAL_DENIED has no
    recourse architecture defined.
    [Go to CP_RENEWAL → Recourse]

  ✓ PC_OVERRIDE
    Every OVERRIDE path has compensating controls.

  ✗ PC_CLOSURE                                     FAILING
    Closure must be reachable from every state.
    ISSUE: No CLOSE commitment point defined for
    withdrawn applications.
    [Add CLOSE for withdrawal]

  ✓ PC_EVOLVE
    The protocol must be changeable (EVOLVE exists).
```

Each failing contract links directly to the specific commitment point and section that needs attention. One click takes you there.

**3.3.6 Protocol Meta**

Protocol name, version, status (DRAFT/LIVE), institution, regulatory basis, design guardrails, purpose statement. Also shows version history if multiple versions exist, with diffs between versions.

**3.3.7 Cross-Protocol**

Events this protocol emits (what other protocols can listen for), events it consumes (what it reacts to from other protocols), shared registry contributions (what this protocol adds to the person registry, property registry, document vault), and evidence reuse rules.

---

### 3.4 THE EDIT EXPERIENCE

**Principle:** Edits are always contextual, structured, and diffed. You never edit raw YAML. You never edit the protocol "globally" — you edit a specific element of a specific commitment point, or a specific cross-cutting definition.

**How edits work:**

1. Every editable element has a small "edit" affordance (pencil icon, or a subtle button that appears on hover). Clicking it opens an inline editing form specific to that element.

2. The editing form is structured. To edit an authority gate, you get a form with: role selector, quorum field, delegation toggle, recording actor field. To add an evidence requirement, you get a wizard: "What does this evidence prove?" → "Who provides it?" → "What level of assurance?" → "How long is it valid?" → "Can it be substituted?"

3. Every edit is tracked. A small diff log accumulates in the session. The user can see "Changes in this session: 3 edits" and review them.

4. Edits can be saved as a draft (staged changes, not yet applied to the protocol) or committed (applied, producing a new protocol version draft that goes through CP_EVOLVE).

**What can be edited:**

- Commitment point properties (description, authority, evidence, reasoning, outcomes, recourse, exceptions, artefacts)
- Evidence type definitions (purpose, source, attestation, validity, substitution)
- Exception types (name, severity, override rules, compensating controls)
- Role definitions (scope, delegation rules)
- Topology relationships (add/remove dependencies, recourse paths)
- Protocol metadata (name, purpose, regulatory references)

**What cannot be edited visually (requires conversational AI):**

- Adding entirely new commitment points (this changes the constitutional structure — too significant for a form)
- Restructuring the topology fundamentally (e.g., splitting one DECIDE into two)
- Creating new cross-protocol interfaces

These structural changes should go through the conversational authoring process, where the AI can ask the right constitutional questions to ensure the change is well-formed.

---

## 4. VISUAL DESIGN DIRECTION

### Overall Aesthetic

The tool should feel like a **legal document meets a modern design tool.** It deals with constitutional structures — authority, evidence, recourse — so it should communicate gravity and precision. But it should also feel approachable and clear, not intimidating.

Think: the precision of a legal brief, the clarity of a well-designed dashboard, the interactivity of Figma.

### Color System

Colors are semantically assigned, not decorative.

**Commitment type colors** — eight distinct colors, one per ACCT type. These are the primary visual vocabulary. They should be distinguishable at small sizes (node badges) and at large sizes (panel headers).

Suggested palette (to be refined by designer):

```
DECIDE    — Red family (institutional commitment, weight, gravity)
ATTEST    — Blue family (evidence, verification, trust)
APPEAL    — Purple (contestation, recourse, counter-flow)
REMEDY    — Indigo (correction, restoration)
OVERRIDE  — Orange (exception, deviation, caution)
EVOLVE    — Teal (growth, change, meta)
CLOSE     — Gray (completion, finality)
DELEGATE  — Gold/amber (trust transfer, authority sharing)
```

**Attestation level colors** — used in evidence displays:
```
Verified  — Green (highest assurance)
Observed  — Blue (system-observed)
Asserted  — Amber (self-declared, lower assurance)
Anchored  — Dark green (tamper-evident, highest)
```

**Severity colors** — used in exception displays:
```
Critical  — Red
Warning   — Amber
Info      — Blue
```

**Constitutional completeness** — used in node indicators and proof contracts:
```
Complete  — Green dot/ring
Partial   — Amber dot/ring
Missing   — Red dot/ring
```

### Typography

Two families:
- **Monospace** (e.g., IBM Plex Mono, JetBrains Mono) — for IDs, type badges, technical identifiers, code-like elements
- **Sans-serif** (e.g., IBM Plex Sans, Söhne, or similar) — for all readable text: names, descriptions, form labels

The monospace is used sparingly — only where precision matters (type labels, evidence IDs, version numbers). Everything else is the readable sans-serif.

### Spatial Design

- Generous whitespace in the detail panel. Constitutional signatures are dense — they need room to breathe.
- The topology canvas should feel open and navigable, not cramped.
- Cards and sections use subtle borders and backgrounds to create visual grouping without heavy visual weight.
- Depth is minimal — one level of shadow for the detail panel, otherwise flat.

---

## 5. RESPONSIVE CONSIDERATIONS

The primary use is desktop (protocol design is a focused, large-screen activity). However, the viewing mode (not editing) should work on tablet for Board members or administrators reviewing a protocol during a meeting.

On tablet:
- The topology view simplifies to a list of commitment points organized by tier, with expand/collapse for detail.
- The detail panel opens full-screen rather than as a side panel.
- Cross-cutting views are full-screen.
- Editing is not available on tablet.

---

## 6. RELATIONSHIP TO CONVERSATIONAL AUTHORING

The viewer/editor and the conversational AI authoring tool are two surfaces of the same system. They share the protocol definition as their common data layer.

```
┌─────────────────────────────────────────────┐
│                                             │
│  CONVERSATIONAL AUTHORING (AI-guided)       │
│  "Tell me about your process..."            │
│  Creates and restructures protocols         │
│                                             │
│              ↕ Protocol YAML ↕              │
│                                             │
│  VISUAL VIEWER/EDITOR                       │
│  Inspect, verify, refine protocols          │
│  Contextual, structured edits              │
│                                             │
└─────────────────────────────────────────────┘
```

The handoff works in both directions:

**Conversation → Viewer:** After the AI generates or modifies a protocol, the user can switch to the viewer to see what was created. "Show me what this looks like" opens the topology view of the protocol the conversation just produced.

**Viewer → Conversation:** When the user identifies a structural change needed (not just a property edit, but a constitutional restructuring), the viewer offers "Discuss this change with AI" which opens the conversational authoring with the specific context pre-loaded. Example: user is looking at the topology and realizes they need a new DECIDE commitment point between verification and the main decision. They click "Add commitment point (via conversation)" and the AI asks the constitutional questions specifically about this new addition.

This bidirectional flow means the two surfaces complement each other rather than competing. The conversation handles creation and structural change. The viewer handles inspection, verification, and targeted refinement.

---

## 7. WHAT SUCCESS LOOKS LIKE

A protocol owner who has never seen ACCT before should be able to:

1. **Within 30 seconds** of opening a protocol in the viewer: understand how many commitment points exist, see the general shape of the topology, and identify the central decision.

2. **Within 2 minutes:** click into the central decision, read its authority gate and evidence requirements, and understand what makes this commitment legitimate.

3. **Within 5 minutes:** navigate the cross-cutting views, identify any proof contract failures, and understand what needs to be fixed.

4. **Within 10 minutes:** make a targeted edit (e.g., add a new exception type to a commitment point) and see the diff.

An auditor should be able to:

1. Open the proof contracts view and immediately see whether the protocol is constitutionally complete.
2. Click into any commitment point and trace its evidence requirements back to their sources.
3. Follow any adverse outcome to its recourse architecture.
4. Verify that every OVERRIDE has compensating controls.

A Board member should be able to:

1. Look at the topology and find the commitment point where they have authority.
2. Click into it and see what evidence will be presented to them and what outcomes they can choose.
3. Understand what happens downstream of each outcome — especially what recourse the applicant has if denied.

None of these users should need to read YAML, understand ACCT's theoretical framework, or learn new vocabulary beyond the eight commitment type names (which the tool teaches through consistent visual association).
