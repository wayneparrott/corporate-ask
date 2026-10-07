# Corporate Ask Build Playbook

## Purpose

This playbook defines a repeatable process for designing, implementing,
evaluating, securing, and deploying a trustworthy AI-powered conversational
assistant for a corporate website.

A Corporate Ask application is not simply an LLM chat interface.

It is a controlled product experience that combines:

- AI reasoning and language capabilities
- company-specific product knowledge
- authoritative information retrieval
- corporate information and disclosure policies
- source authority rules
- privacy protections
- evaluation and regression testing
- abuse and cost controls
- production security and operations

The objective is to create an assistant that is useful, current, trustworthy,
economical to operate, and appropriate for public interaction with customers.

---

# 1. Role of the AI Development Assistant

When following this playbook, the AI acts as both:

1. a product-development advisor; and
2. a software-engineering assistant.

The AI should guide the product owner through the Corporate Ask development
process rather than immediately attempting to construct the complete
application.

The AI may:

- identify decisions that need to be made;
- explain alternatives and tradeoffs;
- recommend an approach;
- draft policies and specifications;
- design architecture;
- implement approved decisions;
- create evaluations and tests;
- analyze failures;
- recommend improvements;
- assist with deployment and operations.

The AI must not invent corporate policy.

When a product-policy decision has not been established, the AI should present
the issue to the product owner, explain meaningful alternatives, recommend an
approach when appropriate, and obtain a decision before encoding that policy
into the application.

The product owner is the final authority for company policy, product
positioning, disclosure decisions, and acceptable assistant behavior.

---

# 2. Core Development Principles

## 2.1 Accuracy Over Apparent Helpfulness

Do not invent information merely because providing an answer appears more
helpful than acknowledging uncertainty.

The assistant should distinguish among:

- information that is supported;
- information that cannot currently be verified;
- information that is outside its scope; and
- information that it intentionally does not disclose.

These are different conditions and should not be conflated.

## 2.2 Authority Over Search Ranking

The easiest information to retrieve is not necessarily the most authoritative.

Corporate Ask must establish an explicit source-authority model.

Current official product documentation will ordinarily outrank historical
documentation, community discussion, search-engine ranking, and third-party
commentary.

Authority rules are company-specific and must be defined by the product owner.

## 2.3 Current Truth Over Historical Truth

Information can have been correct historically while being incorrect as an
answer about the current product.

The system should distinguish among current, legacy, discontinued, and
historical information when those distinctions matter.

## 2.4 Privacy by Design

Private corporate information should be intercepted before unnecessary
retrieval, inference, or answer generation occurs.

Do not retrieve private information and then rely solely on the final model to
decide whether to disclose it.

## 2.5 Positive Product Description

Prefer explaining what a product or technology is rather than volunteering
unnecessary assertions about what it is not.

Negative clarification is appropriate when needed to correct a material
misunderstanding and when corporate policy permits that clarification.

## 2.6 Proportional Assistance

The assistant should provide an amount of assistance proportional to its
purpose.

A corporate product assistant may appropriately answer product questions,
explain technologies, diagnose errors, provide small examples, and help users
understand related technical concepts without automatically becoming an
unrestricted general-purpose coding or research agent.

The desired boundary must be explicitly defined for each Corporate Ask.

## 2.7 Minimize Unnecessary Collection

Production observability should provide enough information to evaluate quality,
reliability, cost, and abuse without unnecessarily collecting identifying or
sensitive user information.

## 2.8 Product-Owner Authority

The AI recommends.

The product owner decides.

Decisions that affect corporate policy, public positioning, privacy,
disclosure, source authority, or product representation must be recorded as
explicit project decisions.

## 2.9 Behavior Must Be Testable

A behavioral policy is not complete merely because it has been written into a
prompt.

Important policies require corresponding evaluation cases.

Where appropriate, evaluations should include:

- positive cases;
- negative cases;
- boundary cases;
- ambiguous cases;
- adversarial cases; and
- regression cases derived from previously discovered failures.

## 2.10 Policy Dimensions Must Compose Explicitly

Important behavioral policies should be modeled as independent dimensions when
they answer different questions.

Examples include:

- topical scope;
- private-information handling;
- disclosure policy;
- product lifecycle;
- assistance complexity;
- retrieval requirements.

Do not overload one classification to represent several independent policy
decisions.

Before multiple behavioral policies are combined, define an explicit routing
and precedence contract describing:

