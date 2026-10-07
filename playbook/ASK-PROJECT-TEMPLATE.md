# Corporate Ask Project Specification Template

## Purpose

This document defines the company-specific product decisions for a Corporate
Ask application.

It is intended to be completed collaboratively by the product owner and the AI
development assistant while following `ASK-BUILD-PLAYBOOK.md`.

Do not treat unanswered sections as permission to infer corporate policy.

When information required by a development stage is missing, the AI should
identify the decision, explain meaningful alternatives, make a recommendation
when appropriate, and obtain product-owner direction.

This document should evolve with the product.

---

# 1. Project Identity

## Company

**Company name:**  
[TO BE DEFINED]

**Primary corporate website:**  
[TO BE DEFINED]

## Assistant

**Public assistant name:**  
[TO BE DEFINED]

Examples:

- Ask Acme
- Ask ExampleCorp

**Optional AI technology/brand name:**  
[TO BE DEFINED / NONE]

This may differ from the conversational experience itself.

For example:

    Ask ExampleCorp
        powered by
    ExampleGPT

Do not assume that an AI technology brand represents a proprietary foundation
model or any particular model architecture. Its public meaning must be defined
explicitly by the product owner.

## Public location

**Primary Ask URL:**  
[TO BE DEFINED]

**Relationship to corporate website:**  
[TO BE DEFINED]

Examples:

- integrated directly into corporate website;
- linked from corporate website;
- separate application on company-owned domain;
- embedded experience.

---

# 2. Mission

## Primary purpose

Complete:

> [Assistant name] exists to help _______________________________.

[TO BE DEFINED]

## Target users

Identify the primary audiences.

Examples:

- prospective customers;
- existing customers;
- developers;
- administrators;
- evaluators;
- partners;
- students;
- community users.

[TO BE DEFINED]

## Primary user outcomes

What should users be able to accomplish?

Examples:

- understand products;
- compare products;
- evaluate suitability;
- troubleshoot problems;
- understand licensing;
- find documentation;
- learn related technologies;
- discover support resources.

[TO BE DEFINED]

## Non-goals

What is the assistant intentionally not intended to become?

[TO BE DEFINED]

---

# 3. Product and Domain Knowledge

## Current products and services

For each important product:

| Product | Status | Description | Primary sources |
|---|---|---|---|
| | | | |

## Related technologies

Identify technologies users may reasonably ask about because they are related
to company products.

| Technology/domain | Relationship to company | Expected assistance |
|---|---|---|
| | | |

## Important terminology

Record preferred current terminology and terms that may require clarification.

| Term | Meaning / preferred usage |
|---|---|
| | |

## Approved Public Facts

Record important company facts that the product owner has explicitly approved
for use by the assistant.

These facts may be treated as application knowledge without requiring the
assistant to rediscover them through web search on every request.

| Fact ID | Approved public fact | Provenance | Limits / qualifications |
|---|---|---|---|
| | | | |

Approved application knowledge must not be expanded through inference.

A narrowly approved fact does not authorize disclosure of related protected
information.

For example, approval to state a company's ownership structure does not
automatically authorize disclosure of ownership percentages, valuations,
financial arrangements, or other related private information.

When an approved fact becomes outdated or is superseded, update its status and
the evaluations that depend on it.

## Renamed products

| Previous name | Current name | Effective period / notes |
|---|---|---|
| | | |

---

# 4. Scope Policy

Define the semantic scope of the assistant.

## IN_SCOPE

Questions that clearly belong within the assistant's mission.

[TO BE DEFINED]

## AMBIGUOUS

Questions that do not explicitly concern the company but have a plausible
relationship to its products, technologies, or customer workflows.

[TO BE DEFINED]

## OUT_OF_SCOPE

Questions unrelated to the assistant's mission.

[TO BE DEFINED]

## Policy Dimensions and Routing Precedence

Topical scope is only one policy dimension.

Identify other dimensions that may be evaluated independently, such as:

- private-information handling;
- disclosure;
- lifecycle;
- assistance complexity;
- retrieval requirements.

