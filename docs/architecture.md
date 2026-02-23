# ICAD Architecture — Master Reference

**Version:** 0.1  
**Date:** February 2026  
**Status:** Design hypothesis — validated through carta de agua analysis  

---

## 0. THE THESIS

Institutions make commitments. Commitments require authority, evidence, reasoning, and recourse. Today, these requirements are enforced by human memory, paper checklists, and institutional culture — all of which fail under load, turnover, and growth pressure.

ACCT (Agentic Constitutional Commitment Typology) models institutional commitments as a formal type system. ICAD is the platform that executes ACCT protocols, with AI agents operating within constitutional boundaries enforced by code.

The thesis: **an AI agent that reads a constitutional protocol can handle 80% of institutional work — navigation, evidence collection, validation, analysis, communication, artefact preparation — while a thin coded layer enforces 100% of the constitutional constraints, and humans retain authority over the commitments that require their judgment.**

The result: institutions that are faster (agent handles routine work), more consistent (constitutional constraints are invariant), more transparent (every commitment produces a receipt), more auditable (audit is graph traversal, not investigation), and safely evolvable (protocol changes are governed commitments).

---

## 1. THE THREE ARTIFACTS

The ICAD architecture separates concerns into three artifacts. Each has a different owner, change frequency, and portability:

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  PROTOCOL DEFINITION                                    │
│                                                         │
│  Owner:      Protocol designer (with AI assistance)     │
│  Format:     YAML                                       │
│  Changes:    Through governed change (CP_EVOLVE)        │
│  Portable:   Yes — same protocol works at any           │
│              institution in the same regulatory domain   │
│                                                         │
│  Contains:                                              │
│  - Commitment points + constitutional signatures        │
│  - Commitment topology (dependencies, recourse,         │
│    obligations, supersedes, governed_by)                 │
│  - Evidence type system (typed, with attestation        │
│    levels, validity, substitution, contestation)        │
│  - Exception taxonomy (named types + UNCLASSIFIED)      │
│  - Recourse architecture                                │
│  - Artefact specifications                              │
│  - Proof contracts (the compiler)                       │
│  - Agent instructions (natural language guidance         │
│    for Claude at each extension point)                  │
│  - Cross-protocol interfaces (events, shared            │
│    registries, evidence reuse rules)                    │
│                                                         │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                                                         │
│  DEPLOYMENT CONFIGURATION                               │
│                                                         │
│  Owner:      Institution (ASADA administrator/IT)       │
│  Format:     YAML                                       │
│  Changes:    Operational — no governed change needed     │
│  Portable:   No — specific to one institution           │
│                                                         │
│  Contains:                                              │
│  - Institution identity and context                     │
│  - Available channels (WhatsApp, email, web, physical)  │
│  - Available integrations (billing system, Drive,       │
│    Sheets, external APIs)                               │
│  - Artefact templates (document files, PDF formats)     │
│  - Role assignments (who specifically fills each role)  │
│  - Local rules (languages, timezone, sectors,           │
│    business day definitions)                            │
│  - Feature flags (no-factibilidad toggle, etc.)         │
│                                                         │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                                                         │
│  EXECUTION ENGINE                                       │
│                                                         │
│  Owner:      ICAD platform team                         │
│  Format:     Code (Python + infrastructure)             │
│  Changes:    Platform releases                          │
│  Portable:   Yes — same engine runs any protocol        │
│              at any institution                         │
│                                                         │
│  Contains:                                              │
│  - Claude (the constitutional agent)                    │
│  - Gate checker (hard constitutional enforcement)       │
│  - State store (cases, receipts, obligations)           │
│  - Evidence store (document vault)                      │
│  - Channel router (WhatsApp, email, web)                │
│  - Template renderer (PDF, DOCX generation)             │
│  - Integration adapters (billing, Drive, Sheets)        │
│  - Receipt writer (append-only, tamper-evident)         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### The Separation Principle

The protocol defines WHAT must be true. The deployment config defines WITH WHAT. The engine provides HOW.

