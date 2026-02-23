# ASADA Nosara — Context for Carta de Agua Agentic Platform

> Extracted and condensed from the full ASADA institutional assessment.
> Purpose: Provide grounding context for an AI agent that automates the "carta de disponibilidad de agua" process at ASADA Playas de Nosara, Costa Rica.

---

## 1. INSTITUTION IDENTITY

**Entity:** ASADA Playas de Nosara (also referred to as "Nimbu")
**Legal form:** Non-profit neighborhood association under Ley de Asociaciones Nº 218, with delegation from AyA to administer the communal aqueduct.
**Service area:** Playa Guiones and Playa Pelada, Nosara district, Nicoya Peninsula, Guanacaste, Costa Rica.
**Mandate:** Provide continuous, safe, regulated potable water service to users in its concession area, complying with AyA technical norms, Health Ministry quality standards, and ARESEP tariff rules.

---

## 2. DESIGN GUARDRAILS (Non-Negotiables for Any System)

1. **Human right & equity first** — No design can compromise minimum continuous access to safe water for existing households (especially vulnerable local users) to accommodate new tourism/real-estate demand.
2. **Ecological safety of the aquifer** — Extraction and expansion must stay within conservative, evidence-based safe yields; designs must avoid salinization and contamination of the coastal aquifer and respect protected areas.
3. **Full legal and regulatory compliance by default** — No workflow or automation may require or normalize practices violating AyA, MINAE/SENARA, Ministerio de Salud, ARESEP, municipal planning rules, or water-concession law. No "informal" wells, no capacity letters beyond demonstrated supply, no off-book developer deals.
4. **Community governance is primary; technology is assistive** — The Asamblea and Junta Directiva remain decision-making organs; digital tools must make their work clearer, faster, and more informed — never replace community deliberation or hide decisions inside opaque algorithms.
5. **Fairness, transparency, and explainability** — Any decision affecting who gets water, under what conditions, or at what tariff must be based on published criteria, be explainable in plain Spanish and English, and include a visible path for appeal.
6. **Financial sustainability without exclusion** — Tariffs must cover operations, maintenance, and renewal while protecting basic consumption for low-income households (including national social tariff rules).
7. **Institutional integrity & conflict-of-interest protection** — No feature may enable or obscure conflicts of interest; all high-stakes actions must produce tamper-evident logs auditable by the Fiscal, AyA, ARESEP, and the community.
8. **Resilience under failure and low-tech operation** — Core functions must continue under power cuts, connectivity loss, or staff turnover using simple fallbacks (paper, SMS/WhatsApp, local backups).

---

## 3. PHYSICAL & ENVIRONMENTAL SUBSTRATE

- **Water source:** Groundwater from a shallow coastal aquifer, accessed via multiple production wells inland from Guiones/Pelada.
- **Infrastructure:** Drilled wells → pumping stations → main storage tanks (elevated) → gravity-fed PVC distribution network → household meters.
- **Condition:** Serviceable but stressed; legacy segments with incomplete maintenance history, intermittent leaks, capacity limits forcing rationing in peak dry months (Feb–Apr).
- **Seasonality:** Rainy (May–Nov): higher recharge, occasional turbidity. Dry (Dec–Apr): minimal recharge + peak tourism demand; ASADA often rations.
- **Key risks:** Drought/climate variability, saltwater intrusion (coastal over-extraction), groundwater contamination from septic/runoff, rapid residential-tourism growth.
- **Growth pressure:** ~6,000 housing points (2024–25), growing ~8%/year. Housing could double by 2035, requiring roughly doubling current effective water capacity.

---

## 4. GOVERNANCE STRUCTURE

### Formal Organs
- **Asamblea General de Asociados** — Maximum authority. Approves budgets, elects/removes Board and Fiscal.
- **Junta Directiva** (Board of Directors) — 7 members: President, Vice-President, Secretary, Treasurer, 3 Vocales. Day-to-day administration, hiring, contracting, operational policies.
- **Órgano Fiscal (Fiscalía)** — Independent oversight (1–3 people). Reviews finances and legality; can convene assemblies or alert AyA.
- **Operational staff** — Administrator/Manager, fontanero/operator, billing/admin staff.
- **AyA** — External delegating/supervising authority with intervention powers.

### Real Governance (How It Actually Works)
- Real power concentrates in: President + 1–2 key board members + operator.
- AyA and Municipality serve as higher-level veto players.
- Large developers/hotels are influential outsiders who lobby via personal connections.
- Many critical decisions are pre-cooked in WhatsApp groups and informal pre-meetings before formal Junta sessions.

---

## 5. REGULATORY STACK (Rules That Bind the Carta de Agua Process)

