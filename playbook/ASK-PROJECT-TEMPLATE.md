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

## Approved domains

[TO BE DEFINED]

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

---

# 18. Request Admission and Cost Controls

Define:

**Request body limit:**  
[TO BE DEFINED]

**Question limit:**  
[TO BE DEFINED]

**History limit:**  
[TO BE DEFINED]

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

**Date:**  
[DATE]

**Issue:**  
[DESCRIPTION]

**Alternatives considered:**

1. [OPTION]
2. [OPTION]
3. [OPTION]

**Decision:**  
[PRODUCT-OWNER DECISION]

**Rationale:**  
[OPTIONAL]

**Affected artifacts:**  
[FILES / POLICIES / EVALUATIONS]

---

# 25. Open Questions

Track unresolved product-policy questions.

| Question | Owner | Blocking stage? | Status |
|---|---|---|---|
| | | | |

The AI should consult this section before assuming that an unresolved question
has already been decided.

---

# 26. Current Project Stage

**Current stage:**  
[STAGE]

**Completed stages:**  
[LIST]

**Current completion gate:**  
[DESCRIPTION]

**Blocking decisions:**  
[LIST]

**Next recommended action:**  
[DESCRIPTION]

This section should be kept current so that a new AI session can quickly
determine where development should resume.