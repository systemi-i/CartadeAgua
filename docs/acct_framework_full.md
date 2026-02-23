**ACCT**

Agentic Constitutional Commitment Typology

*The Product Framework v2*

A first-principles, governance-first model for institutional operations

February 2026

0\. The Paradigm Shift

BPMN and every workflow orchestrator descended from it model the same
thing: the flow of tasks. The fundamental unit is a task, the
fundamental structure is a sequence, and everything else --- authority,
evidence, exceptions, recourse, versioning --- is either metadata or a
bolt-on.

ACCT inverts this. The fundamental unit is a Commitment: the moment an
institution binds itself to an outcome under authority, with evidence,
producing a receipt and creating recourse. The fundamental structure is
a Commitment Topology: the constitutional relationships between
commitments. The path between commitments is flexible; the
constitutional constraints at each commitment point are rigid.

**BPMN says:** *here is the sequence; follow it.*

**ACCT says:** *here are the commitments and their constitutional
requirements; navigate toward them however makes sense.*

This inversion resolves five structural failures of the BPMN paradigm:

  --------------- ---------------------------- ----------------------------
  **Dimension**   **BPMN**                     **ACCT**

  Atomic unit     Task                         Commitment

  Structure       Sequential flow              Commitment topology

  What's rigid    The sequence                 Constitutional constraints

  Exceptions      Error events (deviation =    Exception space (governed
                  failure)                     alternative)

  Authority       Swimlane annotation (no      Authority gate (enforced at
                  enforcement)                 commitment)

  Evidence        Data objects (untyped)       Evidence type system

  Change          Redeploy diagram             Governed release

  Recourse        None (separate process)      Structural (linked to
                                               commitment)

  Time            Current version only         Version-bound

  AI              AI as task performer         AI as constitutional agent
                                               within bounded authority

  Audit           Activity log                 Receipt graph with
                                               provenance traversal
  --------------- ---------------------------- ----------------------------

**ACCT is the model. ICAD is the runtime and platform.** ACCT defines
what commitments exist and what constitutional constraints govern them.
ICAD designs, executes, and evolves ACCT protocols. The model can be
adopted as a standard beyond the product.

1\. Commitment Types

Every institutional action compiles to one of eight commitment types.
This is the type system of institutional authority.

  -------------- ------------------- ----------------------- ---------------------
  **Type**       **What it does**    **Constitutional        **What it produces**
                                     requirements**          

  **DECIDE**     Bind the            Authority + evidence +  Receipt with
                 institution to a    reasoning               relied-on set.
                 determination                               Recourse if adverse.

  **OVERRIDE**   Deviate from        All of DECIDE +         Receipt + ex-post
                 default path under  exception type +        review obligation.
                 governed exception  justification +         
                                     compensating control    

  **APPEAL**     Contest a prior     Standing + grounds +    Response obligation
                 commitment          linkage to original     (time-bound).
                                                             Independent review.

  **REMEDY**     Correct or          Appeal disposition +    Linked to original.
                 compensate for      authority + remedy type Closes recourse loop.
                 deficient                                   
                 commitment                                  

  **EVOLVE**     Change the rules    Change authority +      Effectivity boundary.
                 (meta-commitment)   dossier + diff + tests  Rollback semantics.
                                                             Continuity.

  **CLOSE**      Terminate case with All obligations         Final receipt
                 final receipt       discharged. All         confirming
                                     recourse respected.     completeness.

  **ATTEST**     Submit or certify   Attestation level +     Challenge path.
                 evidence            provenance + validity   Visibility ceiling.

  **DELEGATE**   Transfer or share   Scope + duration +      Logged. Bounded.
                 authority           accountability chain    Revocable.
  -------------- ------------------- ----------------------- ---------------------

1.1 The commitment/navigation distinction

Not everything an operator does is a commitment. Much of institutional
work is navigation: collecting information, communicating with
applicants, consulting colleagues, preparing analysis. ACCT does not
model navigation as commitments. Navigation is the flexible path between
commitment points.

This distinction is critical for the automation dial. Navigation can be
freely automated, AI-assisted, or manual without changing the
constitutional structure. Commitments always require their
constitutional signatures to be satisfied, regardless of who or what
performs them.