### External (Cannot Be Changed)
- **Constitutional principles** — Right to health and healthy environment.
- **Ley de Asociaciones Nº 218** — Governs non-profit association structure.
- **Ley Constitutiva del AyA Nº 2726** — Authorizes delegation to ASADAs.
- **Reglamento de las ASADAS** (Decreto 42582-S-MINAE, 2020) — Defines organizational structure, functions, oversight, AyA powers.
- **Health Ministry regulations** — Potability norms, sampling, reporting.
- **ARESEP regulations** — Tariff methodology, regulatory accounting, service standards.
- **MINAE/SENARA** — Groundwater management, concessions, aquifer protection.
- **Municipal zoning** — Land-use, construction permits.
- **SETENA** — Environmental impact assessment.

### Internal
- **Estatutos/Bylaws of ASADA Playas de Nosara** — Membership, governance organs, meeting procedures, voting rules.
- **Internal service regulations** — Connection requirements, disconnection rules, payment terms.

### Hard Constraints
- Cannot operate outside AyA delegation framework.
- Cannot set/change tariffs unilaterally (ARESEP approval required).
- Must comply with drinking water quality norms and environmental restrictions.
- Must maintain Assembly, Junta, Fiscal structure with at least one ordinary Assembly/year.
- Cannot distribute profits; all surpluses reinvested.

---

## 6. CARTA DE AGUA PROCESS — CURRENT STATE (As-Is)

### What Is a Carta de Agua?
A **carta de disponibilidad de agua** (water availability letter) is a formal document issued by the ASADA confirming whether water capacity exists to serve a proposed development. Developers and property owners need this letter to obtain building permits from the Municipality or proceed with real-estate projects.

### Trigger
Developer or property owner requests the letter via email, in-person, or through a legal representative/broker.

### Actors & Roles
| Actor | Role |
|-------|------|
| **Developer/owner** | Submits request with project description |
| **Administrator** | Receives request, gathers project info, checks regulatory status |
| **President + Junta Directiva** | Reviews capacity and decides whether to issue letter |
| **AyA** | Provides technical guidelines on capacity/demand assessment |
| **Municipality** | Uses the letter when granting/denying construction permits |
| **Operator** | Provides input on current system stress |

### Current Process Flow (Sense → Decide → Act → Verify)

**SENSE**
1. Developer submits basic project description (lots/units, bedrooms, pools, use type).
2. Administrator checks whether ASADA is under "no factibilidad técnica" status.
3. Administrator requests a technical water demand study from developer if project is sizeable (per AyA guidance).
4. Informal sense: Operator provides input on current system stress.

**DECIDE**
1. President + Board discuss in meeting (or via informal pre-meetings).
2. Factors considered: current capacity vs existing commitments; political/social sensitivity.
3. Outcomes:
   - **Letter denied** — Especially under current no-factibilidad condition, or if developer hasn't delivered required study.
   - **Letter with conditions** — Limited units, requirement for tanks, conservation measures.
   - **Letter granted** — Historically more common before current stricter environment.

**ACT**
1. Administrator drafts letter referencing project name, location, ASADA's technical status, and conditions.
2. Letter signed by President (sometimes sealed) and delivered physically or by email.
3. Copy stored in paper file and/or digital folder; rarely in a structured database.

**VERIFY**
- **Little systematic verification** that built project matches what was requested (number of units, pools, etc.).
- No automated link between issued letters and later actual connections.

### Known Failures & Edge Cases
- Letters issued with ambiguous language ("subject to...") that Municipalities interpret as unconditional approval.
- Weak/missing linkage between letters and actual future connections.
- Municipalities approving permits without valid letters (e.g., Epic Nosara case).
- Developers pressuring ASADA via politicians or public campaigns.
- Projects split into smaller phases to avoid triggering stricter review.
- Old letters reused for expanded or changed projects.

### Time & Delays
- Simple/small requests: weeks to a couple of months.
- Large or controversial projects: months+, especially when AyA input is sought or public controversy arises.

---

## 7. CURRENT FACTIBILIDAD STATUS

ASADA Playas de Nosara is currently under a **"no factibilidad técnica"** (no technical feasibility) condition. This means:
- The ASADA has publicly determined it lacks sufficient demonstrated capacity to serve additional large developments.
- New cartas de agua for large projects are generally being denied or heavily conditioned.
- This status was publicly communicated via Facebook (Spanish/English) with detailed technical explanations.
- The Epic Nosara case demonstrated that the Municipality of Nicoya approved construction permits without valid water availability letters, leading to public controversy and investigation.

---

## 8. CAPACITY ALLOCATION CIVIC LOOP (Target Protocol)

### Sense
- Single intake registry for ALL requests (who, what, where, size, use type, date).
- System computes basic demand estimate (configurable template) for each project.
- Dashboard: current connections, pipeline of approved-but-not-yet-connected projects, active moratoria.

### Decide
- **Technical review team** (Operator + Administrator) prepares recommendation.
- **Board subcommittee** decides small connections; full Board + AyA consultation for major developments.
- Pre-documented capacity rules: safe yield, peak demand factor, reserve for households, existing moratoria, environmental constraints.
- Fairness principles: household-first, no approval beyond critical thresholds, alignment with no-factibilidad status.
- Decision outputs: Approve / Approve with conditions / Defer pending info / Deny (with reason referencing norms).

