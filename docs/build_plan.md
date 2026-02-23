# ICAD MVP — Build Plan for Claude Code

**Version:** 0.1  
**Date:** February 2026  
**Purpose:** Everything needed to build the ICAD platform MVP (carta de agua at ASADA Nosara) using Claude Code as the primary development tool.

---

## 0. HOW CLAUDE CODE WORKS BEST

Claude Code reads repository context — files, documentation, code — to understand what to build and how. It works best when:

1. **The architecture is documented before coding begins.** Claude Code shouldn't have to infer architectural decisions. They should be explicit in documents it can read.

2. **Each component has a clear specification.** Inputs, outputs, interfaces, constraints. Claude Code builds against specs, not against vague descriptions.

3. **The repository structure is navigable.** A clear directory layout with a top-level README and a CLAUDE.md file that orients Claude Code to the project.

4. **Decisions are recorded.** When you make an architectural choice (e.g., "use PostgreSQL, not SQLite"), document it where Claude Code will find it. Otherwise it may make different assumptions in different sessions.

5. **Tests define correctness.** Claude Code can write tests and code against them. The gate checker, in particular, should have tests written before implementation — the tests ARE the spec.

---

## 1. REPOSITORY STRUCTURE

```
icad/
│
├── CLAUDE.md                          # Claude Code orientation file
├── README.md                          # Project overview
│
├── docs/                              # All documentation
│   ├── architecture.md                # ICAD master architecture reference
│   ├── acct_primer.md                 # ACCT framework summary (for Claude's context)
│   ├── build_phases.md                # This document's Phase section, extracted
│   └── decisions.md                   # Architecture Decision Records (ADRs)
│
├── protocols/                         # Protocol definitions
│   ├── README.md                      # How protocols are structured
│   ├── carta_de_agua/
│   │   ├── protocol.yaml              # The ACCT protocol definition
│   │   └── README.md                  # Protocol-specific notes
│   └── _base/
│       └── acct_schema.yaml           # ACCT protocol schema (for validation)
│
├── deployments/                       # Deployment configurations
│   ├── README.md                      # How deployments are structured
│   └── nosara/
│       ├── config.yaml                # Nosara deployment configuration
│       ├── templates/                 # Document templates
│       │   ├── carta_disponibilidad.docx
│       │   ├── denegacion.docx
│       │   └── paquete_junta.docx
│       └── README.md                  # Deployment-specific notes
│
├── engine/                            # The execution engine (Python)
│   ├── README.md                      # Engine overview
│   ├── pyproject.toml                 # Python project config
│   │
│   ├── core/                          # Core ACCT primitives (protocol-agnostic)
│   │   ├── __init__.py
│   │   ├── protocol_loader.py         # Reads and validates protocol YAML
│   │   ├── deployment_loader.py       # Reads deployment config YAML
│   │   ├── gate_checker.py            # Constitutional enforcement
│   │   ├── state_manager.py           # Case state management
│   │   ├── receipt_writer.py          # Append-only receipt generation
│   │   ├── evidence_manager.py        # Evidence storage and type checking
│   │   ├── obligation_tracker.py      # Deadline and obligation management
│   │   └── models.py                  # Data models (cases, receipts, evidence, etc.)
│   │
│   ├── agent/                         # Claude integration
│   │   ├── __init__.py
│   │   ├── context_builder.py         # Assembles Claude's system prompt
│   │   ├── tool_definitions.py        # Tools Claude can use
│   │   ├── agent_router.py            # Routes interactions to Claude
│   │   └── prompt_templates/          # System prompt layers
│   │       ├── acct_primer.md         # Layer 1: How to interpret ACCT
│   │       ├── protocol_context.md    # Layer 2: Template for protocol injection
│   │       └── interaction_rules.md   # Layer 6: Conversation guidelines
│   │
│   ├── channels/                      # Channel integrations
│   │   ├── __init__.py
│   │   ├── base.py                    # Abstract channel interface
│   │   ├── whatsapp.py                # WhatsApp Business API adapter
│   │   ├── email_channel.py           # Email (SMTP) adapter
│   │   └── web.py                     # Web interface adapter
│   │
│   ├── integrations/                  # External system adapters
│   │   ├── __init__.py
│   │   ├── base.py                    # Abstract integration interface
│   │   ├── google_drive.py            # Google Drive adapter
│   │   ├── google_sheets.py           # Google Sheets adapter
│   │   └── manual_billing.py          # Manual billing check (CISA placeholder)
│   │
│   ├── artefacts/                     # Document generation
│   │   ├── __init__.py
│   │   ├── renderer.py                # Template renderer (DOCX → PDF)
│   │   └── delivery.py                # Artefact delivery pipeline
│   │
│   └── api/                           # HTTP API layer
│       ├── __init__.py
│       ├── app.py                     # Flask/FastAPI application
│       ├── routes_webhook.py          # Incoming webhooks (WhatsApp, etc.)
│       ├── routes_admin.py            # Admin dashboard API
│       └── routes_internal.py         # Internal API (Claude's tools)
│
├── db/                                # Database
│   ├── README.md                      # Schema documentation
│   ├── migrations/                    # Database migrations
│   │   └── 001_initial.sql
│   └── schema.sql                     # Full schema reference
│
├── tests/                             # Test suites
│   ├── README.md                      # Testing strategy
│   ├── core/
│   │   ├── test_gate_checker.py       # Gate checker tests (WRITE FIRST)
│   │   ├── test_protocol_loader.py
│   │   ├── test_state_manager.py
│   │   ├── test_receipt_writer.py
│   │   └── test_evidence_manager.py
│   ├── agent/
│   │   └── test_context_builder.py
│   ├── integration/
│   │   └── test_case_flow.py          # End-to-end case flow tests
│   └── fixtures/
│       ├── sample_protocol.yaml       # Minimal test protocol
│       └── sample_deployment.yaml     # Minimal test deployment
│
└── scripts/                           # Utility scripts
    ├── validate_protocol.py           # Validate protocol against ACCT schema
    ├── run_proof_contracts.py         # Run proof contract checks
    └── seed_test_data.py              # Seed database with test cases
```

