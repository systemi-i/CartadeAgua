# ICAD — Institutional Constitutional Agentic Design

## What This Is

ICAD is a platform that runs ACCT protocols — formal definitions of institutional commitment processes — with Claude as the primary execution agent and a coded constitutional enforcement layer (the gate checker) ensuring legitimacy.

The first deployment is the **carta de agua** (water availability letter) process at **ASADA Playas de Nosara**, a community water utility in Costa Rica.

This is simultaneously an MVP for the ASADA (automating their most complex public-facing process) and an MVP for the ICAD platform (proving the architecture works).

## The Three Artifacts

The system is built from three artifacts that must stay separated:

### 1. Protocol Definition (`protocols/`)
YAML files that define the constitutional structure of an institutional process. Contains: commitment points with constitutional signatures, evidence type system, exception taxonomy, recourse architecture, commitment topology, artefact specifications, and agent instructions for Claude.

**The protocol is the source of truth for the process.** The engine code must NEVER contain domain logic. It reads domain logic from the protocol.

### 2. Deployment Configuration (`deployments/`)
YAML files that define institution-specific infrastructure. Contains: available channels (WhatsApp, email, web), integration details (billing system, Google Drive, Sheets), document templates, role assignments, local rules.

**The deployment config is the source of truth for infrastructure.** The engine code must NEVER hardcode channel details, endpoints, or template paths.

### 3. Execution Engine (`engine/`)
Python code that reads both artifacts and runs the system. Contains: Claude integration, gate checker, state management, evidence storage, channel routing, artefact generation.

**The engine is protocol-agnostic and institution-agnostic.** If you removed all protocol YAML and deployment YAML, the engine should still compile and pass its own unit tests (using test fixtures).

## Architecture Summary

```
Protocol YAML ──→ Claude (reads as context) ──→ Navigation
                         │                      (conversations, evidence
                         │                       collection, analysis,
                         │                       artefact drafting)
                         │
                         ▼
                   Gate Checker (code) ──→ Commitments
                         │                (binding institutional
                         │                 actions with receipts)
                         │
                         ▼
Deployment YAML ──→ Infrastructure
                   (channels, storage,
                    integrations)
```

**Claude handles ~80% of the work** — everything between commitment points (navigation). This includes: guiding applicants, collecting documents, validating evidence, preparing analysis, drafting artefacts, sending notifications.

**The gate checker handles 100% of constitutional enforcement.** When any actor (Claude, administrator, Board) attempts a binding commitment, it passes through the gate checker. The gate checker is deterministic code — no AI, no LLM calls. It reads the commitment point's constitutional signature from the protocol, checks authority + evidence + reasoning + dependencies + recourse, and returns PASS (with receipt) or BLOCK (with specific reasons).

**Humans retain authority** at commitment points that require their judgment — Board decisions, President's signature, override authorization, appeals.

## Hard Invariants (Do Not Violate)

1. **The gate checker is deterministic Python.** No AI calls. No LLM reasoning. No external API calls. It reads protocol structure + case state and returns PASS or BLOCK. This is the constitutional firewall.

2. **Receipts are append-only.** The receipts table has no UPDATE and no DELETE operations. A receipt, once written, is permanent. Corrections are new commitments (REMEDY, SUPERSEDES) that reference the original.

3. **Protocol YAML is the single source of truth for process logic.** The engine does not contain if/else branches for specific protocols, evidence types, or commitment points. It reads these from the protocol.

4. **Deployment YAML is the single source of truth for infrastructure.** No hardcoded WhatsApp numbers, Drive folder IDs, email addresses, or template paths in the engine code.

5. **Claude cannot make commitments without delegation.** Claude's tool for attempting commitments always goes through the gate checker. The gate checker always verifies authority. Without a valid DELEGATE in the delegation registry, Claude's commit attempts are blocked.

6. **Every commitment produces a receipt.** No exceptions. The receipt includes: who committed, under what authority, relying on what evidence, at what attestation levels, under which protocol version, with what reasoning, producing what outcome.