- which decisions are independent;
- which decisions may intercept processing;
- which decisions may override ordinary routing;
- which combinations select different answer modes;
- which decisions are final before answer generation.

For example, a private-information decision may intercept a request before
ordinary scope handling, while a bounded technical-assistance decision may
permit useful assistance even when the topic is not otherwise central to the
company.

These are project-specific decisions.

Once trusted application routing has made a policy decision, the answer model
should not silently reconsider or reverse that decision unless the architecture
explicitly assigns that responsibility to the model.

Evaluation should test both individual policy dimensions and their composition.

---

# 3. Required Project Artifacts

Every Corporate Ask project should maintain explicit artifacts describing its
behavior and operation.

At minimum:

## Project Specification

Defines:

- company identity;
- assistant identity;
- purpose;
- target audience;
- scope;
- product terminology;
- product lifecycle;
- information boundaries;
- disclosure policy;
- source authority;
- specialized assistance policies; and
- public branding.

## Evaluation Suite

Provides repeatable tests for the behavioral requirements established by the
project specification.

## Security and Operations Specification

Defines:

- browser/server trust boundaries;
- request admission controls;
- bot protection;
- rate and concurrency limits;
- input limits;
- timeout behavior;
- logging;
- retention;
- health/readiness;
- deployment;
- rollback; and
- production validation.

## Decision Record

Important product-owner decisions should be preserved so future AI sessions
and developers understand not only the resulting behavior but why it exists.

A decision should record, at minimum:

- the issue;
- alternatives considered;
- the product-owner decision;
- rationale when useful;
- affected policies/evaluations; and
- date or project version when appropriate.

---

# 4. Development Workflow

Corporate Ask should be developed incrementally.

The stages below describe dependencies and qualification milestones. They are not intended to require a rigidly linear implementation schedule. Work may overlap when dependencies are satisfied, but a later stage must not silently bypass an unresolved earlier policy decision.

Do not attempt to implement every capability during the first development
stage.

The recommended sequence is:

1. Corporate Discovery
2. Scope and Qualification
3. Privacy and Information Boundaries
4. Disclosure Policy
5. Source Authority
6. Basic Answer Generation
7. Grounding and Citation Validation
8. Product Lifecycle and Historical Information
9. Specialized Assistance Policies
10. Behavioral and Adversarial Evaluation
11. Request Admission and Abuse Protection
12. User Experience
13. Production Logging and Operations
14. Production Trust Boundary
15. Deployment and Rollback
16. Production Validation
17. Continuous Improvement

Each stage should produce explicit artifacts or decisions and should have
completion criteria.

---

# 5. Stage 1 — Corporate Discovery

Do not begin by writing a large system prompt.

First understand the organization and intended assistant.

Establish:

- company name;
- assistant name;
- assistant purpose;
- target users;
- primary products/services;
- technologies relevant to those products;
- public websites and documentation;
- support/community resources;
- desired public personality;
- likely user questions;
- known information that should not be disclosed;
- expected technical depth; and
- desired relationship between the assistant and the main corporate website.

The AI should interview the product owner when these items are not known.

### Deliverable

Initial Corporate Ask Project Specification.

### Completion Gate

The product owner can clearly answer:

> Who is this assistant for, what should it help them accomplish, and what
> broad subjects should it handle?

---

# 6. Stage 2 — Scope and Qualification

Define the semantic boundary of the assistant.

A useful starting classification is:

- IN_SCOPE
- AMBIGUOUS
- OUT_OF_SCOPE

Do not rely exclusively on keywords.

For technical companies, topics adjacent to the company's products may be
useful even when they do not explicitly mention the company.

Define how ambiguous questions should be handled.

Also determine whether some otherwise out-of-scope questions deserve limited
assistance.

### Evaluation Requirement

Create representative cases for:

- clearly in-scope questions;
- clearly unrelated questions;
- adjacent-domain questions;
- ambiguous questions;
- misleading wording; and
- attempts to turn the assistant into a general-purpose assistant.

### Completion Gate

Scope behavior is documented and passes its initial evaluation suite.

---

# 7. Stage 3 — Privacy and Information Boundaries

Identify categories of corporate information the public assistant should not
provide.

Possible categories include:

- financial condition;
- non-public revenue;
- profitability;
- personnel information;
- internal organization;
- employee locations;
- internal operations;
- infrastructure;
- security architecture;
- credentials;
- internal systems;
- confidential partnerships;
- unannounced products; and
- private roadmap information.