### Act
- For **new connections**: If approved → user pays fee → operator installs → billing account created. If denied → written explanation + recourse options.
- For **cartas de agua**: Letter generated from decision record including conditions, validity period, references to constraints. Copies archived and linked to request/project ID.

### Verify
- Periodic reconciliation: issued cartas vs actual built units & connections.
- Check total committed demand vs monitored production and peak stress.
- Check denied/conditional projects didn't slip in via other channels.

### Learn
- Analyze patterns of denials, conditions that work, capacity exceedances.
- Refine demand coefficients and reserve margins.

### Legitimize
- Publish capacity allocation policy and anonymized stats (requests, approvals, denials by category).
- Every decision has clear, shareable justification; appeals path is explicit.
- Use assemblies/forums to explain high-profile cases linked to aquifer protection.

---

## 9. KEY INFORMATION OBJECTS (Data Schemas)

### Request Record
- Applicant identity and contact
- Property location (cadastral/lot number, sector)
- Project description (lots/units, bedrooms, pools, use type, estimated demand)
- Request date and channel
- Status (received / documents pending / under review / decided)
- Linked decision record

### Technical Capacity Assessment
- Current system capacity (production, storage, peak limits)
- Existing committed demand (active connections + approved-not-connected)
- Regulatory status (factibilidad / no factibilidad / moratorium)
- Project demand estimate (using standard coefficients)
- Margin analysis (available capacity vs projected demand)
- Recommendation (approve / conditional / deny) with reasoning

### Board Decision Record
- Episode/request ID
- Decision type (approve / approve with conditions / defer / deny)
- Decision date
- Decided by (names/quorum status)
- Summary rationale (referencing specific metrics and norms)
- Conditions (if any)
- Linked documents

### Carta de Agua (Output Document)
- Reference number and date
- Applicant and project identification
- ASADA's current technical status
- Decision (availability confirmed / denied / conditional)
- Specific conditions and their basis
- Validity period
- Signatures (President, Secretary)
- Legal references

---

## 10. RECOURSE & APPEALS

- **Internal:** Request reconsideration by Junta Directiva; bring issue to Assembly.
- **External:** Appeal through AyA if denial perceived as arbitrary. Developers may also pressure Municipality and political actors.
- **Backdoor:** Political connections, lawyers, business association lobbying.
- The system must make the **formal appeal path clear and accessible** to reduce reliance on informal/backdoor recourse.

---

## 11. FAIRNESS & RED LINES

### Implicit Community Norms
- **Human consumption first** — Households before luxury uses (pools, tourism amenities).
- **"Tourism should pay more"** — High-end tourism/real-estate profits should carry larger financial burden.
- **No approvals that worsen scarcity** — Approving luxury projects while everyday users face rationing is seen as deeply unfair.

### Red Lines
- Open collusion with developers contradicting no-factibilidad status.
- Preferential treatment for connected developers.
- Issuing cartas without technical basis.
- Any process that effectively hides decisions from community scrutiny.

### Structural Risks
- Board members or associates who are developers/contractors/property managers (conflict of interest).
- Heavy dependency on one operator's tacit knowledge.
- Information asymmetry between inner circle and community.

---

## 12. CROSS-PROTOCOL DEPENDENCIES

The carta de agua process connects to other ASADA operations:

| Protocol | Dependency |
|----------|------------|
| **Water Production & Rationing (P1)** | Capacity assessments must reflect actual production capacity, peak stress, and historical rationing patterns |
| **Billing & Payments (P3)** | New connections from approved cartas become billing accounts |
| **Leak & NRW Control (P4)** | Non-revenue water reduces effective available capacity |
| **Water Quality (P5)** | Quality issues at specific sources may reduce usable capacity |

**Priority hierarchy when protocols conflict:**
1. Health/Potability (P5)
2. Basic human access & aquifer protection (P1)
3. Capacity allocation & growth (P2) ← Carta de Agua lives here
4. Financial sustainability (P3)
5. Efficiency/loss reduction (P4)

---

## 13. AI ROLE BOUNDARIES

For the carta de agua process, AI should operate as:

- **Advisory only** for capacity assessment and demand estimation — the Board decides.
- **Drafting assistant** for cartas, notices, and explanations — humans review and approve.
- **Registry/tracking system** — maintaining the single source of truth for all requests, decisions, and outcomes.
- **Compliance checker** — flagging when a request or decision appears to conflict with regulations or established rules.

**AI must NOT:**
- Autonomously approve or deny cartas.
- Override Board decisions.
- Hide reasoning or data from stakeholders.
- Make final determinations on capacity that bypass human judgment.
- Communicate decisions to applicants without human approval.

---

## 14. LANGUAGE & COMMUNICATION

- All outputs must be available in **Spanish and English** (bilingual community).
- Explanations must be **plain language** — no technical jargon without definition.
- Costa Rican regulatory terminology should use the official Spanish terms with English translations where needed.
- Key terms to preserve in Spanish: carta de disponibilidad de agua, factibilidad técnica, Junta Directiva, Asamblea General, Órgano Fiscal, fontanero, padrón.