**Product implication:** the operator's UX is not a task list of
everything they must do. It is a view of the next commitment point they
can reach, what's required to reach it, and what's currently missing.
Navigation is the operator's judgment call; the system scaffolds it but
doesn't prescribe it.

2\. Constitutional Requirements

Each commitment type has a constitutional signature: the set of
conditions that must be satisfied for the commitment to be legitimate.
This is the type system of institutional governance.

2.1 The DECIDE signature (canonical example)

  ---------------- ------------------------------------- ----------------
  **Gate**         **What it checks**                    **Strictness**

  Authority        The committing actor has the required Hard
                   role, delegation, and scope for this  
                   commitment point under the active     
                   protocol version.                     

  Evidence         All required evidence types are       Hard (per type)
                   present, with sufficient attestation  
                   level, within validity windows, and   
                   not contested without resolution.     

  Reasoning        Minimum rationale: outcome key +      Soft (minimum)
                   structured or free-text justification 
                   within a structured slot.             

  Version binding  Commitment is bound to the ACTIVE     Hard (system)
                   protocol version at time of           
                   commitment.                           

  Recourse         If adverse outcome, recourse path is  Hard (if
                   defined or explicitly designated      adverse)
                   non-appealable with basis.            

  Receipt          System generates receipt with full    Hard (system)
                   relied-on set. Non-overridable.       
  ---------------- ------------------------------------- ----------------

**Product implication:** the commit action in the UI is gated by this
signature. The operator sees "you can commit" (all gates green) or "you
cannot commit because" (specific gates red with human-readable reasons).
This is constitutional enforcement rendered as UX.

2.2 The compiler metaphor

A protocol is source code. Constitutional requirements are the type
system. The runtime is the compiler and interpreter. A case is a program
execution. A receipt is a proof certificate. An audit is type-checking
the execution trace.

Signatures are defined at the protocol level, not hardcoded. Protocol
designers specify which evidence types, roles, and reasoning levels
apply at each commitment point. The runtime compiles these into
enforceable gates. The thin waist (12 canonical primitives) provides the
objects. The protocol provides the constraints.

3\. Commitment Topology

A protocol in ACCT is not a flowchart. It is a commitment topology: a
directed graph of commitment points and the constitutional relationships
between them.

3.1 Relationship types

  ------------------------ ------------------------------ ------------------------
  **Relationship**         **Meaning**                    **Example**

  **DEPENDS_ON**           B cannot be reached until A is Permit decision depends
                           satisfied.                     on completeness
                                                          determination.

  **CREATES_RECOURSE**     Adverse outcome at A generates Denial creates appeal
                           recourse path to B.            right.

  **CREATES_OBLIGATION**   A generates a future           Override creates ex-post
                           obligation at B.               review.

  **SUPERSEDES**           B replaces the effect of A.    Appeal remedy reverses
                                                          original denial.

  **FORKS**                A creates a parallel           Referral creates a new
                           constitutional space linked to linked case.
                           the original.                  

  **GOVERNED_BY**          Meta-relationship linking      All permit DECIDEs
                           operational commitments to the governed by the
                           EVOLVE that can change them.   protocol's EVOLVE.
  ------------------------ ------------------------------ ------------------------

3.2 What the designer authors

1.  **Commitment points:** each has a type (from the eight), a name, and
    its constitutional signature.

2.  **Relationships:** the topology. DEPENDS_ON defines sequencing.
    CREATES_RECOURSE defines contestation. CREATES_OBLIGATION defines
    accountability chains.

3.  **Default path:** an optional suggested sequence for simple cases. A
    default, not a mandate.

4.  **Exception space:** at each commitment point, the governed
    deviations with their modified and compensating requirements.

5.  **Closure conditions:** what must be true for CLOSE to be valid.

3.3 Path flexibility

The topology defines what commitments exist and how they relate. It does
not prescribe the order of navigation (beyond DEPENDS_ON constraints):

-   **Simple institutions:** follow the default path. The UI guides step
    by step. Feels like a traditional workflow.

-   **Complex institutions:** navigate the topology based on case
    specifics. The UI shows available commitment points, requirements,
    and current status.

-   **Agentic systems:** agents compose paths dynamically. Every
    commitment must satisfy its constitutional signature. The
    constitution constrains; the agent navigates.

In all three modes, the constitutional requirements are invariant. The
flexibility is in navigation, not in governance.

4\. The Evidence Type System