## Repository Structure

```
icad/
├── CLAUDE.md                    ← You are here
├── README.md
├── docs/
│   ├── architecture.md          — Full architecture reference
│   ├── acct_primer.md           — ACCT framework summary
│   ├── data_models.md           — All data structures
│   ├── gate_checker_spec.md     — Gate checker specification
│   ├── agent_spec.md            — Claude integration spec
│   └── decisions.md             — Architecture Decision Records
├── protocols/
│   ├── carta_de_agua/
│   │   └── protocol.yaml        — The ACCT protocol definition
│   └── _base/
│       └── acct_schema.yaml     — Protocol validation schema
├── deployments/
│   └── nosara/
│       ├── config.yaml          — Nosara deployment config
│       └── templates/           — Document templates (DOCX)
├── engine/
│   ├── core/                    — ACCT primitives (protocol-agnostic)
│   │   ├── models.py            — Data models
│   │   ├── protocol_loader.py   — Parse/validate protocol YAML
│   │   ├── deployment_loader.py — Parse deployment config
│   │   ├── gate_checker.py      — Constitutional enforcement
│   │   ├── state_manager.py     — Case lifecycle
│   │   ├── receipt_writer.py    — Append-only receipts
│   │   ├── evidence_manager.py  — Evidence storage + type checking
│   │   └── obligation_tracker.py
│   ├── agent/                   — Claude integration
│   │   ├── context_builder.py   — System prompt assembly
│   │   ├── tool_definitions.py  — Tools Claude can call
│   │   └── agent_router.py      — Interaction routing
│   ├── channels/                — Channel adapters
│   │   ├── whatsapp.py
│   │   ├── email_channel.py
│   │   └── web.py
│   ├── integrations/            — External system adapters
│   │   ├── google_drive.py
│   │   ├── google_sheets.py
│   │   └── manual_billing.py
│   ├── artefacts/               — Document generation
│   │   ├── renderer.py
│   │   └── delivery.py
│   └── api/                     — HTTP layer
│       └── app.py
├── db/
│   ├── schema.sql
│   └── migrations/
├── tests/
│   ├── core/
│   │   ├── test_gate_checker.py — WRITE THESE FIRST
│   │   └── ...
│   └── fixtures/
└── scripts/
```

## Key Technical Decisions

- **Python 3.12+**
- **PostgreSQL** for the state store (not SQLite — we need proper constraints and concurrent access)
- **Flask** or **FastAPI** for the HTTP layer (decide based on async needs)
- **Anthropic Python SDK** for Claude API calls
- **python-docx + WeasyPrint** for document generation (DOCX templates → PDF)
- **Google API client libraries** for Drive and Sheets integration
- **Alembic** for database migrations

## How to Run

```bash
# Setup
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Database
createdb icad
alembic upgrade head

# Tests
pytest tests/

# Development server
python -m engine.api.app
```

## Key Context Documents

When working on specific components, read the relevant specification:

| Working on... | Read first... |
|---------------|---------------|
| Any component | This file (CLAUDE.md) |
| Data models, database | docs/data_models.md |
| Gate checker | docs/gate_checker_spec.md |
| Claude integration | docs/agent_spec.md |
| Understanding ACCT | docs/acct_primer.md |
| Overall architecture | docs/architecture.md |
| The carta de agua process | protocols/carta_de_agua/protocol.yaml |
| Nosara-specific details | deployments/nosara/config.yaml |

## What to Build First

Phase 1 (current): Simple web interface where you can chat with Claude about the carta de agua process. Claude reads the protocol YAML as context. No database yet, no gate checker yet. Goal: validate that the conversational protocol-driven approach works.

Phase 2: Add persistence (database + state manager) and the gate checker. Conversations create real case records. Commitments are constitutionally gated.

Phase 3: Connect real channels (WhatsApp, email) and generate real artefacts (carta PDFs, Board packages).