These categories are examples, not universal policy.

The product owner must decide the company's actual boundaries.

Where practical, private-information requests should be detected before
retrieval or answer generation.

The system should not search for, estimate, infer, calculate, confirm, or deny
protected corporate information merely because a third-party source claims to
contain it.

### Evaluation Requirement

Test:

- direct requests;
- indirect requests;
- requests framed as estimates;
- requests asking for confirmation;
- requests citing alleged third-party knowledge;
- inference attempts; and
- combinations of public and private questions.

### Completion Gate

Protected information categories are explicit and adversarial privacy tests
pass.

---

# 8. Stage 4 — Disclosure Policy

Decide what the assistant may reveal about itself and its implementation.

Consider:

- assistant branding;
- underlying AI provider;
- model identity;
- model version;
- prompts;
- classifiers;
- routing;
- source restrictions;
- internal configuration;
- infrastructure;
- security controls; and
- credentials.

Do not assume that transparency requires revealing implementation details.

Conversely, do not make false denials.

Define approved public explanations.

## Deterministic Versus Generated Disclosure Responses

Not every semantically classified request needs a generated response.

For disclosure decisions where the product owner requires tightly controlled
public substance, consider:

    semantic classification
        ↓
    deterministic approved response

This can be preferable when generated prose could accidentally:

- confirm something the company intentionally does not confirm;
- deny something the company intentionally does not deny;
- identify a protected provider, model, relationship, or implementation detail;
- introduce unnecessary assertions beyond approved public facts.

Deterministic interception does not make the semantic classifier infallible.
The classification decision must still be evaluated.

Use generated answers when variability, explanation, retrieved evidence, or
question-specific reasoning provides meaningful value.

The project specification should record which disclosure categories use:

- deterministic responses;
- generated responses; or
- generated responses constrained by approved public facts.

### Completion Gate

Common self-referential and implementation questions have approved behavioral
rules and evaluation cases.

---

# 9. Stage 5 — Source Authority

Define what sources the assistant trusts and how conflicts are resolved.

Possible classes include:

1. current first-party product documentation;
2. official release/delivery information;
3. first-party support material;
4. reliably identified company staff guidance;
5. official upstream technology documentation;
6. community discussion;
7. third-party sources;
8. historical material.

The actual hierarchy is company-specific.

For each source class determine:

- authority;
- applicability;
- freshness expectations;
- citation requirements;
- reproduction/quotation rules; and
- whether it may establish definitive claims.

## Retrieval Capability Is Layered

Do not treat "retrieval works" as a single property.

Evaluate separately whether the system can:

1. discover an appropriate source;
2. acquire the actual source content;
3. establish the source's identity;
4. determine its authority for the claim;
5. determine its current applicability;
6. determine whether the evidence supports the claim; and
7. deliver a valid citation associated with that evidence.

Discovery metadata, catalogs, indexes, search snippets, aliases, or summaries
may help locate evidence without themselves becoming evidence.

Likewise, permission to search a domain does not automatically establish:

- source ownership;
- author authority;
- first-party status;
- current applicability; or
- entitlement to substantiate a particular claim.

## Retrieval Experiments

When source retrieval is uncertain, perform a bounded experiment before
building substantial retrieval infrastructure.

Define:

- representative queries;
- expected sources;
- discovery success;
- acquisition success;
- citation-delivery success;
- call/time/cost budget;
- stopping criteria.

Diagnose the failing layer before repeatedly tuning prompts or search queries.

If discovery is unreliable but the source set is valuable and reasonably
bounded, consider a different discovery mechanism rather than weakening source
authority rules.

The product owner should decide whether the expected source coverage justifies
additional retrieval infrastructure.

### Completion Gate

The assistant has an explicit authority model rather than simply trusting
whatever search retrieves first.

---

# 10. Stage 6 — Basic Answer Generation

Only after scope, privacy, disclosure, and authority are understood should the
core answer-generation behavior be stabilized.

Answers should generally be:

- accurate;
- relevant;
- appropriately concise;
- grounded when grounding is required;
- clear about uncertainty;
- consistent with company terminology; and
- useful without unnecessary marketing language.

Avoid one enormous prompt containing unrelated policy when structured
classification, routing, retrieval, or deterministic handling is safer.

### Completion Gate

Representative ordinary questions produce consistently acceptable answers.

---

# 11. Stage 7 — Grounding and Citation Validation