Evidence in ACCT is not data. It is constitutionally typed. The evidence
type system catches institutional failures the way a programming
language's type system catches bugs: before they reach production.

4.1 Evidence type definition

  ---------------- ---------------------------------- --------------------
  **Property**     **What it defines**                **Example**

  Purpose          What this evidence proves.         Proof of structural
                                                      soundness

  Source class     Who/what can attest: self,         Licensed structural
                   official, third-party, machine.    engineer

  Attestation      Reliance level: Asserted,          Verified (signed
  level            Observed, Verified, Anchored.      report)

  Validity         Expiry, refresh requirements,      Valid 12 months
                   jurisdictional scope.              

  Substitution     Alternative evidence that          Municipal inspection
                   satisfies the same requirement.    may substitute

  Contestation     How the evidence can be            Counter-inspection
                   challenged.                        

  Visibility       Who can see this evidence.         Internal (redacted
                                                      in public export)
  ---------------- ---------------------------------- --------------------

4.2 AI outputs as evidence

AI-generated analysis is evidence with specific type constraints:

-   **Source class:** always "machine." Never official or third-party.

-   **Attestation level:** "Asserted" by default. "Observed" if it
    processed verified inputs. Never "Verified" without external
    validation.

-   **Mandatory contestation:** must always be challengeable. Any
    high-stakes adverse commitment relying solely on machine-attested
    evidence is a constitutional violation.

-   **Provenance:** model version, input references, processing method
    stored in the evidence record.

**The type-checking analogy:** when a commitment point requires "proof
of eligibility at Verified level," an AI assessment at Asserted level
fails the type check. The runtime blocks the commitment. This is not
policy --- it's a type error.

5\. The Receipt Schema

Every commitment produces a receipt. The receipt is a structured
constitutional record proving the commitment was legitimate at the time
it was made.

  ---------------------- ----------------------------------------------------
  **Field**              **Content**

  commitmentType         DECIDE \| OVERRIDE \| APPEAL \| REMEDY \| EVOLVE \|
                         CLOSE \| ATTEST \| DELEGATE

  commitmentPointId      Which commitment point in the topology was
                         exercised.

  protocolVersionId      Which protocol version governed this commitment.

  caseId                 Which case this commitment belongs to.

  authority              Who committed: actor, role, delegation chain, scope.

  reliedOnSet            Evidence references used, with attestation levels.

  reasoning              Outcome key + rationale.

  outcome                What the institution bound itself to.

  recourseArchitecture   If adverse: standing, grounds, response obligation,
                         remedy types.

  provenanceLinks        References to prior commitments, evidence,
                         artefacts, external refs.

  occurredAt /           Timestamps preserving deterministic ordering.
  recordedAt             

  visibilityMarking      PUBLIC \| INTERNAL \| RESTRICTED.

  artefactsGenerated     Notices, permits, letters produced.

  automationLevel        MANUAL \| AI_ASSISTED \| AI_OVERSIGHT \| AUTOMATED.
                         Records who/what made this commitment.
  ---------------------- ----------------------------------------------------

Receipts are append-only. They cannot be edited, only superseded by
subsequent commitments. The receipt chain is the institutional memory.
Audit is graph traversal: from any receipt, traverse to evidence,
authority, version, prior and subsequent commitments, and generated
artefacts. "What happened and why?" is a query, not an investigation.

6\. Per-Commitment-Point Activation

This is one of ACCT's most consequential design decisions: commitment
points go live one by one. Within a single end-to-end process, different
commitment points can be at different stages of activation and different
levels of automation. Trust is earned per commitment point, not per
protocol.

6.1 Two modes, not three

The platform has two modes:

**DRAFT** --- design, validate, rehearse. The protocol is being authored
and tested. Operators can rehearse commitments. Nothing binds.
Everything is preparation.

**LIVE** --- commitments are binding. Receipts are authoritative.
Constitutional requirements are enforced.

There is no observation mode. The institution does not watch itself
before acting. It designs a constitutional structure, validates it, and
starts operating. The first weeks of operation produce the reality data
that earlier approaches tried to capture through observation --- but as
a byproduct of real institutional action, not as a separate preparatory
phase.

6.2 Granular activation

An institution does not "go LIVE" as a binary. Commitment points are
activated individually:

-   **Week 1--2:** Protocol authored and validated. Proof contracts
    pass. Operators rehearse in DRAFT.