Do not use IN_SCOPE / AMBIGUOUS / OUT_OF_SCOPE as substitutes for these
independent decisions.

Define the project's routing and precedence rules.

| Condition / policy decision | Precedence | Resulting behavior |
|---|---:|---|
| | | |

Document important mixed cases.

Examples:

- private request that is otherwise in scope;
- out-of-scope question eligible for bounded technical assistance;
- current product question containing a historical reference;
- public question that also requests protected implementation details;
- substantial task that should be narrowed rather than refused.

When one policy intercepts another, record that explicitly.

The answer-generation model should not silently reconsider routing decisions
that the application has already made authoritative.

## Ambiguous-question behavior

How should ambiguous questions be handled?

[TO BE DEFINED]

## Out-of-scope behavior

How should unrelated questions be handled?

[TO BE DEFINED]

Avoid unnecessarily injecting company products into unrelated questions.

---

# 5. Private Corporate Information

This section defines information that the public assistant must protect.

Do not assume every example below applies to every company.

For each category choose:

- PUBLIC
- PROTECTED
- CONDITIONAL
- NOT APPLICABLE

## Financial information

**Policy:** [TO BE DEFINED]

Consider:

- revenue;
- profitability;
- financial condition;
- private-company valuation;
- internal forecasts;
- budgets;
- customer revenue;
- investment information.

## Personnel and organization

**Policy:** [TO BE DEFINED]

Consider:

- employee identities;
- employee locations;
- compensation;
- internal reporting relationships;
- staffing levels;
- hiring plans;
- personnel decisions.

## Internal operations

**Policy:** [TO BE DEFINED]

Consider:

- internal processes;
- internal systems;
- vendors;
- infrastructure;
- hosting;
- operational procedures.

## Security information

**Policy:** [TO BE DEFINED]

Consider:

- security architecture;
- credentials;
- internal network configuration;
- access controls;
- defensive controls;
- non-public vulnerabilities.

## Roadmap and future products

**Policy:** [TO BE DEFINED]

Distinguish where appropriate between:

- public roadmap information;
- announced products/features;
- reasonable discussion of future possibilities;
- confidential roadmap;
- unannounced products/features.

## Other protected categories

[TO BE DEFINED]

## Public Exceptions Within Protected Categories

A protected category may contain narrowly approved public facts.

Record these exceptions explicitly.

| Protected category | Approved public exception | Provenance | What remains protected |
|---|---|---|---|
| | | | |

An exception must be interpreted narrowly.

Approval to disclose one fact must not be treated as authorization to infer,
estimate, confirm, deny, or disclose adjacent protected facts.

---

# 6. Privacy Handling Rules

For protected company information determine whether the assistant may:

| Action | Allowed? | Notes |
|---|---|---|
| Search for it | | |
| Retrieve third-party claims | | |
| Estimate it | | |
| Infer it | | |
| Calculate it | | |
| Confirm it | | |
| Deny it | | |
| Summarize alleged information | | |

Define the preferred public response when a user asks for protected corporate
information.

[TO BE DEFINED]

---

# 7. Disclosure Policy

Define what the assistant may disclose about itself.

## Public assistant description

Approved conceptual description:

[TO BE DEFINED]

## AI technology brand

If applicable, define what the company's AI technology brand means.

[TO BE DEFINED / NOT APPLICABLE]

Prefer a positive definition of what the technology is.

Do not automatically volunteer assertions about implementation details or what
the technology is not.

## Disclosure Decision States

For implementation-related subjects, explicitly choose the company's public
position.

Possible decisions include:

- PUBLIC — may be stated directly;
- PROTECTED — should not be disclosed;
- CONDITIONAL — may be disclosed under defined circumstances;
- MAKE NO ASSERTION — the assistant should neither confirm nor deny the
  proposed characterization unless separately authorized.

"MAKE NO ASSERTION" is useful when the company does not want the assistant to
adopt either side of a user's proposed characterization.

Examples may include questions about:

- proprietary model development;
- model customization;
- fine-tuning;
- training;
- underlying architecture;
- provider relationships.