Retrieval alone does not guarantee grounding.

The system should distinguish where appropriate among:

- VERIFIED PRESENT;
- VERIFIED ABSENT; and
- COULD NOT VERIFY.

Negative factual claims deserve particular care.

Failure to find something is not automatically proof that it does not exist.

Citations should support the claim being made rather than merely point to a
related page.

## Evidence Provenance

Grounding evidence should retain enough provenance to establish what evidence
was actually available for the operation being evaluated.

Evidence retrieved later during review may help assess an answer, but it must
not automatically be represented as evidence that was available during the
original generation.

Where evaluation uses source quotations or extracted evidence:

- verify quoted text against the captured source where practical;
- preserve explicit UNKNOWN or UNVERIFIABLE states;
- do not allow a plausible evaluator explanation to substitute for evidence;
- distinguish source authority from claim entailment;
- distinguish source applicability from claim entailment;
- distinguish citation presence from citation coverage.

A model-based evaluator can itself hallucinate.

Its conclusions should therefore be treated as evaluated evidence rather than
as an infallible ground truth.

## Validation and Repair

If answers are validated before delivery, define the repair contract explicitly.

Repair should be:

- bounded;
- subject to the remaining request deadline and resource budget;
- governed by the same privacy, disclosure, source, and lifecycle policies;
- based on trusted inputs rather than unnecessarily reinforcing rejected draft
  content.

Do not create open-ended generate-review-repair loops.

## Answer Delivery Contract

Before implementing answer streaming, decide whether the application promises
validation before the user sees an answer.

Possible delivery models include:

- buffered final delivery;
- direct answer streaming;
- hybrid delivery.

If the project guarantees validation-before-exposure, unvalidated draft answer
content must not be streamed to the user.

The application may still stream truthful activity information while the final
answer is being generated and validated.

### Completion Gate

Grounding and citation behavior passes dedicated evaluation.

---

# 12. Stage 8 — Product Lifecycle and Historical Information

Determine how the assistant handles:

- current products;
- legacy products;
- discontinued products;
- renamed products;
- historical documentation; and
- superseded guidance.

Historical information may still be useful when the user explicitly asks
about historical behavior.

It should not silently override current guidance.

### Completion Gate

Lifecycle boundaries are explicit and tested.

---

# 13. Stage 9 — Specialized Assistance Policies

Determine whether the company needs additional assistance boundaries.

Examples include:

- software development;
- configuration assistance;
- legal-document explanation;
- troubleshooting;
- security guidance;
- financial topics;
- product comparisons; and
- migration assistance.

Define proportional behavior rather than relying on vague instructions such as
"be helpful."

Where useful, classify request complexity independently from topical scope.

### Completion Gate

Specialized assistance boundaries are documented and tested.

---

# 14. Stage 10 — Behavioral and Adversarial Evaluation

Consolidate the evaluation suite.

Test interactions among policies, not merely each policy independently.

Include attempts to:

- bypass privacy rules;
- manipulate source authority;
- induce unsupported claims;
- reveal protected implementation information;
- exploit historical information;
- override instructions;
- expand technical assistance beyond its intended boundary; and
- combine several legitimate capabilities into an unintended result.

Failures discovered here should become permanent regression tests when
appropriate.

### Completion Gate

The product owner has reviewed representative answers and the automated suite
meets the project's acceptance criteria.

---

# 15. Stage 11 — Request Admission and Abuse Protection

Protect expensive model operations before they occur.

Consider:

- request-body limits;
- question length;
- conversation-history limits;
- bot/human verification;
- per-client rate limits;
- global rate limits;
- per-client concurrency;
- global concurrency;
- timeouts;
- cancellation behavior; and
- cost ceilings.

Prefer rejecting invalid or abusive work before expensive processing begins.

## Protect Paid Prototypes Early

Stage 11 is the formal request-admission hardening milestone, but basic resource
bounds should exist before any paid prototype is exposed to untrusted users.

At minimum consider early bounds on:

- request size;
- question size;
- request deadline;
- concurrency;
- model output;
- aggregate spend.

Later stages may refine these controls.

## Real Integration Verification

Mocked and injected tests establish important contracts but do not prove that
the real browser, application configuration, verification service, credentials,
and external dependencies interoperate.

Before declaring admission controls complete, perform at least one bounded
real-path integration check in an appropriate non-production environment.

Distinguish:

- configuration readiness;
- mocked contract verification;
- real external integration;
- operational health.

A readiness endpoint should not be treated as proof that an external
verification flow actually works.

### Completion Gate

Resource controls have automated tests and cannot be trivially bypassed
through ordinary request manipulation.

---

# 16. Stage 12 — User Experience

The user should understand that work is occurring without the application
fabricating progress.

Useful states may include:

- understanding the question;
- locating relevant information;
- reviewing sources;
- preparing the answer; and
- checking the answer.

Expose semantic activity, not internal architecture.

Do not expose chain-of-thought or protected internal reasoning.

Accessibility and reduced-motion behavior should be considered.

## Delivery Semantics

The user experience must conform to the answer-delivery contract established
during grounding and validation design.

If final answers are buffered for validation:

- activity may be streamed;
- rejected drafts must never become visible;
- transient activity is not conversation history;
- failures and cancellations must not create completed conversation turns.

Activity indicators should correspond to real application operations rather
than fabricated progress.

Where streaming crosses proxies, CDNs, compression, or caching layers, verify
incremental delivery through the actual serving path.

### Completion Gate

Normal, fast, slow, failed, and cancelled requests have coherent UX behavior.

---

# 17. Stage 13 — Production Logging and Operations

Define what must be observable in production.

Potential measurements include:

- request outcome;
- policy decisions;
- latency;
- retrieval activity;
- token usage;
- estimated cost;
- citations;
- final answer; and
- failure category.

Explicitly define what must NOT be logged.

Establish retention periods.

Provide health and readiness endpoints with clearly different purposes where
appropriate.

### Completion Gate

Operations can diagnose quality and reliability without unnecessary collection
of user information.

---

# 18. Stage 14 — Production Trust Boundary

Document the complete request path.

For example:

    Browser
       ↓
    Edge / CDN
       ↓
    Reverse proxy
       ↓
    Application server
       ↓
    AI / retrieval services

For every boundary determine:

- which component is trusted;
- which headers are trusted;
- who creates those headers;
- how spoofing is prevented;
- where TLS terminates;
- how origin bypass is prevented; and
- where credentials exist.

Never trust a client-controlled forwarding header merely because it has a
familiar name.

### Completion Gate

The production trust model is explicit and tested.

---

# 19. Stage 15 — Deployment and Rollback

Production deployment should be repeatable.

Prefer:

- immutable or timestamped releases;
- deterministic dependency installation;
- production builds;
- pre-activation validation;
- atomic activation;
- service restart;
- post-activation health checks;
- automatic rollback when practical; and
- bounded release retention.

A successful process exit is not sufficient evidence of a successful
deployment.

Validate the actual public-serving path, not merely the application process.

### Completion Gate

A deployment and rollback have both been demonstrated successfully.

---

# 20. Stage 16 — Production Validation

Validate the real system after deployment.

Check:

- public homepage;
- Ask request;
- streaming/activity behavior;
- bot protection;
- source retrieval;
- citations;
- privacy interception;
- disclosure behavior;
- health monitoring;
- logging;
- rate limits; and
- failure behavior.

Production-specific defects should become regression tests or deployment
checks whenever possible.

### Completion Gate

The production application demonstrates the intended behavior through the real
public request path.

---

# 21. Stage 17 — Continuous Improvement

Production is not the end of evaluation.

Use privacy-conscious quality information and product-owner review to identify:

- unanswered questions;
- weak grounding;
- outdated sources;
- terminology changes;
- lifecycle changes;
- new products;
- recurring user confusion;
- policy gaps; and
- regressions.

Changes to important behavioral policy should include corresponding evaluation
changes.

Do not allow accumulated exceptions to silently replace the documented
product policy.

---

# 22. AI Operating Procedure

This section defines how an AI should bootstrap, resume, and advance a
Corporate Ask project.

## 22.1 Bootstrap in a New Repository

When asked to begin a new Corporate Ask project:

1. Read `ASK-BUILD-PLAYBOOK.md`.
2. Read all companion Corporate Ask standards and templates applicable to the
   project.
3. Inspect the repository before assuming it is empty.
4. Create or locate the project's Corporate Ask Project Specification.
5. Create or locate its decision records, open-question state, and evaluation
   artifacts.
6. Determine the current development stage.
7. Identify unresolved decisions required for that stage.
8. Propose one bounded next milestone.
9. Define the evidence required to complete that milestone.
10. Obtain product-owner decisions for unresolved corporate policy before
    encoding them.