-   **Week 2--3:** First commitment point goes LIVE. Typically the
    highest-stakes decision gate --- the one where the most
    institutional authority is exercised and the most scrutiny falls.

-   **Week 3--6:** Additional commitment points activate as the team
    builds confidence. Exception data drives the first governed change.

-   **Week 6+:** Full topology is LIVE. The team has shipped at least
    one governed change based on real data. The protocol is a living,
    evolving constitutional structure.

Commitment points that are still in DRAFT while others are LIVE simply
don't produce binding receipts. The case flows through the LIVE
commitment points (with full constitutional enforcement) and through the
DRAFT points (as rehearsal or passthrough). This means the institution
gets value from day one of the first LIVE commitment point, without
needing the entire topology to be ready.

6.3 The automation dial is per commitment point

Within a single end-to-end service, different commitment points operate
at different automation levels:

  ------------------- ---------------- ------------------ -------------------
  **Commitment        **Automation**   **Agent**          **Why this level**
  point**                                                 

  Completeness        Automated        AI agent under     Low stakes. High
  determination                        DELEGATE           volume. Agent has
                                                          earned trust
                                                          through
                                                          demonstrated
                                                          accuracy.

  Technical review    AI-assisted      AI drafts; human   Medium stakes. AI
                                       commits            reduces work from
                                                          hours to minutes.
                                                          Human validates.

  Final approval      Manual           Human authority    High stakes.
                                                          Politically
                                                          sensitive. Full
                                                          constitutional
                                                          ceremony.

  Override            Manual           Human (always)     Overrides require
                                                          justification only
                                                          human judgment can
                                                          provide.

  Appeal review       AI-assisted      AI summarises;     AI identifies
                                       human decides      precedents.
                                                          Independent human
                                                          reviewer commits.
  ------------------- ---------------- ------------------ -------------------

**The critical invariant:** the constitutional signature at a commitment
point does not change based on automation level. A DECIDE requires the
same authority, evidence, reasoning, version binding, and recourse
whether a human or AI makes it. What changes is who/what satisfies the
requirements --- and that is specified through a DELEGATE commitment.

6.4 Trust is earned through receipts

The automation dial turns based on evidence, not aspiration. Because
every commitment --- regardless of automation level --- produces a
receipt with full provenance, the institution accumulates the data
needed to decide when to increase automation:

-   **Accuracy:** compare AI recommendations against human decisions at
    AI-assisted commitment points. What percentage of AI suggestions
    were accepted? Where did humans override?

-   **Appeal rates:** are decisions at automated commitment points
    contested more frequently than manual ones?

-   **Exception rates:** are automated commitment points generating more
    overrides?

-   **Outcome quality:** do cases that passed through automated
    commitment points have better or worse downstream outcomes?

When this data shows consistent, high-quality performance, the
institution can issue a DELEGATE for the next commitment point. That
DELEGATE is itself a constitutional commitment: it has authority
requirements (who can delegate), scope (which commitment point, which
case types), duration (time-bounded or performance-bounded), and
recourse (the delegation can be revoked, and any decisions made under it
can be contested).

**This is how agents earn trust:** not through benchmarks or demos, but
through months of receipted institutional performance at lower-stakes
commitment points, with the data to prove it.

6.5 What this means for the adoption journey

The per-commitment-point model eliminates the binary "go/no-go" adoption
decision that kills most institutional technology. An institution never
has to decide "are we ready to operate entirely under a new system?"
Instead:

-   They activate the commitment point where pain is highest and value
    is clearest.

-   They see results (receipts, consistency, audit packets) immediately.

-   They activate the next commitment point when ready.

-   They increase automation at each commitment point based on
    demonstrated performance.

This is adoption as a ratchet, not a leap. Each activated commitment
point creates institutional gravity --- receipts, data, patterns,
learned governance grammar --- that makes the next activation easier and
makes reverting harder.

7\. The Exception Bootstrap

Exceptions are where institutions actually operate. A protocol that
perfectly models the happy path but has no exception taxonomy is
useless. The question is: how do you define exception types before you
have operational data?

7.1 Launch with a minimal taxonomy