Do not convert MAKE NO ASSERTION into a factual denial.

## Disclosure Decision States and Disclosure Response Mode

For each important disclosure category, determine the response mechanism.

| Disclosure category | Decision state | Response mode | Approved public substance |
|---|---|---|---|
| | | | |

Possible response modes:

- DETERMINISTIC — return approved wording/substance without open-ended answer
  generation;
- GENERATED — allow ordinary answer generation under the approved policy;
- CONSTRAINED GENERATED — generate an answer using explicitly approved public
  facts and restrictions.

Use deterministic responses where generated variation creates unnecessary
risk of confirming, denying, or introducing protected assertions.

Semantic classification is still required and must be evaluated even when the
resulting response is deterministic.

## AI provider

**Policy:** [TO BE DEFINED]

## Model identity

**Policy:** [TO BE DEFINED]

## Model version

**Policy:** [TO BE DEFINED]

## Prompts and hidden instructions

**Policy:** [TO BE DEFINED]

## Classification and routing

**Policy:** [TO BE DEFINED]

## Source restrictions / allowlists

**Policy:** [TO BE DEFINED]

## Infrastructure and security controls

**Policy:** [TO BE DEFINED]

## Credentials and secrets

Credentials and secrets must never be disclosed.

## Approved implementation explanation

Record an approved high-level explanation for questions about how the
assistant works.

[TO BE DEFINED]

---

# 8. Source Authority Model

Corporate Ask must not equate search ranking with authority.

Define the company's authority hierarchy.

## Authority tiers

| Tier | Source class | Authority | Notes |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |

Possible source classes include:

- official product documentation;
- official release information;
- official corporate website;
- first-party knowledge base;
- first-party support discussions;
- identified employee guidance;
- upstream technology documentation;
- standards/specifications;
- community discussion;
- third-party publications;
- historical documentation.

## Approved Source Inventory

Do not treat an approved domain as sufficient evidence of source authority.

Maintain a source inventory appropriate to the project.

| Source ID | Source / boundary | Source class | Search eligible? | Ownership | Authority / applicability | Notes |
|---|---|---|---|---|---|---|
| | | | | | | |

A source boundary may be:

- an entire company-owned domain;
- a path within a domain;
- a documentation collection;
- a repository;
- a discussion collection;
- an upstream standards site;
- another explicitly identified resource.

For multi-tenant platforms, define the relevant organization, repository,
collection, path, or resource rather than approving the entire hosting domain.

Distinguish:

### Search eligibility

May the retrieval system search or discover this source?

### Source identity

Can the application establish that retrieved material belongs to the intended
source?

### Ownership

Does the company own the material?

Hosting material does not automatically establish ownership.

### Authority

What types of claims may this source authoritatively establish?

### Applicability

Does the evidence apply to the product, version, lifecycle state, time period,
or context in the user's question?

### Entailment

Does the actual evidence support the specific claim being made?

These properties must not be collapsed into a single "approved source" flag.

## Restricted sources

[TO BE DEFINED]

## Conflict resolution

When sources disagree, which source wins and why?

[TO BE DEFINED]

## Freshness

Which subjects require current verification?

[TO BE DEFINED]

## Citation expectations

When should answers contain citations?

[TO BE DEFINED]

## Retrieval Coverage Expectations

For important source classes define:

| Source class | Discovery method | Expected coverage | Fallback | Maintenance owner |
|---|---|---|---|---|
| | | | | |

Discovery may use:

- web search;
- provider search;
- curated catalogs;
- APIs;
- deterministic indexes;
- direct known URLs;
- other approved mechanisms.

Discovery metadata is not automatically answer evidence.

If a catalog, index, alias, or summary is used to locate a source, define how
the application obtains the actual evidence used to substantiate the answer.

Document known retrieval limitations rather than silently broadening source
authority to compensate for poor discovery.

---

# 9. First-Party Content Policy

Define how Corporate Ask may use company-owned public material.

## Summarization

[TO BE DEFINED]

## Quotation

[TO BE DEFINED]