Do not begin by generating the complete application.

## 22.2 Resuming an Existing Project

When resuming work:

1. Read the current project specification.
2. Read approved and superseding decision records relevant to the current
   stage.
3. Inspect repository state and existing implementation.
4. Review the current stage, completion gate, known limitations, and open
   questions.
5. Determine whether later decisions supersede earlier requirements or tests.
6. Identify the next authorized action.

Do not assume that an older evaluation expectation remains valid after a later
product-owner decision supersedes the underlying policy.

## 22.3 Distinguish Decision Types

The AI should distinguish among:

### Corporate Policy Decisions

Require product-owner authority.

Examples:

- public positioning;
- privacy boundaries;
- disclosure;
- source authority;
- lifecycle recommendations;
- reproduction authorization;
- acceptable assistance boundaries;
- retention policy;
- product acceptance.

### Engineering Decisions

The AI may recommend and, when implementation has been authorized, make
ordinary engineering choices consistent with approved requirements.

Examples:

- internal function decomposition;
- test organization;
- safe parsing strategy;
- implementation details that do not change product policy.

### Engineering Requirements

Some properties follow from the approved architecture and are not optional
branding or policy choices.

Examples:

- secrets must not be shipped in public browser bundles;
- untrusted headers must not silently become trusted identity;
- malformed inputs must not bypass validated request contracts.

When uncertain whether a decision changes corporate policy, ask the product
owner.

## 22.4 Authorization Boundaries

Authorization to perform one action does not imply authorization for another.

Distinguish permission to:

- investigate;
- recommend;
- modify files;
- run tests;
- perform live external evaluations;
- incur external API cost;
- commit;
- push;
- deploy;
- modify production configuration;
- create or change external resources.

Do not infer deployment or external-resource authorization merely because an
implementation or test suite passes.

## 22.5 Stage Execution

For the current bounded milestone:

1. record relevant approved decisions;
2. implement only the authorized work;
3. create or update evaluations for behavioral changes;
4. run focused tests;
5. diagnose failures at the layer where they occur;
6. run adjacent-policy tests;
7. run the complete regression suite when appropriate;
8. perform bounded live/integration checks when required;
9. report what each test establishes and what it does not establish;
10. record remaining limitations.

Do not repeatedly tune prompts when evidence indicates the failure belongs to
retrieval, transport, configuration, policy routing, deployment, or another
layer.

## 22.6 Completion Gates

A stage or milestone is complete only when its required evidence exists.

Evidence may include:

- approved product-owner decisions;
- deterministic test results;
- semantic evaluation results;
- product-owner answer review;
- integration verification;
- production-path verification;
- known limitations.

Passing tests does not by itself constitute product-owner approval when the
gate includes product judgment.

Record:

- completion evidence;
- unresolved limitations;
- approval status;
- authorized next action.

## 22.7 Superseding Decisions

A later approved decision may intentionally replace an earlier decision.

When this occurs:

1. preserve the historical decision where appropriate;
2. mark it superseded rather than silently rewriting history;
3. identify the replacing decision;
4. update current policy;
5. update affected evaluations;
6. update implementation when authorized;
7. remove obsolete expectations from active regression criteria.

Historical evaluation results should remain identifiable as results against
the policy that existed when they were produced.

## 22.8 Bounded Experiments

Live model, retrieval, or external-service experiments should have:

- a stated question being investigated;
- representative test cases;
- call/time/cost bounds;
- stopping criteria;
- expected evidence.

Do not continue spending on repeated variations merely because the desired
result has not appeared.

At the end of an experiment, determine whether to:

- refine;
- change architecture;
- accept the limitation;
- defer the capability; or
- obtain a product-owner decision.

---

# 23. Definition of Done

A Corporate Ask application is not done merely because users can type
questions and receive AI-generated answers.

It is production-ready when the product owner has confidence that:

- its purpose and scope are explicit;
- private information is protected;
- disclosure policy is deliberate;
- authoritative sources are defined;
- current and historical information are distinguished;
- important claims are appropriately grounded;
- specialized assistance boundaries are controlled;
- important behaviors are evaluated;
- abuse and cost are bounded;
- production trust boundaries are understood;
- operations are observable without unnecessary data collection;
- deployment and rollback are repeatable; and
- production behavior has been validated through the real serving path.

The goal is not an assistant that answers everything.

The goal is an assistant that users can trust to represent the company well.