- Change the protocol → the constitutional structure changes (governed).
- Change the deployment config → the infrastructure changes (operational).
- Change the engine → the platform capabilities change (release).

No artifact depends on the internal details of another. The protocol doesn't know which billing system is deployed. The deployment config doesn't know the protocol's internal topology. The engine doesn't know the domain — it reads both artifacts and connects them.

---

## 2. CLAUDE AS THE CONSTITUTIONAL AGENT

### The Role

Claude is the primary operator of the ICAD platform. It reads the protocol definition and deployment configuration as context, and performs all navigation tasks — everything between commitment points.

Claude handles:
- Conversational intake with applicants (collecting information, answering questions, explaining requirements)
- Evidence collection (guiding document uploads, validating formats, extracting data)
- Evidence validation (checking completeness, dates, cross-references, type conformance)
- Demand estimation and analysis (applying coefficients, comparing to thresholds)
- Anomaly detection (flagging patterns that match exception types)
- Artefact drafting (generating carta documents, denial letters, Board packages)
- Communication (sending notifications, status updates, reminders in the right language through the right channel)
- Cross-protocol coordination (emitting events, checking shared registries)
- Status reporting (answering "where is my application?")
- Preparing commitment packages (assembling everything the human authority needs to make a decision)

Claude does NOT handle:
- Making binding commitments (unless explicitly delegated via DELEGATE commitment)
- Overriding constitutional constraints
- Changing the protocol
- Deciding outcomes at authority-gated commitment points
- Communicating decisions without human approval (at commitment points that require it)

### The Context Stack

Claude's system prompt for any given interaction contains:

```
┌─────────────────────────────────────────────────────────┐
│  LAYER 1: ACCT Framework Primer                         │
│  How to interpret ACCT protocols. The eight commitment  │
│  types. Constitutional signatures. Evidence type        │
│  system. The commitment/navigation distinction.         │
│  How to read agent_instructions.                        │
├─────────────────────────────────────────────────────────┤
│  LAYER 2: Active Protocol Definition                    │
│  The specific protocol being executed (e.g., carta de   │
│  agua). Commitment points, topology, evidence types,    │
│  exception taxonomy, agent instructions.                │
├─────────────────────────────────────────────────────────┤
│  LAYER 3: Deployment Configuration                      │
│  The institution's specific setup. Channels,            │
│  integrations, templates, role assignments, local rules.│
├─────────────────────────────────────────────────────────┤
│  LAYER 4: Current Case State                            │
│  Where this specific case is. Which commitment points   │
│  are satisfied. Which evidence exists. What's missing.  │
│  Current gate status. Outstanding obligations.          │
├─────────────────────────────────────────────────────────┤
│  LAYER 5: Active Delegations                            │
│  What commitments Claude is authorized to make.         │
│  Delegation scope, duration, and conditions.            │
├─────────────────────────────────────────────────────────┤
│  LAYER 6: Interaction Context                           │
│  Who Claude is talking to (applicant, admin, operator). │
│  Which channel (WhatsApp, web, dashboard).              │
│  Conversation history for this interaction.             │
└─────────────────────────────────────────────────────────┘
```

Claude reasons about all six layers to determine what to do next in any given interaction.

### The Agent Instructions Pattern

The protocol contains natural language instructions for Claude at each extension point. These instructions are:
- **Version-controlled** — they're part of the protocol, so changes go through CP_EVOLVE
- **Domain-specific** — written by the protocol designer who understands the institutional context
- **Auditable** — the instructions that governed Claude's behavior are recorded in the receipt provenance
- **Evolvable** — as Claude's capabilities improve, instructions can be simplified; as the institution learns, instructions can be refined

Example:

```yaml
evidence_types:
  certificacion_literal:
    # ... constitutional properties ...
    
    collection:
      method: "document_upload"
      agent_instructions: >
        Ask the applicant to provide their certificación literal
        from the Registro Nacional. It must be less than 30 days
        old from the date of issuance. Accept image or PDF.
        
        Check that:
        1. The document is legible
        2. You can identify the issuance date
        3. The issuance date is within 30 days
        4. The Folio Real number matches what the applicant provided
        5. The owner name matches the applicant (or the authorization chain)
        
        If the document is older than 25 days, warn the applicant
        that it may expire during processing and suggest obtaining
        a fresh one.
        
        If the document is older than 30 days, do not accept it.
        Explain that per RPSAyA regulations, the certificación
        must be current, and guide them to obtain a new one
        (available via rnpdigital.com or at the Registro Nacional office).
        
        If you cannot determine the date or read the document,
        ask for a clearer photo.
        
        Store the extracted Folio Real number and issuance date
        as evidence metadata.
```

These instructions tell Claude exactly how to handle this evidence type, including edge cases (approaching expiry), validation rules, and user guidance. They're specific enough to be reliable but natural enough to allow Claude to adapt to conversational context.

---

## 3. THE GATE CHECKER (Hard Constitutional Enforcement)

### Why It Exists

Claude operating within a protocol is a soft constraint. Claude reads the protocol and follows it — but there's no mechanical guarantee. If the protocol says "only the Board can commit at CP_AVAILABILITY_DECISION," Claude will respect this. But constitutional legitimacy requires more than good behavior — it requires enforcement.

The gate checker is the hard constraint. It's a coded component (not AI) that enforces constitutional signatures at commitment time. It's the difference between "Claude follows the rules" and "the system makes it impossible to break the rules."

### What It Does

When any actor (Claude, administrator, Board via admin recording) attempts to make a commitment, the attempt passes through the gate checker before it becomes binding:

```
Actor attempts commitment
        │
        ▼
┌───────────────────────────────────┐
│  GATE CHECKER                     │
│                                   │
│  1. AUTHORITY CHECK               │
│     Is this actor authorized at   │
│     this commitment point?        │
│     Is there a valid DELEGATE?    │
│     Is quorum met (if required)?  │
│     → Block with reason if NO     │
│                                   │
│  2. EVIDENCE CHECK                │
│     Are all required evidence     │
│     types present in the store?   │
│     Do attestation levels meet    │
│     minimums?                     │
│     Are validity windows current? │
│     → Block with specific         │
│       missing items if NO         │
│                                   │
│  3. REASONING CHECK               │
│     Is reasoning provided         │
│     (if required)?                │
│     Does it meet minimum          │
│     structure?                    │
│     → Block with prompt if NO     │
│                                   │
│  4. DEPENDENCY CHECK              │
│     Are all DEPENDS_ON            │
│     commitments satisfied?        │
│     → Block with specific         │
│       unsatisfied deps if NO      │
│                                   │
│  5. VERSION BINDING               │
│     Bind to ACTIVE protocol       │
│     version at this moment.       │
│                                   │
│  6. RECOURSE CHECK                │
│     If outcome is adverse:        │
│     is recourse architecture      │
│     defined?                      │
│     → Block if adverse outcome    │
│       has no recourse defined     │
│                                   │
│  ALL GATES PASS                   │
│        │                          │
│        ▼                          │
│  7. GENERATE RECEIPT              │
│     Append-only. Includes:        │
│     commitment type, point,       │
│     version, authority, relied-on │
│     set, reasoning, outcome,      │
│     recourse, provenance,         │
│     timestamp, automation level.  │
│                                   │
│  8. TRIGGER DOWNSTREAM            │
│     Create obligations.           │
│     Open recourse windows.        │
│     Emit cross-protocol events.   │
│     Fire artefact generation.     │
│                                   │
└───────────────────────────────────┘
        │
        ▼
  Commitment is binding.
  Receipt is authoritative.
```

### What It Is (Code)

The gate checker is simple, deterministic code. It does not use AI. It reads:
- The commitment point's constitutional signature (from the protocol)
- The current case state (from the state store)
- The actor's identity and role (from the session)
- The active delegations (from the delegation registry)