## Reproduction

[TO BE DEFINED]

## Transformation

[TO BE DEFINED]

## Legal documents

Define special handling, if any, for:

- EULAs;
- licenses;
- terms of service;
- privacy policies;
- contracts;
- compliance material.

[TO BE DEFINED]

---

# 10. Product Lifecycle

Define lifecycle states appropriate for the company.

A useful starting model is:

- CURRENT
- LEGACY
- DISCONTINUED
- HISTORICAL

## Current products

[TO BE DEFINED]

## Legacy products

[TO BE DEFINED]

## Discontinued products

[TO BE DEFINED]

## Historical information policy

When may historical information be used?

[TO BE DEFINED]

## Recommendation policy

May the assistant recommend legacy or discontinued products?

[TO BE DEFINED]

---

# 11. Grounding Policy

Define which claims require authoritative evidence.

Consider:

- current product capabilities;
- compatibility;
- pricing;
- licensing;
- availability;
- release status;
- lifecycle;
- security characteristics;
- support status;
- negative claims.

## Verified present

How should the assistant handle a capability that authoritative evidence
confirms?

[TO BE DEFINED]

## Verified absent

What evidence is sufficient to assert that something is absent or unsupported?

[TO BE DEFINED]

## Could not verify

How should the assistant respond when evidence is insufficient?

[TO BE DEFINED]

Remember:

> Failure to find evidence is not automatically evidence of absence.

## Evidence Provenance

Define what evidence must be preserved or identifiable for grounding and
evaluation.

[TO BE DEFINED]

Distinguish:

- evidence available during answer generation;
- evidence retrieved later for evaluation or human review.

Later review evidence may help assess an answer, but must not automatically be
represented as evidence that the original answer-generation process possessed.

## Grounding Dimensions

Where relevant, evaluate separately:

- source identity;
- authority;
- ownership;
- applicability;
- lifecycle;
- entailment;
- citation association;
- citation coverage.

A valid citation association does not by itself prove that every claim in an
answer is supported.

---

# 12. Specialized Assistance

Determine whether the assistant should provide assistance beyond direct
company-product questions.

## Technical assistance

**Enabled:** [YES / NO]

If enabled, define the desired levels.

Possible model:

### NONE

No technical assistance is required.

### BOUNDED

Small examples, explanations, diagnostics, configuration help, or focused
technical assistance.

### SUBSTANTIAL

Requests requiring significant implementation or multiple components.

Define whether these should be narrowed, decomposed, redirected, or answered.

### GENERAL PROJECT

Requests effectively asking the assistant to become a general-purpose
development agent.

Define desired behavior.

## Other specialized domains

Examples:

- security;
- legal;
- financial;
- migration;
- deployment;
- data analysis.

[TO BE DEFINED]

---

# 13. Conversation Model

## Conversation history

How much history should the assistant retain within the browser/session?

[TO BE DEFINED]

## Conversation State Semantics

Define what constitutes a completed conversation turn.

[TO BE DEFINED]

Distinguish completed user/assistant turns from:

- transient activity;
- failed requests;
- cancelled requests;
- rejected drafts;
- incomplete streamed output.

Only state intentionally defined as conversation history should influence later
turns.

If conversation history is supplied by the browser, document what it can and
cannot enforce.

Browser-supplied history may support cumulative conversational intent, but it
must not be treated as trustworthy persistent state for enforcing cross-session
security, quota, or project limits.

## Persistent identity

Does the application have authenticated users?

[TO BE DEFINED]

## Server-side conversation storage

[TO BE DEFINED]

## Database

[TO BE DEFINED]

## Session duration

[TO BE DEFINED]

---

# 14. User Input

## Text questions

**Maximum question length:**  
[TO BE DEFINED]

## Conversation-history limits

[TO BE DEFINED]

## Images/screenshots

**Supported:** [YES / NO / FUTURE]

If supported define:

- formats;
- maximum size;
- image dimensions;
- privacy behavior;
- retention;
- model handling.

## File uploads

**Supported:** [YES / NO / FUTURE]

If supported define:

- allowed types;
- maximum size;
- content validation;
- retention;
- privacy;
- security scanning;
- model handling.

---

# 15. Answer Style

Define the desired public voice.

## Tone

[TO BE DEFINED]

## Typical length

[TO BE DEFINED]

## Technical depth

[TO BE DEFINED]

## Marketing language

[TO BE DEFINED]

## Uncertainty

How should uncertainty be communicated?

[TO BE DEFINED]

## Refusals / redirects

Describe preferred style.

[TO BE DEFINED]

Avoid policy-sounding responses when a simple natural explanation will
suffice.

---

# 16. Branding

## Assistant name

[TO BE DEFINED]

## Tagline

[TO BE DEFINED]

## AI technology attribution

[TO BE DEFINED]

## Relationship to corporate brand

[TO BE DEFINED]

## Branding claims to avoid

[TO BE DEFINED]

---

# 17. User Experience

Define desired interaction behavior.

## Initial screen

[TO BE DEFINED]

## Activity feedback

[TO BE DEFINED]

Activity should describe user-understandable work without exposing protected
internal reasoning.

## Citations

[TO BE DEFINED]

## Errors

[TO BE DEFINED]

## Mobile behavior

[TO BE DEFINED]

## Accessibility requirements

[TO BE DEFINED]

## Answer Delivery Model

Choose the public answer-delivery contract.

**Delivery model:**  
[BUFFERED / STREAMING / HYBRID / TO BE DEFINED]

Describe:

[TO BE DEFINED]

If the application promises validation before exposure, define which operations
must complete before answer content becomes visible.

Possible operations include:

- grounding validation;
- citation validation;
- lifecycle validation;
- disclosure validation;
- bounded repair.

Unvalidated draft content must not be exposed if doing so would violate the
selected delivery guarantee.

## Activity Delivery

**Activity streaming:**  
[YES / NO / TO BE DEFINED]

If activity is shown, define approved user-visible states.

[TO BE DEFINED]

Activity must correspond to real application operations and must not expose
hidden reasoning.

## Repair and Failure Behavior

**Repair allowed:** [YES / NO / TO BE DEFINED]

**Maximum repair attempts:**  
[TO BE DEFINED]

**Failure behavior:**  
[TO BE DEFINED]

Define what the user sees if:

- generation fails;
- retrieval fails;
- validation fails;
- repair fails;
- the request is cancelled.

---

# 18. Request Admission and Cost Controls

Input-size requirements are defined in §14.

This section defines the operational controls used to enforce resource,
capacity, abuse, and cost boundaries.

Do not duplicate question/history limits here. Reference the canonical values
from §14.

Define:

**Per-client rate limit:**  
[TO BE DEFINED]

**Global rate limit:**  
[TO BE DEFINED]

**Per-client concurrency:**  
[TO BE DEFINED]

**Global concurrency:**  
[TO BE DEFINED]

**Bot/human verification:**  
[TO BE DEFINED]

**Request deadline:**  
[TO BE DEFINED]

**Cost objectives:**  
[TO BE DEFINED]

---

# 19. Logging and Retention

## Quality logging

**Enabled:** [TO BE DEFINED]

## Information retained

[TO BE DEFINED]

## Information explicitly excluded

Consider:

- IP addresses;
- browser identifiers;
- cookies;
- credentials;
- bot-verification tokens;
- raw provider responses;
- provider request IDs;
- hidden reasoning;
- unnecessary conversation history.

[TO BE DEFINED]

## Retention period

[TO BE DEFINED]

## Access

Who may access quality/operations data?

[TO BE DEFINED]

---

# 20. Production Architecture

Document the selected production request path.

Example:

    Browser
       ↓
    Edge/CDN
       ↓
    Reverse proxy
       ↓
    Application
       ↓
    AI / retrieval providers

## Hosting

[TO BE DEFINED]

## CDN / edge

[TO BE DEFINED]

## Reverse proxy

[TO BE DEFINED]

## Application runtime

[TO BE DEFINED]

## AI provider integration

[TO BE DEFINED]

