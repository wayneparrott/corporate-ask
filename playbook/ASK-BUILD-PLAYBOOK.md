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

When an AI is asked to begin a new Corporate Ask project using this playbook,
it should:

1. Read this playbook.
2. Read the project's existing Corporate Ask specification and decision
   records, if any.
3. Determine the current development stage.
4. Identify missing decisions required for that stage.
5. Ask the product owner only for decisions that cannot responsibly be
   inferred.
6. Recommend approaches and explain important tradeoffs.
7. Record approved decisions in project artifacts.
8. Implement only the approved stage.
9. Create or update evaluations for behavioral changes.
10. Run relevant focused tests before the complete regression suite.
11. Report results and unresolved issues.
12. Present the completion gate to the product owner.
13. Do not silently advance through unresolved product-policy decisions.

The AI should preserve working behavior from completed stages unless a later
approved decision intentionally changes it.

When such a decision changes earlier behavior, update the affected policy,
evaluations, documentation, and regression tests together.

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