And it produces a binary result: PASS (commitment proceeds, receipt generated) or BLOCK (commitment rejected, specific reasons returned).

The gate checker is the smallest, most critical piece of coded infrastructure. It must be correct, tested, and auditable. It's the constitutional firewall that makes the 80% agentic automation trustworthy.

### The Automation Level Tag

Every receipt records how the commitment was made:

```
MANUAL          — Human made the commitment directly
AI_ASSISTED     — AI prepared; human committed
AI_OVERSIGHT    — AI committed under DELEGATE; human can review
AUTOMATED       — AI committed under DELEGATE; no human in loop
```

This is recorded in the receipt, not configured in the protocol. The same commitment point might be MANUAL for one case and AI_OVERSIGHT for another, depending on the active delegations. The receipt preserves this for audit.

---

## 4. THE THIN INFRASTRUCTURE LAYER

Everything that isn't Claude and isn't the gate checker is infrastructure. It's thin, generic, and protocol-agnostic.

### 4.1 State Store

**What it stores:**
- Case records (one per application/request)
- Commitment receipts (append-only ledger per case)
- Evidence metadata (what evidence exists, attestation levels, validity)
- Gate status (current evaluation of each commitment point's signature)
- Obligations (outstanding duties created by prior commitments)
- Delegation registry (active DELEGATEs with scope and duration)

**Technology:** PostgreSQL or equivalent relational database. The schema is derived from ACCT primitives, not from any specific protocol. Cases have commitment points; commitment points have receipts; receipts have relied-on sets; relied-on sets reference evidence.

**Key property:** The receipt ledger is append-only. Receipts cannot be edited or deleted. They can only be superseded by subsequent commitments. This is the audit trail.

### 4.2 Evidence Store

**What it stores:** The actual documents — images, PDFs, scans. Separate from evidence metadata (which is in the state store).

**Technology:** Cloud storage (Google Drive for Nosara, S3 or equivalent for others). Each document has a URI, a hash (for integrity), and metadata linking it to the evidence type and case.

**Key property:** Documents are immutable once stored. If a new version is needed, it's a new document with a new URI.

### 4.3 Channel Router

**What it does:** Routes messages between Claude and the outside world. Claude composes messages; the channel router delivers them through the appropriate channel.

**Channels:**
- WhatsApp Business API (primary for applicants in Nosara)
- Email (secondary for applicants, primary for formal notices)
- Web interface (for admin dashboard, operator mobile)
- Physical (printable outputs for Board, office pickup)

**Technology:** Channel-specific adapters. Each adapter handles the API integration (WhatsApp Business API, SMTP, web sockets) and normalizes the interface so Claude doesn't need to know channel specifics.

**Key property:** Channel selection is driven by the deployment config and the protocol's delivery preferences. Claude says "send this notification to the applicant"; the router determines the channel based on the applicant's preferences and available channels.

### 4.4 Template Renderer

**What it does:** Generates formatted documents (PDFs, DOCX) from templates populated with case data.

**Technology:** Python document generation (python-docx, WeasyPrint, or similar). Templates are DOCX or HTML files stored in the deployment config's template directory.

**How it works:** Claude prepares the data payload (all fields for the artefact). The renderer takes the data + template and produces the formatted document. Claude reviews the output for correctness (if required by the artefact spec) before it enters the delivery pipeline.

### 4.5 Integration Adapters

**What they do:** Connect to external systems referenced in the deployment config.

**Adapters for Nosara (initial):**
- Google Drive adapter (file storage and archival)
- Google Sheets adapter (tracking sheet sync)
- CISA adapter (initially manual — admin confirms; future: API wrapper)

**Key property:** Adapters are deployment-specific. The protocol references abstract system types ("billing", "document_management"); the deployment config maps them to specific systems; the adapter provides the connection.

### 4.6 Receipt Writer

**What it does:** Writes commitment receipts to the state store. Ensures append-only integrity. Generates receipt IDs. Links receipts to their provenance chain.

**Key property:** The receipt writer is the only component that writes to the receipt ledger. Claude provides the receipt content (via the gate checker); the receipt writer ensures integrity.

---

## 5. HOW A CASE FLOWS (Carta de Agua Example)

### 5.1 Applicant Contacts ASADA via WhatsApp

```
Applicant sends: "Hola, necesito una carta de disponibilidad de agua"

Channel router → routes to Claude

Claude reads:
  - Protocol: CDA carta de agua
  - Deployment: Nosara, WhatsApp channel
  - Case state: No existing case for this phone number
  - Delegations: Navigation authorized, no commitment delegation yet

Claude responds (following protocol's agent_instructions for CP_SUBMIT):
  "¡Hola! Soy el asistente de ASADA Playas de Nosara. Puedo ayudarle
   con el proceso de solicitud de Carta de Disponibilidad de Agua.
   
   ¿En qué idioma prefiere continuar? / Which language do you prefer?"

[Navigation begins — Claude guides through intake conversation,
 collecting applicant identity, property data, project description.
 This is all NAVIGATION — no commitments yet.]
```

### 5.2 Evidence Collection

```
Claude (following agent_instructions for EV_CERTIFICACION_LITERAL):
  "Ahora necesito la certificación literal de su propiedad. Debe tener
   menos de 30 días de emitida. Puede enviarme una foto o PDF."

Applicant sends: [photo of certificación literal]

Claude:
  - Receives image via channel router
  - Stores in evidence store (gets URI and hash)
  - Examines document (following agent_instructions):
    - Is it legible? Yes
    - Can I find the issuance date? Yes — January 28, 2026
    - Is it within 30 days? Yes (today is Feb 22 — 25 days)
    - Folio Real matches application? Yes — 5-123456-000
    - Owner name matches? Yes — Juan Carlos Pérez Mora
  - Stores evidence metadata in state store:
    type: EV_CERTIFICACION_LITERAL
    attestation: Verified (official source)
    valid_until: 2026-02-27 (30 days from issuance)
    extracted_fields: {folio_real: "5-123456-000", issue_date: "2026-01-28"}
  
  - Notes approaching expiry (25 of 30 days):
    "He recibido su certificación literal. Está vigente pero le quedan
     solo 5 días de validez. Si el proceso toma más tiempo, podría
     necesitar obtener una nueva."
```

### 5.3 Claude Attempts a Delegated Commitment

```
[All evidence collected. Claude checks protocol — CP_ADMISSIBILITY
 is the next commitment point. Claude has a DELEGATE for
 CP_ADMISSIBILITY on Tier 1 applications.]

Claude prepares commitment attempt:
  commitment_point: CP_ADMISSIBILITY
  actor: AI_AGENT (under DELEGATE-2026-001)
  outcome: ADMISSIBLE
  reasoning: "All RPSAyA Art. 30 requirements satisfied. Property is
    inscrito. Cédula verified. Certificación literal valid (5 days
    remaining). Plano catastrado number confirmed. Project classified
    as Tier 1 vivienda unifamiliar."
  relied_on_set: [EV_CEDULA_FISICA, EV_CERTIFICACION_LITERAL,
    EV_PLANO_CATASTRADO, EV_PROJECT_DESCRIPTION]

Claude → Gate Checker:

  Gate checker evaluates:
    1. AUTHORITY: AI_AGENT at CP_ADMISSIBILITY?
       → Check delegation registry
       → DELEGATE-2026-001 found: scope=CP_ADMISSIBILITY for Tier 1
       → This case is Tier 1
       → PASS
    2. EVIDENCE: All required types present?
       → Art. 30 checklist: cédula ✓, certificación ✓, plano ✓,
         project description ✓
       → Morosidad: NOT YET (separate commitment point)
       → But morosidad is not required at CP_ADMISSIBILITY,
         it's required at CP_AVAILABILITY_DECISION
       → PASS
    3. REASONING: Provided? Yes. Structured? Yes.
       → PASS
    4. DEPENDENCIES: CP_SUBMIT satisfied? Yes.
       → PASS
    5. VERSION: Bind to CDA v0.1
    6. RECOURSE: Outcome is ADMISSIBLE (non-adverse) — no recourse needed
  
  ALL GATES PASS
  
  → Receipt generated:
    receipt_id: RCP-2026-00892
    commitment_type: DECIDE
    commitment_point: CP_ADMISSIBILITY
    protocol_version: CDA-0.1
    case_id: CDA-2026-045
    authority: AI_AGENT (via DELEGATE-2026-001)
    automation_level: AI_OVERSIGHT
    relied_on_set: [EV_CEDULA_FISICA, EV_CERTIFICACION_LITERAL, ...]
    reasoning: "All RPSAyA Art. 30 requirements satisfied..."
    outcome: ADMISSIBLE
    occurred_at: 2026-02-22T14:32:00-06:00

Claude notifies administrator:
  "Application CDA-2026-045 has been assessed as admissible.
   I verified all Art. 30 requirements. Please confirm morosidad
   in CISA for Juan Carlos Pérez Mora, cédula 1-1234-0567."
```

### 5.4 Administrator Makes a Commitment

```
Administrator opens web dashboard (or responds via WhatsApp).

Claude (in admin channel):
  "CDA-2026-045 — Juan Carlos Pérez Mora
   Vivienda unifamiliar, Sector Guiones
   
   I need you to verify morosidad in CISA.
   Applicant: Juan Carlos Pérez Mora
   Cédula: 1-1234-0567
   Property: Folio Real 5-123456-000
   
   Please check and confirm."

Administrator checks CISA, confirms no debt.

Administrator: "Confirmed, no morosidad"

Claude prepares commitment attempt:
  commitment_point: CP_MOROSIDAD
  actor: ADMINISTRATOR
  outcome: NO_MOROSIDAD
  evidence: EV_MOROSIDAD (administrator attestation)

Claude → Gate Checker:
  1. AUTHORITY: ADMINISTRATOR at CP_MOROSIDAD? → PASS
  2. EVIDENCE: EV_MOROSIDAD present? → Administrator just attested → PASS
  [... all gates pass ...]
  
  → Receipt generated.
```

### 5.5 Board Decision (Human Authority, Agent Records)

```
[Application has passed CP_ADMISSIBILITY, CP_MOROSIDAD,
 CP_ADMIN_VERIFICATION, and CP_TECHNICAL_ASSESSMENT.
 All gates at CP_AVAILABILITY_DECISION are green except
 the commitment itself — waiting for Board meeting.]

Before the meeting, Claude generates the Board package
(following artefact spec for ART_BOARD_SHEET):
  - One-page printable summary per application
  - Agenda cover sheet listing all applications for review
  - Template renderer produces PDFs
  - Administrator prints them

After the meeting, administrator enters the Board's decision:

Administrator: "The Board approved CDA-2026-045, standard conditions,
  Acta 2026-008, quorum confirmed with 5 members present."

Claude prepares commitment attempt:
  commitment_point: CP_AVAILABILITY_DECISION
  actor: BOARD (recorded by ADMINISTRATOR)
  outcome: APPROVED
  reasoning: "Tier 1 vivienda unifamiliar in Sector Guiones.
    System has capacity. Pipeline exists at property.
    Standard demand 0.86 m³/day. No detriment to existing service."
  relied_on_set: [all prior evidence + EV_ACTA]
  acta_reference: "2026-008"
  members_present: 5
  quorum_confirmed: true

Claude → Gate Checker:
  1. AUTHORITY: BOARD at CP_AVAILABILITY_DECISION?
     → Actor is ADMINISTRATOR recording for BOARD
     → Quorum confirmed (5 of 7, minimum 4)
     → PASS
  2. EVIDENCE: Technical assessment ✓, demand estimate ✓,
     morosidad ✓, complete package ✓, acta ✓
     → PASS
  [... all gates pass ...]
  
  → Receipt generated. This is the central commitment of the case.
  
  → Downstream triggers:
     - Obligation created: generate carta (CP_CARTA_ISSUANCE)
     - Cross-protocol event: carta_approved → billing protocol
     - Notification: applicant informed of decision

Claude notifies applicant:
  "¡Buenas noticias! La Junta Directiva ha aprobado su solicitud
   CDA-2026-045. Su Carta de Disponibilidad está siendo preparada.
   Le notificaremos cuando esté lista para recoger o se la
   enviaremos digitalmente."
```

---

## 6. THE VIEWER/EDITOR IN THIS ARCHITECTURE

The protocol viewer/editor (specified in the UX document) connects to this architecture as follows:

- **Viewing mode** reads the protocol YAML and renders the topology, constitutional signatures, evidence catalog, exception taxonomy, and proof contracts.

- **Editing mode** produces structured diffs to the protocol YAML. These diffs accumulate as a change dossier for CP_EVOLVE.

- **Conversational authoring** (AI-guided protocol creation and structural changes) produces new protocol YAML versions that the viewer renders.

The viewer/editor is a design-time tool. It does not interact with the execution engine, state store, or live cases. It operates on the protocol artifact only.

A separate **operations dashboard** (which Claude powers) shows live case status, queue views, and commitment interfaces. This is the runtime surface. It reads from the state store and renders projections per the protocol's projection specs.

---

## 7. THE DELEGATION LIFECYCLE

### How Agents Earn Trust

```
PHASE 1: Navigation Only (Weeks 1-4)
  Claude performs all navigation tasks.
  All commitments are MANUAL (human makes them).
  Measurement: accuracy of Claude's assessments vs. human decisions.

PHASE 2: First DELEGATE (Weeks 4-8)
  Based on Phase 1 data (e.g., >95% accuracy on admissibility):
  
  Administrator issues DELEGATE:
    commitment_point: CP_ADMISSIBILITY
    scope: Tier 1 applications only
    duration: 3 months
    oversight: Admin notified of every AI commitment, can override within 24h
    revocation: Immediate if error rate exceeds 5%
  
  This DELEGATE is itself a commitment:
    → Goes through the gate checker
    → Produces a receipt
    → Is in the provenance chain of every AI commitment made under it
  
  Claude now commits CP_ADMISSIBILITY for Tier 1 cases.
  Automation level: AI_OVERSIGHT.
  Receipts record the DELEGATE reference.

PHASE 3: Expanded Delegation (Months 3+)
  Based on Phase 2 performance data:
  - If AI admissibility decisions match human decisions >98%
  - If override rate is <2%
  - If no appeals resulted from AI-committed admissibility
  
  Consider expanding:
  - CP_ADMISSIBILITY for Tier 2 applications
  - Preliminary analysis at CP_TECHNICAL_ASSESSMENT (draft, human confirms)
  
  NEVER delegated (architectural constraint):
  - CP_AVAILABILITY_DECISION (Board authority — constitutional)
  - CP_CARTA_ISSUANCE (President signing — legal)
  - CP_OVERRIDE (exception governance — human judgment)
  - CP_APPEAL (independent review — human judgment)
  - CP_EVOLVE (protocol change — institutional governance)
```

---

## 8. PROTOCOL INTEROPERABILITY

### How Protocols Talk to Each Other

Protocols communicate through three mechanisms, all mediated by the engine:

**Events:** When a commitment produces a receipt, the engine checks the protocol's cross-protocol section for events to emit. Other protocols' event handlers (also defined in their YAML) receive these events and create appropriate effects (new cases, flags, state updates).

**Shared Registries:** The person registry, property registry, service registry, and document vault are platform-level stores shared across all protocols. Each protocol contributes to and reads from these registries. Evidence collected in one protocol is available to others (subject to reuse rules defined in each evidence type).

**Evidence Reuse:** When a protocol requires evidence that already exists in the document vault from another protocol, the engine checks the reuse rules. If the evidence is reusable and still valid, the user is not asked to provide it again. If it's expired or non-reusable, a new collection is required.

Claude orchestrates all of this. When processing a carta de agua application, Claude checks the shared registries: "Has this person applied before? Does this property have history in other protocols? Is there valid evidence in the vault we can reuse?" This is navigation — Claude's natural strength.

---

## 9. WHAT TO BUILD FIRST (The Carta de Agua Vertical)

### Build Order

**Step 1: The Protocol YAML**
Already drafted (CDA_protocol_ACCT_v01.yaml). Needs:
- Addition of agent_instructions at all extension points
- Addition of collection blocks for all evidence types
- Addition of projection blocks for all commitment points
- Addition of production blocks for all artefacts
- Review and refinement based on this architecture document

**Step 2: The Deployment Configuration**
Write the Nosara-specific YAML:
- WhatsApp channel config
- Google Drive integration
- Google Sheets integration
- CISA manual procedure
- Artefact templates
- Role assignments
- Local rules

**Step 3: The Gate Checker**
Simple, deterministic Python code:
- Read commitment point signature from protocol
- Evaluate authority, evidence, reasoning, dependencies
- Return PASS or BLOCK with reasons
- Generate receipt on PASS
- This is the most critical piece — it must be correct

**Step 4: The State Store**
PostgreSQL schema derived from ACCT primitives:
- Cases, receipts, evidence records, obligations, delegations
- Receipt ledger is append-only

**Step 5: Claude Integration**
System prompt assembly:
- ACCT primer + protocol + deployment config + case state
- Tool definitions for: state store read/write, evidence store, channel router, gate checker
- Test with simulated cases end-to-end

**Step 6: Channel Integration**
WhatsApp Business API (or manual WhatsApp bridge for MVP):
- Incoming messages → Claude
- Outgoing messages ← Claude
- Document uploads → evidence store

**Step 7: Template Renderer**
PDF generation for cartas, denial letters, Board packages:
- DOCX templates populated with case data
- Print-ready formatting

**Step 8: The Viewer/Editor**
Protocol visualization and editing surface:
- Topology view, commitment detail, cross-cutting views
- Per the UX specification

### What MVP Looks Like

An applicant sends a WhatsApp message to ASADA Nosara. Claude responds, guides them through the application, collects their documents, validates evidence, and produces a complete application package. The administrator reviews (Claude has prepared everything), confirms morosidad, and routes to the Board. The Board meets with a printed package generated by Claude. After the meeting, the administrator enters the decision. Claude generates the carta, notifies the applicant, and tracks validity for renewal. Every step produces a receipt. Every commitment passes through the gate checker. The protocol governs the entire process.

That's the MVP. It works for one protocol at one ASADA. And the architecture ensures it scales to many protocols at many ASADAs without rebuilding.

---

## 10. SUCCESS CRITERIA

### For the Carta de Agua Vertical (60-day test)

**Recurring use:** The administrator processes applications through ICAD daily.

**One governed change shipped:** Based on real operational data, the protocol has been evolved at least once (a new exception type, an adjusted evidence requirement, a refined agent instruction) through CP_EVOLVE.

**Audit packet trusted:** The Fiscal or an AyA auditor can reconstruct "what happened and why" for any case from the receipt chain alone.

**Measurable outcome delta:**
- Administrator time per application: >50% reduction
- Applicant time to status visibility: from "unknown" to "instant"
- Incomplete applications reaching the Board: near zero
- Applications processed per Board meeting: >2x increase

### For the Platform (12-month test)

**Second protocol live:** At least one additional protocol (billing or rationing) running on the same engine at Nosara.

**Second ASADA deployed:** At least one additional ASADA running the carta de agua protocol with their own deployment configuration.

**AI delegation active:** At least one commitment point operating under AI_OVERSIGHT with positive performance metrics.

**Protocol evolution demonstrated:** Multiple governed changes shipped across protocols, with measurable impact data.