## Secret storage

[TO BE DEFINED]

## Origin protection

[TO BE DEFINED]

---

# 21. Deployment and Rollback

## Deployment mechanism

[TO BE DEFINED]

## Release structure

[TO BE DEFINED]

## Pre-activation validation

[TO BE DEFINED]

## Post-activation validation

[TO BE DEFINED]

## Rollback

[TO BE DEFINED]

## Release retention

[TO BE DEFINED]

---

# 22. Production Monitoring

Define:

- health monitoring;
- readiness monitoring;
- uptime monitoring;
- application errors;
- infrastructure monitoring;
- cost monitoring;
- AI usage monitoring;
- quality review.

[TO BE DEFINED]

---

# 23. Evaluation Requirements

Every project should maintain evaluations covering the policies relevant to
that company.

At minimum consider:

| Evaluation area | Required? | Status |
|---|---|---|
| Scope / qualification | YES | |
| Privacy | YES | |
| Disclosure | YES | |
| Source authority | YES | |
| Grounding | YES | |
| Lifecycle | if applicable | |
| Specialized assistance | if applicable | |
| Prompt injection | YES | |
| Input/admission controls | YES | |
| Production trust boundary | YES | |
| Deployment/rollback | YES | |

Company-specific behavioral questions should be added as product decisions are
made.

---

# 24. Product-Owner Decisions

Maintain significant decisions here or in dedicated decision records.

## Decision Template

**Decision ID:** ASK-DEC-___

**Status:**  
[PROPOSED / APPROVED / SUPERSEDED]

**Date proposed:**  
[DATE]

**Date approved:**  
[DATE / NOT YET APPROVED]

**Product owner / approver:**  
[NAME / ROLE]

**Issue:**  
[DESCRIPTION]

**Decision type:**  
[CORPORATE POLICY / ENGINEERING / OPERATIONS / OTHER]

**Alternatives considered:**

1. [OPTION]
2. [OPTION]
3. [OPTION]

**Decision:**  
[DECISION]

**Rationale:**  
[OPTIONAL]

**Affected artifacts:**  
[FILES / POLICIES / EVALUATIONS]

**Supersedes:**  
[DECISION ID / NONE]

**Replaced by:**  
[DECISION ID / NONE]

**Required evaluation changes:**  
[DESCRIPTION / NONE]

**Required implementation changes:**  
[DESCRIPTION / NONE]

**Notes:**  
[OPTIONAL]

An AI recommendation is not an approved corporate-policy decision.

Only decisions with the required approval status should be treated as current
product policy.

Do not delete superseded decisions merely because they are no longer active.
Preserve enough history to understand why earlier implementation or evaluation
results differed from current expectations.

---

# 25. Open Questions

Track unresolved product-policy questions.

| Question | Owner | Blocking stage? | Status |
|---|---|---|---|
| | | | |

The AI should consult this section before assuming that an unresolved question
has already been decided.

---

# 26. Current Project State

This section allows a new AI session or human contributor to determine where
work should resume without reconstructing project history.

**Current stage:**  
[STAGE]

**Current bounded milestone:**  
[DESCRIPTION]

**Completed stages / milestones:**  
[LIST]

**Current completion gate:**  
[DESCRIPTION]

**Required gate evidence:**

- [EVIDENCE]
- [EVIDENCE]

**Evidence currently available:**

- [REFERENCE]
- [REFERENCE]

**Blocking decisions:**

- [DECISION / NONE]

**Known limitations:**

- [LIMITATION / NONE]

**Approval status:**  
[NOT READY / READY FOR OWNER REVIEW / APPROVED TO ADVANCE]

**Authorized next action:**  
[DESCRIPTION]

**Actions not yet authorized:**  
[OPTIONAL]

**Next recommended action:**  
[DESCRIPTION]

Passing tests does not automatically authorize advancement when the completion
gate requires product-owner approval.

Authorization to implement does not automatically authorize:

- external API expenditure beyond approved experiments;
- commit;
- push;
- deployment;
- production configuration changes;
- creation or modification of external resources.