---

## 2. DOCUMENTS TO WRITE BEFORE CODING

The following documents must exist before Claude Code writes any code. They are the specifications that Claude Code builds against.

### 2.1 CLAUDE.md (Repository Orientation)

**Purpose:** The first thing Claude Code reads. Orients it to the project.

**Must contain:**
- One-paragraph project description
- Architecture summary (three artifacts: protocol, deployment config, engine)
- Repository map (where things are and what they do)
- Key conventions (Python version, formatting, naming conventions)
- How to run tests
- Important constraints (e.g., "the gate checker must never use AI — it's deterministic code")
- Links to key documents for deeper context

**Approximate length:** 1-2 pages

---

### 2.2 Architecture Reference (docs/architecture.md)

**Purpose:** Complete architecture context for Claude Code. This is the ICAD architecture document we already wrote, trimmed to what's needed for implementation.

**Must contain:**
- The three-artifact model (protocol, deployment config, engine)
- Claude's role as constitutional agent
- The gate checker's role as hard enforcement
- The thin infrastructure components and their responsibilities
- How a case flows through the system (the worked example from Section 5)
- What Claude handles vs. what code handles
- The context stack (what goes into Claude's system prompt)

**Source:** Adapt from ICAD_architecture_master_reference.md

**Approximate length:** 5-8 pages

---

### 2.3 ACCT Primer (docs/acct_primer.md)

**Purpose:** Concise reference on ACCT for Claude Code (so it understands the model while building) and also serves as Layer 1 of Claude agent's system prompt.

**Must contain:**
- The eight commitment types with one-sentence definitions
- Constitutional signatures explained (authority, evidence, reasoning, version, recourse, receipt)
- The commitment/navigation distinction
- Evidence type system basics (source class, attestation level, validity)
- Receipt schema
- Commitment topology relationship types
- The automation dial and DELEGATE

**Source:** Condense from ACCT_Product_Framework_v2.md

**Approximate length:** 3-4 pages

---

### 2.4 Data Models Specification (docs/data_models.md)

**Purpose:** Defines every data structure in the system. Claude Code uses this to build models.py, the database schema, and all interfaces.

**Must contain:**

```
Case
  - case_id (string, format: "{protocol_id}-{year}-{sequential}")
  - protocol_id (string, references protocol)
  - protocol_version (string, version bound at creation)
  - status (enum: OPEN, CLOSED, EXPIRED, WITHDRAWN)
  - created_at (datetime)
  - closed_at (datetime, nullable)
  - current_position (list of satisfied commitment point IDs)
  - metadata (JSONB — protocol-specific case data)

CommitmentReceipt
  - receipt_id (string, auto-generated, unique)
  - case_id (string, references case)
  - commitment_type (enum: DECIDE, ATTEST, APPEAL, REMEDY, OVERRIDE, EVOLVE, CLOSE, DELEGATE)
  - commitment_point_id (string, references protocol)
  - protocol_version (string, version at time of commitment)
  - actor_id (string, who attempted the commitment)
  - actor_role (string, the role they hold)
  - delegation_ref (string, nullable — DELEGATE receipt ID if AI-committed)
  - automation_level (enum: MANUAL, AI_ASSISTED, AI_OVERSIGHT, AUTOMATED)
  - outcome_key (string, the selected outcome)
  - reasoning (text)
  - relied_on_set (JSONB — array of evidence references with attestation levels)
  - recourse_architecture (JSONB, nullable — populated if outcome is adverse)
  - artefacts_generated (JSONB — array of artefact references)
  - provenance_links (JSONB — references to prior receipts, evidence, external refs)
  - occurred_at (datetime — when the commitment was made)
  - recorded_at (datetime — when the receipt was written)
  - visibility (enum: PUBLIC, INTERNAL, RESTRICTED)

EvidenceRecord
  - evidence_id (string, auto-generated)
  - case_id (string, references case)
  - evidence_type_id (string, references protocol's evidence type)
  - attestation_level (enum: ASSERTED, OBSERVED, VERIFIED, ANCHORED)
  - source_actor (string — who provided or attested)
  - collected_at (datetime)
  - valid_from (datetime)
  - valid_until (datetime, nullable — for time-limited evidence)
  - document_uri (string, nullable — link to file in evidence store)
  - document_hash (string, nullable — integrity check)
  - extracted_metadata (JSONB — fields extracted from the document)
  - status (enum: ACTIVE, SUPERSEDED, CONTESTED, EXPIRED)
  - notes (text, nullable)

Obligation
  - obligation_id (string, auto-generated)
  - case_id (string, references case)
  - created_by_receipt (string, references receipt that created this)
  - obligated_role (string — who owes the obligation)
  - description (text)
  - deadline (datetime, nullable)
  - status (enum: PENDING, SATISFIED, EXPIRED, WAIVED)
  - satisfied_by_receipt (string, nullable — receipt that discharged this)

Delegation
  - delegation_id (string, auto-generated)
  - delegation_receipt (string — the DELEGATE commitment receipt)
  - delegated_from_role (string)
  - delegated_to_actor (string — e.g., "AI_AGENT")
  - commitment_point_id (string — which commitment point)
  - scope_conditions (JSONB — e.g., "Tier 1 only")
  - valid_from (datetime)
  - valid_until (datetime)
  - revoked (boolean, default false)
  - revoked_at (datetime, nullable)
  - performance_metrics (JSONB — tracked accuracy, override rate, etc.)

PersonRegistry (shared across protocols)
  - person_id (string, auto-generated)
  - canonical_id (string — cédula or cédula jurídica)
  - canonical_id_type (enum: CEDULA_FISICA, CEDULA_JURIDICA)
  - name (string)
  - contact_email (string, nullable)
  - contact_phone (string, nullable)
  - contact_whatsapp (string, nullable)
  - roles_held (JSONB — array of {protocol, case_id, role})

PropertyRegistry (shared across protocols)
  - property_id (string, auto-generated)
  - folio_real (string, nullable)
  - plano_catastrado (string, nullable)
  - location_province (string)
  - location_canton (string)
  - location_district (string)
  - location_sector (string, nullable)
  - location_address (text)
  - area_m2 (numeric, nullable)
  - history (JSONB — array of {protocol, case_id, outcome, date})
```

**Approximate length:** 4-6 pages including field descriptions and constraints

---

### 2.5 Gate Checker Specification (docs/gate_checker_spec.md)

**Purpose:** The most critical specification. Defines exactly how constitutional enforcement works. Tests are written from this spec before implementation.

**Must contain:**

**Interface:**
```python
class GateCheckResult:
    passed: bool
    blocked_gates: list[BlockedGate]  # Empty if passed
    receipt: CommitmentReceipt | None  # Generated if passed

class BlockedGate:
    gate_type: str  # "authority", "evidence", "reasoning", "dependency", "recourse"
    reason: str     # Human-readable explanation
    details: dict   # Specific missing items

def check_gates(
    protocol: Protocol,
    commitment_point_id: str,
    actor: Actor,
    outcome_key: str,
    reasoning: str | None,
    relied_on_evidence: list[str],  # evidence_ids
    additional_inputs: dict,  # conditions, acta_reference, etc.
    case_state: CaseState,
    delegation_registry: DelegationRegistry,
) -> GateCheckResult:
```

**Gate evaluation logic (pseudocode for each gate):**

```
AUTHORITY GATE:
  1. Get commitment point's required_role from protocol
  2. Check if actor holds that role
  3. If not, check delegation_registry for valid DELEGATE:
     - Matches commitment_point_id
     - Actor matches delegated_to_actor
     - Current time within valid_from/valid_until
     - Not revoked
     - Scope conditions satisfied (e.g., case is Tier 1)
  4. If quorum required, check additional_inputs.members_present >= quorum
  5. PASS or BLOCK with specific reason

EVIDENCE GATE:
  1. Get commitment point's evidence requirements from protocol
  2. For each required evidence type:
     a. Check if an EvidenceRecord of that type exists for this case
     b. Check attestation level meets minimum
     c. Check validity window (valid_until >= now)
     d. Check status is ACTIVE (not SUPERSEDED, CONTESTED, or EXPIRED)
  3. For conditional requirements, evaluate condition against case state
  4. PASS or BLOCK with specific missing items

REASONING GATE:
  1. Check if commitment point requires reasoning
  2. If yes, check reasoning parameter is non-empty
  3. If structured reasoning required, validate structure
  4. PASS or BLOCK

DEPENDENCY GATE:
  1. Get all DEPENDS_ON relationships for this commitment point from topology
  2. For each dependency:
     a. Check if a receipt exists for the depended-on commitment point
     b. If dependency has a condition, check the receipt's outcome matches
  3. PASS or BLOCK with specific unsatisfied dependencies

RECOURSE GATE:
  1. Check if the selected outcome is marked adverse in the protocol
  2. If adverse, check that recourse architecture is defined for this outcome
  3. If no recourse defined for an adverse outcome, BLOCK
     (this is a protocol design error that should be caught by proof contracts,
      but the runtime enforces it as a safety net)
  4. PASS

VERSION BINDING:
  1. Get ACTIVE protocol version
  2. Bind the commitment to this version
  3. Always PASS (informational, not blocking)
```

**Receipt generation logic:**
```
If all gates PASS:
  Generate CommitmentReceipt with:
  - All fields populated from inputs + protocol + case state
  - automation_level derived from actor type + delegation presence
  - provenance_links pointing to relied_on evidence and upstream receipts
  - recourse_architecture copied from protocol if outcome is adverse
  
  Write receipt via receipt_writer (append-only)
  
  Trigger downstream effects:
  - Create obligations per protocol spec
  - Open recourse windows if adverse
  - Emit cross-protocol events
  - Queue artefact generation
```

**Test cases to write FIRST (before implementation):**

```
test_authority_gate_passes_with_correct_role
test_authority_gate_blocks_wrong_role
test_authority_gate_passes_with_valid_delegation
test_authority_gate_blocks_expired_delegation
test_authority_gate_blocks_revoked_delegation
test_authority_gate_blocks_delegation_scope_mismatch
test_authority_gate_checks_quorum
test_authority_gate_blocks_insufficient_quorum

test_evidence_gate_passes_with_all_evidence
test_evidence_gate_blocks_missing_evidence
test_evidence_gate_blocks_expired_evidence
test_evidence_gate_blocks_insufficient_attestation_level
test_evidence_gate_handles_conditional_requirements
test_evidence_gate_accepts_substitution

test_reasoning_gate_passes_when_provided
test_reasoning_gate_blocks_when_missing_and_required
test_reasoning_gate_passes_when_not_required

test_dependency_gate_passes_when_deps_satisfied
test_dependency_gate_blocks_when_dep_missing
test_dependency_gate_checks_conditional_deps

test_recourse_gate_passes_non_adverse_outcome
test_recourse_gate_passes_adverse_with_recourse_defined
test_recourse_gate_blocks_adverse_without_recourse

test_receipt_generation_includes_all_fields
test_receipt_generation_records_delegation_provenance
test_receipt_generation_records_automation_level
test_receipt_is_append_only

test_full_commit_happy_path
test_full_commit_blocks_and_returns_all_reasons
```

**Approximate length:** 6-8 pages

---

### 2.6 Claude Agent Specification (docs/agent_spec.md)

**Purpose:** How Claude is integrated. Context assembly, tool definitions, interaction patterns.

**Must contain:**

**Context assembly:**
- How the six layers are assembled into a system prompt
- Maximum context budget and how to manage it
- What gets loaded per interaction vs. per case vs. per session

**Tool definitions (what Claude can call):**

```
get_case_state(case_id) → CaseState
  Returns current position, evidence inventory, gate status, obligations

store_evidence(case_id, evidence_type_id, attestation_level, 
               document_uri?, extracted_metadata?) → EvidenceRecord
  Stores new evidence in the case

attempt_commitment(case_id, commitment_point_id, outcome_key,
                   reasoning?, relied_on_evidence?, 
                   additional_inputs?) → GateCheckResult
  Attempts a commitment through the gate checker.
  Returns PASS with receipt or BLOCK with reasons.

get_person(canonical_id) → PersonRecord | null
  Lookup in shared person registry

register_person(canonical_id, name, contact?) → PersonRecord
  Register new person in shared registry

get_property(folio_real?, plano_catastrado?) → PropertyRecord | null
  Lookup in shared property registry

register_property(folio_real?, plano_catastrado?, location, area?) → PropertyRecord
  Register property in shared registry

send_notification(recipient, channel, template_id, data) → DeliveryResult
  Send a notification via the channel router

generate_artefact(case_id, artefact_id, data) → ArtefactResult
  Generate a document from template

get_protocol_context(commitment_point_id) → CommitmentPointDetail
  Get full constitutional signature and agent instructions
  for a specific commitment point

search_cases(filters) → list[CaseSummary]
  Search existing cases (for anomaly detection, history lookup)
```

**Interaction patterns:**
- Applicant intake conversation (guided by protocol's agent_instructions)
- Administrator review interaction (present case, guide through attestations)
- Status query handling (read case state, present in natural language)
- Notification dispatch (compose message following artefact templates)
- Anomaly flagging (match patterns to exception taxonomy)

**Error handling:**
- What Claude does when a gate check fails (explain to appropriate actor)
- What Claude does when it doesn't have enough context (ask, don't assume)
- What Claude does when the protocol doesn't cover a situation (flag as UNCLASSIFIED exception)

**Approximate length:** 5-7 pages

---

### 2.7 Database Schema Documentation (db/README.md + schema.sql)

**Purpose:** The complete database schema with explanations.

**Source:** Derived from data models spec (2.4), translated to SQL.

**Must include:**
- Table definitions with all constraints
- Indexes for common queries
- The append-only constraint on the receipts table (no UPDATE, no DELETE)
- Migration strategy

**Approximate length:** 3-4 pages + SQL

---

### 2.8 Deployment Configuration Schema (deployments/README.md)

**Purpose:** Documents the structure of deployment YAML files so Claude Code can build the deployment loader and validate configs.

**Must contain:**
- Every section of the deployment config with field definitions
- Required vs. optional fields
- Valid values for enums (channel types, integration types, etc.)
- Example: the Nosara deployment config

**Approximate length:** 3-4 pages

---

### 2.9 Protocol Schema (protocols/_base/acct_schema.yaml)

**Purpose:** A formal schema definition for ACCT protocol YAML files. Used by the protocol loader to validate that a protocol is well-formed, and by the proof contract checker to verify constitutional completeness.

**Must contain:**
- Required sections (commitment_points, topology, evidence_types, exceptions, roles)
- Required fields per commitment point (type, constitutional_signature, outcomes)
- Required fields per evidence type (purpose, source_class, attestation_level)
- Valid values for all enums
- Structural constraints (every DEPENDS_ON must reference an existing commitment point, etc.)

**Approximate length:** 3-4 pages (YAML schema)

---

### 2.10 Channel Integration Specs (docs/channels/)

**Purpose:** Spec for each channel adapter.

**WhatsApp spec must contain:**
- API integration approach (WhatsApp Business API via cloud provider, or manual bridge for MVP)
- Message types: text, image receive, PDF receive, document send
- Webhook format for incoming messages
- Rate limits and error handling
- How conversations map to cases (phone number → person → active case)

**Web interface spec must contain:**
- Admin dashboard routes and views
- Authentication approach
- What Claude generates vs. what's static HTML
- Responsive requirements

**Email spec must contain:**
- SMTP configuration
- Template format for outgoing notifications
- Inbound email handling (if any)

**Approximate length:** 2-3 pages per channel

---

### 2.11 Artefact Template Specs (deployments/nosara/templates/README.md)

**Purpose:** Spec for each document template.

**Carta de disponibilidad spec must contain:**
- Exact document structure (sections, fields, boilerplate text)
- Variable fields and their data sources
- Formatting requirements (fonts, margins, logo placement)
- Bilingual requirements
- Signature block layout

**Source:** The artefact section of the ACCT protocol YAML + the AyA carta samples analyzed earlier in the session.

**Approximate length:** 2-3 pages per template

---

## 3. BUILD PHASES

### Phase 0: Documentation (Before any code)
**Duration:** 3-5 days  
**Output:** All documents in Section 2 written and in the repository

Write every document listed above. Place them in the repository structure. Write CLAUDE.md. This is the foundation — Claude Code reads these to build everything that follows.

Key decision: start by writing the gate checker test cases (2.5). These are the most important specification in the system. If the tests are right, the gate checker will be right.

### Phase 1: Core Engine (The Constitutional Layer)
**Duration:** 1-2 weeks  
**Dependencies:** All documentation from Phase 0

Build order:
1. `models.py` — Data models from spec 2.4
2. `schema.sql` + migrations — Database from spec 2.7
3. `protocol_loader.py` — Parse and validate protocol YAML against schema
4. `deployment_loader.py` — Parse and validate deployment config
5. `evidence_manager.py` — Evidence storage and type checking
6. `state_manager.py` — Case lifecycle management
7. `receipt_writer.py` — Append-only receipt generation
8. `obligation_tracker.py` — Deadline and obligation tracking
9. **`gate_checker.py`** — Constitutional enforcement (tests first!)
10. `validate_protocol.py` + `run_proof_contracts.py` — Protocol validation scripts

**Test at end of phase:** 
- Load the carta de agua protocol YAML
- Load the Nosara deployment config
- Create a case programmatically
- Walk the case through every commitment point via direct API calls
- Verify every gate check passes/blocks correctly
- Verify receipts are generated correctly
- Verify proof contracts pass for the carta de agua protocol

### Phase 2: Claude Integration (The Agent Layer)
**Duration:** 1-2 weeks  
**Dependencies:** Phase 1 complete

Build order:
1. `context_builder.py` — Assemble Claude's system prompt from protocol + deployment + case state
2. `tool_definitions.py` — Define all tools Claude can use (wrapping Phase 1 components)
3. `agent_router.py` — Route interactions to Claude with appropriate context
4. `prompt_templates/` — System prompt layers

**Test at end of phase:**
- Claude can read the carta de agua protocol and explain it
- Claude can guide a simulated applicant through intake
- Claude can collect evidence and store it correctly
- Claude can attempt a delegated commitment and get PASS/BLOCK from gate checker
- Claude can prepare an admin review summary
- Claude can generate a Board package draft

### Phase 3: Channel Integration (The Interface Layer)
**Duration:** 1-2 weeks  
**Dependencies:** Phase 2 complete

Build order:
1. `api/app.py` — HTTP application
2. `channels/web.py` — Web interface (admin dashboard + applicant web chat)
3. `channels/whatsapp.py` — WhatsApp integration (start with webhook receiver)
4. `channels/email_channel.py` — Email notifications
5. `api/routes_webhook.py` — WhatsApp webhooks
6. `api/routes_admin.py` — Admin dashboard endpoints
7. `api/routes_internal.py` — Claude's tool API

**Test at end of phase:**
- A message sent to WhatsApp reaches Claude and gets a response
- Admin can open a web dashboard and see pending cases
- Email notifications are sent at appropriate triggers

### Phase 4: Artefact Generation (The Output Layer)
**Duration:** 1 week  
**Dependencies:** Phase 3 complete

Build order:
1. `artefacts/renderer.py` — DOCX template filling + PDF conversion
2. `artefacts/delivery.py` — Delivery pipeline (channel selection, confirmation)
3. Create actual templates: carta, denial letter, Board package
4. `integrations/google_drive.py` — Archival
5. `integrations/google_sheets.py` — Tracking sheet sync

**Test at end of phase:**
- A complete approved case generates a carta PDF
- The carta matches the expected format from the AyA samples
- Board packages are generated and printable
- Files are archived in Google Drive
- Tracking sheet updates automatically

### Phase 5: End-to-End Testing & Refinement
**Duration:** 1-2 weeks  
**Dependencies:** All phases complete

Activities:
1. Run 10+ simulated cases end-to-end (various project types, property types, outcomes)
2. Test edge cases: incomplete applications that expire, denied applications with appeals, renewals, moratorium toggle
3. Administrator walkthrough: actual administrator tests the system
4. Refine agent instructions based on testing
5. Refine templates based on administrator and Board feedback
6. Load testing: simulate peak volume (10 concurrent applications)

### Phase 6: Protocol Viewer/Editor
**Duration:** 1-2 weeks (can overlap with Phase 5)  
**Dependencies:** Protocol YAML is stable

Build the React-based protocol viewer per the UX specification:
1. Topology view (generated layout from protocol)
2. Commitment detail panel (constitutional signature inspector)
3. Cross-cutting views (evidence catalog, exception catalog, proof contracts)
4. Basic editing mode (contextual property edits)

---

## 4. DOCUMENTS INDEX (What Exists vs. What Needs to Be Written)

### Already Exists (from this session)

| Document | Location | Status |
|----------|----------|--------|
| ACCT Framework | ACCT_Product_Framework_v2.md (uploaded) | Complete — needs condensing for acct_primer.md |
| ICAD Architecture | ICAD_architecture_master_reference.md | Complete — needs trimming for docs/architecture.md |
| CDA Protocol (ACCT) | CDA_protocol_ACCT_v01.yaml | Draft — needs agent_instructions, collection blocks, projection blocks |
| Viewer/Editor UX Spec | ACCT_viewer_editor_UX_spec.md | Complete |
| ASADA Context | asada_context_carta_de_agua.md | Complete |
| Admin Interview Insights | administrator_interview_insights.md | Complete |
| Regulatory Requirements | carta_de_agua_requirements_reference.md | Complete |

### Needs to Be Written

| Document | Purpose | Priority | Approx. Effort |
|----------|---------|----------|-----------------|
| CLAUDE.md | Repository orientation for Claude Code | Critical — write first | 1-2 hours |
| docs/acct_primer.md | Condensed ACCT reference | Critical | 2-3 hours |
| docs/architecture.md | Implementation-focused architecture | Critical | 2-3 hours |
| docs/data_models.md | All data structures | Critical | 3-4 hours |
| docs/gate_checker_spec.md | Gate checker specification + test cases | Critical — most important | 4-6 hours |
| docs/agent_spec.md | Claude integration specification | Critical | 3-4 hours |
| docs/decisions.md | Architecture Decision Records | Important | Ongoing |
| db/schema.sql | Database schema | Critical | 2-3 hours |
| protocols/_base/acct_schema.yaml | Protocol validation schema | Important | 3-4 hours |
| deployments/nosara/config.yaml | Nosara deployment config | Critical | 2-3 hours |
| docs/channels/whatsapp_spec.md | WhatsApp integration spec | Important | 2-3 hours |
| docs/channels/web_spec.md | Web interface spec | Important | 2-3 hours |
| Protocol update: agent_instructions | Add to all evidence types and commitment points | Critical | 4-6 hours |
| Protocol update: collection blocks | Add to all evidence types | Critical | 3-4 hours |
| Protocol update: projection blocks | Add to all commitment points | Important | 3-4 hours |
| Protocol update: production blocks | Add to all artefacts | Important | 2-3 hours |
| deployments/nosara/templates/ | Actual DOCX templates | Important | 4-6 hours |

### Estimated Total Documentation Effort

~50-70 hours of documentation before coding begins. This sounds like a lot but it's the investment that makes the coding phase fast and accurate. Claude Code with good documentation can build in days what would take weeks without it.

---

## 5. CRITICAL PATH

The minimum viable sequence to get to a working system:

```
Week 1:     CLAUDE.md + architecture.md + acct_primer.md + data_models.md
            + gate_checker_spec.md (with test cases)
            + agent_spec.md
            + Nosara deployment config
            + Protocol updates (agent_instructions, collection blocks)

Week 2-3:   Phase 1 (Core Engine) — Claude Code builds from specs
            Gate checker tests pass.
            Protocol loads and validates.
            Cases flow through state machine.

Week 3-4:   Phase 2 (Claude Integration)
            Claude reads protocol and navigates cases.
            Tools work. Context assembly works.

Week 4-5:   Phase 3 (Channels)
            WhatsApp connected. Admin web interface works.
            Real messages flow through the system.

Week 5-6:   Phase 4 (Artefacts)
            Cartas generate. Board packages print.
            Google Drive and Sheets integrate.

Week 6-8:   Phase 5 (Testing & Refinement)
            Real cases with real administrator.
            Edge cases and exceptions.
            Agent instruction refinement.

Week 8+:    Phase 6 (Viewer/Editor) + first governed change
```

**8 weeks from documentation start to a working system processing real carta de agua applications at ASADA Nosara, simultaneously proving ICAD as a platform.**