The protocol launches with a small set of exception types (3--5 named
types based on the designer's knowledge) plus one critical type:

**UNCLASSIFIED** --- an exception that doesn't fit any named type.
Requires justification. Creates a mandatory review obligation.

Every UNCLASSIFIED exception is data. The justification explains what
happened and why the existing taxonomy didn't cover it. The review
obligation ensures someone looks at it.

7.2 The exception-to-evolution loop

After 2--4 weeks of LIVE operation:

1.  UNCLASSIFIED exceptions accumulate with justifications.

2.  The protocol owner reviews them and identifies clusters.

3.  Clusters become proposed new exception types through the governed
    change process.

4.  A new protocol version ships with an expanded exception taxonomy.

5.  UNCLASSIFIED rate drops. Governance quality improves.

This loop is better than pre-operational observation for three reasons:

-   The exceptions are real (they occurred during binding commitments).

-   The justifications are real (operators had to explain why they
    needed the exception).

-   The governed change that results is real (a version was shipped, a
    diff exists, impact is measurable).

**The exception bootstrap is the institution's first experience of the
full ACCT loop:** operate, encounter reality, capture structured data,
evolve through governed change, measure impact. If this works in the
first month, the thesis is proven.

8\. The Protocol Design Experience

Protocol design in ACCT is not drawing a flowchart. It is structured
authoring guided by constitutional questions.

8.1 The constitutional questionnaire

The designer answers questions. The platform generates the protocol:

-   *"What decisions does this workflow make?"* → commitment points of
    type DECIDE.

-   *"Who can make each decision, and under what authority?"* →
    authority gates.

-   *"What must be proven before each decision?"* → evidence
    requirements.

-   *"What happens when something doesn't fit?"* → exception taxonomy
    (plus UNCLASSIFIED).

-   *"What can someone do if they disagree with a decision?"* → recourse
    architecture.

-   *"How do we change these rules?"* → EVOLVE commitment and change
    governance.

-   *"How do we know we're done?"* → closure conditions.

The output is a protocol definition: commitment points, topology,
evidence types, exception space, artefact templates, and default path.
The designer sees their workflow expressed back in terms they recognise,
structured constitutionally underneath.

8.2 Proof contracts (compilation)

Before activation, a protocol must pass proof contracts:

-   Every commitment point has its authority gate defined.

-   Every commitment point has satisfiable evidence requirements.

-   Every adverse outcome path has a recourse architecture (or explicit
    non-appealable designation with basis).

-   Every OVERRIDE path has compensating controls.

-   Closure conditions are reachable.

-   The EVOLVE commitment exists (the protocol must be changeable).

**This is the compiler.** A protocol that fails proof contracts cannot
be activated. Design errors are caught before they become institutional
failures.

9\. The Constitutional Runtime

The runtime takes a protocol definition and a case, and enforces
constitutional constraints at each commitment point.

9.1 What the runtime maintains

For any active case:

1.  **Current position:** which commitment points are satisfied,
    available, or blocked (and why).

2.  **Gate status:** for each available commitment point, which
    requirements are satisfied and which are not.

3.  **Evidence state:** which evidence records exist, their attestation
    levels, validity status.

4.  **Obligation tracker:** outstanding obligations from prior
    commitments.

5.  **Receipt chain:** the append-only sequence of receipts with
    provenance.

This state is deterministic: given the same protocol version and
receipts, the runtime produces the same state. This makes replay
possible.

9.2 The commit action

When an agent attempts a commitment, the runtime:

1.  Checks authority gate. Block with reason if unsatisfied.

2.  Checks evidence gate. Block with specific missing items if
    unsatisfied.

3.  Checks reasoning. Prompt if minimum rationale not provided.

4.  Checks procedural gates. Dependencies, recourse windows,
    obligations.

5.  Binds to protocol version. Records the ACTIVE version.

6.  Generates receipt. Full constitutional record with relied-on set and
    provenance.

7.  Generates artefacts. Notices, permits, letters from templates.

8.  Creates downstream effects. Recourse windows, obligations, state
    transitions.

9.  Appends to ledger. Immutable. Deterministic ordering.

9.3 What the runtime owns vs. what stays external

**Inside the runtime** (constitutionally required for commitment
legitimacy):

-   Evidence collection against typed requirements.

-   Routing to authority.

-   Queue and triage derived from commitment topology.

-   Exception invocation and governance.

-   Recourse initiation and tracking.

-   Receipt and artefact generation.

-   Governed change management.

**Outside the runtime** (not constitutionally required):

-   Intake portals and CRM. Scheduling and assignment. Email/SMS
    delivery. Document storage. Payments. Field operations.

**Boundary test:** is this capability constitutionally required for the
commitment to be legitimate? If yes, the runtime owns it. If no, it
stays external.

10\. The Projection Model

ACCT is a meta-product: the product generates different operational
surfaces depending on the protocol, case state, and user role. Screens
are projected from constitutional state, not designed per domain.

10.1 Five projections

  ---------------- ------------ ------------------------- ---------------------
  **Projection**   **User**     **Shows**                 **Answers**

  **Operate**      Operator     Next commitment points,   What do I need to do,
                                what's missing, what you  and what's blocking
                                can do. Derived inbox.    me?

  **Approve**      Authority    Commitments awaiting      Should I approve
                                authority. Evidence       this?
                                summary. Commit action.   

  **Explain**      Auditor      Receipt traversal.        What happened, why,
                                Provenance graph.         under what rules?
                                Deterministic replay.     

  **Evolve**       Owner        Hotspots, exception       What should we
                                rates, impact by version. change, and is it
                                Change authoring.         safe?

  **Recourse**     Affected     Contestation paths.       What can I do about
                   party        Response obligation       this decision?
                                status. Remedy tracking.  
  ---------------- ------------ ------------------------- ---------------------

10.2 Generated, not designed

Projections are rendered from protocol semantics + case state + user
role. The Operate projection reads the commitment topology, identifies
available commitment points, evaluates gate status, and renders "what's
next + what's missing." Different protocols produce different views
without custom UI work. This preserves generality and prevents bespoke
gravity.

10.3 The Operate projection in detail

Inbox

Derived from: all cases where this operator's role matches an available
commitment point's authority requirement. Each item shows: case
reference, current position, what commitment is needed, what's ready and
what's missing.

Case workspace

When the operator opens a case:

-   **Current position** (where we are).

-   **Next commitment point(s)** available (what we're heading toward).

-   **Gate status:** authority (✅ / ❌ route to approver), evidence
    (checklist with status per type), reasoning (ready / needed).

-   **Blocked reason** in plain language ("Waiting for structural
    inspection report --- required evidence, Verified level, currently
    absent").

-   **Exception button** (always visible): invoke a governed exception.

-   **Timeline** (one click away): receipt chain with provenance.

**The operator never sees a topology diagram.** They see "what I need to
do next" and "what's preventing me," rendered in domain language.

10.4 Progressive disclosure

-   **Level 1 (default):** next commitment + what's missing + action
    buttons. Sufficient for routine cases.

-   **Level 2:** full evidence checklist + gate details + exception
    options. For complex cases.

-   **Level 3:** receipt chain + provenance + version history. For audit
    or investigation.

11\. Integration Architecture

**ICAD owns constitutional state. External systems own everything
else.**

11.1 Four integration patterns

  -------------------- --------------------------- ----------------------------
  **Pattern**          **How it works**            **When to use**

  **Reference-only**   External refs and           Minimum viable. Legacy
                       correlation IDs. Commits    system handles everything
                       happen in ICAD.             except the commit moment.

  **Metadata           Lightweight import of case  Zero double-entry requires
  ingestion**          fields. Stored as asserted  ICAD to show case context.
                       facts.                      

  **Evidence linking** Evidence references         Evidence lives in a DMS,
                       external files via URIs,    GIS, or registry.
                       hashes, attestation levels. 

  **Event emission**   ICAD emits canonical events External systems react to
                       that external systems       commitments (notifications,
                       consume.                    registry updates, payments).
  -------------------- --------------------------- ----------------------------

11.2 Attestation levels

Every piece of information from external systems carries an attestation
level: Asserted (declared without verification), Observed (captured from
system event), Verified (validated against source/signature), Anchored
(hash-anchored for tamper evidence). ICAD never overclaims what it
knows. Provenance views disclose attestation for every element.

11.3 The zero double-entry contract

For any deployment: the operator can complete a case without re-entering
the same facts in both ICAD and the legacy system. This is a deployment
gate, not an aspiration. If a commitment point fails this test, the
integration approach must change before that commitment point goes LIVE.

12\. The AI Architecture

AI touches every layer of ACCT but always within constitutional
boundaries.

  --------------- ------------------------------- ------------------------
  **Layer**       **What AI does**                **Constitutional
                                                  constraint**

  Protocol design Drafts protocols from policy    All drafts require human
                  documents. Suggests evidence    review before
                  types.                          activation.

  Evidence        Summarises evidence. Flags      Output is
  analysis        gaps. Drafts analysis.          machine-attested
                                                  evidence. Cannot be sole
                                                  basis for high-stakes
                                                  adverse decisions.

  Commitment prep Drafts reasoning. Suggests      Drafts labelled. Human
                  outcomes. Prepares artefacts.   commits. Provenance in
                                                  receipt.

  Navigation      Suggests next steps. Identifies Suggestions only.
                  optimal path through topology.  Operator chooses.
                                                  Constraints unchanged.

  Explanation     Generates plain-language        Derived artefacts with
                  explanations of decisions and   provenance. The receipt
                  blockers.                       is authoritative.

  Evolution       Identifies hotspots. Drafts     All changes go through
                  dossiers. Generates tests.      EVOLVE commitment. AI
                                                  cannot change rules.
  --------------- ------------------------------- ------------------------

12.1 The AI invariant

**AI cannot make commitments unless explicitly delegated through a
DELEGATE commitment with bounded scope, duration, and recourse.**

This is a runtime constraint, not a policy. The constitutional runtime
rejects commit events from AI actors without a valid DELEGATE. Even
under delegation, the commitment produces a full receipt, recourse
applies, and the DELEGATE is in the provenance chain.

12.2 The trust-earning path

An agent earns delegation through demonstrated performance at
lower-stakes commitment points:

1.  Deploy at a commitment point as AI-assisted (AI drafts, human
    commits).

2.  Accumulate receipts showing AI recommendation quality (acceptance
    rate, override rate, appeal rate).

3.  When data shows consistent performance, issue DELEGATE for that
    commitment point.

4.  Monitor automated commitment quality through the same receipt-based
    metrics.

5.  Revoke DELEGATE if performance degrades.

This is the responsible automation path: evidence-based, incremental,
reversible, and constitutionally governed. The same receipt system that
makes human decisions auditable makes AI delegation auditable.

13\. Governed Change

Changing the rules is itself a commitment --- the EVOLVE type. Protocol
changes receive the same constitutional treatment as the decisions the
protocol governs.

13.1 The change lifecycle

1.  **Hotspot identification:** data shows where the protocol is under
    stress (exception rates, evidence quality, cycle times, recourse
    clusters).

2.  **Draft change:** author or AI drafts a modification with change
    dossier.

3.  **Diff generation:** the system produces a structural diff.

4.  **Review and approval:** the change goes through the EVOLVE
    commitment's authority and evidence gates.

5.  **Activation:** the new version becomes ACTIVE with an effectivity
    boundary. Proof contracts re-checked.

6.  **Impact measurement:** outcomes under the new version compared to
    the prior version.

**This is the core loop of institutional learning:** identify a problem,
propose a change, test it, ship it, measure impact, iterate. This is
what institutions currently cannot do safely. ACCT makes it routine.

13.2 Continuity guarantees

When a new version activates:

-   New cases use the new version.

-   Existing cases continue under their bound version.

-   Past receipts remain valid and replayable against the version that
    governed them.

-   History does not change.

This is what makes change safe: the institution can evolve without
retroactively altering its past. Past decisions are defensible under the
rules that governed them, even as rules improve.

14\. The Adoption Journey

The adoption journey is commitment-oriented, not observation-oriented.
There is no preparatory phase. There are two phases: design the
constitutional structure, then start operating.

14.1 Phase 0: Protocol authoring and validation (1--2 weeks)

The protocol owner answers the constitutional questionnaire. The
platform generates a draft protocol. Operators rehearse representative
cases in DRAFT to validate that gates and evidence requirements match
reality. Adjustments are made. Proof contracts pass. The first
commitment point is selected for activation.

14.2 Phase 1: Incremental activation (week 2 onward)

The first commitment point goes LIVE. Real commitments produce real
receipts. The institution experiences:

-   Constitutional gates enforcing consistency.

-   Receipts proving what happened and why.

-   Exceptions captured as structured data.

-   Evidence requirements surfacing what's actually needed.

Additional commitment points activate as the team builds confidence. The
automation dial turns per commitment point based on demonstrated
performance.

14.3 Phase 2: First governed change (weeks 3--6)

This is the PMF proof. Based on LIVE data, the protocol owner:

1.  Identifies a hotspot (high UNCLASSIFIED exception rate, evidence
    quality gap, cycle time issue).

2.  Drafts a protocol change (new exception types, adjusted evidence
    requirements, refined authority gates).

3.  Ships a governed release with diff, dossier, and approval.

4.  Measures impact (exception rate drops, cycle time improves,
    consistency increases).

**The institution just shipped a governed process improvement in days,
not months.** With a receipt. With a diff. With impact measurement.
Without breaking anything. That's the moment the thesis is proven.

14.4 PMF signals

Product-market fit for ICAD is not "people like it." It is:

-   **Recurring use:** operators make commitments through ICAD daily.

-   **One governed change shipped:** the institution evolved its
    protocol and measured impact.

-   **Audit packet trusted:** an outsider can reconstruct "what happened
    and why" from the export.

-   **Measurable outcome delta:** cycle time, consistency, exception
    rate, or audit cost improved.

If all four signals are present within 60 days of the first LIVE
commitment point, the product works.

15\. Persona Journeys

15.1 The Operator

**Projection:** Operate. **Daily rhythm:** inbox → case workspace →
review evidence → assess gates → commit or escalate → handle exceptions
→ issue artefacts.

**What ACCT gives them:** clarity (what's missing, what's blocking),
protection (receipts prove they followed the rules), speed (no hunting
across systems), governed exceptions (they don't invent workarounds).

**30-day test:** the operator says "that's an exception type," "we can't
commit without evidence," "what's blocking this?"

15.2 The Authority

**Projection:** Approve. **Rhythm:** review commitments awaiting
authority. Check evidence sufficiency. Approve, request more evidence,
or escalate. Review override obligations.

**What ACCT gives them:** decision-ready packets (evidence + analysis +
gate status), accountability protection (every approval receipted),
delegation management.

15.3 The Auditor

**Projection:** Explain. **Rhythm:** select cases. Traverse receipt
chains. Verify constitutional compliance. Export deterministic audit
packets. Flag anomalies.

**What ACCT gives them:** audit as query not reconstruction. Receipt
integrity verification. Version-aware replay. Exportable packets.

15.4 The Protocol Owner

**Projection:** Evolve. **Rhythm:** monitor hotspots. Identify
improvements. Author dossiers. Review diffs. Approve activations.
Measure impact.

**What ACCT gives them:** data-driven evolution. Safe change with
rollback. Before/after by version. Institutional learning as
infrastructure.

15.5 The Affected Party

**Projection:** Recourse. **Experience:** receive a decision artefact
with reasoning and recourse options. If adverse: see contestation paths,
grounds, deadlines. Initiate. Track response obligation. Receive remedy.

**What ACCT gives them:** legibility (explanations from receipts),
agency (structured contestation), accountability (response obligations
with time bounds), effect (remedies that change outcomes).

16\. What ACCT Makes Possible

16.1 For institutions

-   **Legitimate velocity:** move faster without collapsing due process.

-   **Safe change:** evolve continuously through governed releases.

-   **Institutional memory:** every commitment is structured data that
    compounds.

-   **Safe automation:** deploy AI within constitutional boundaries. The
    dial turns per commitment point without turning off accountability.

-   **Incremental adoption:** commitment points go live one by one. No
    binary go/no-go. Trust is earned through receipts.

16.2 For affected people

-   **Legibility:** decisions have explanations.

-   **Recourse:** contestation is a workflow with response obligations
    and remedies.

-   **Consistency:** same constitutional constraints, every case, every
    version.

16.3 For the field

-   **A shared language:** eight commitment types, constitutional
    signatures, commitment topology, evidence type system.

-   **Protocol packs:** reusable, forkable, certifiable templates
    carrying constitutional guarantees.

-   **A platform surface:** agents, analytics, and third-party tools
    build against ACCT's constitutional primitives.

16.4 The summary

*BPMN says: here is the sequence of tasks; follow it.*

*ACCT says: here are the commitments and their constitutional
requirements; navigate toward them, activate them one by one, automate
them as trust is earned, and evolve them through governed change. The
institution will be governable by construction.*

That is the first-principles, governance-first way of building
institutional operations.
