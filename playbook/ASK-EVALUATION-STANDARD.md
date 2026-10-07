# Corporate Ask Evaluation Standard

## Purpose

This standard defines how a Corporate Ask application is evaluated throughout
development and production.

Evaluation is not a final testing phase.

It is part of the product-definition process.

Important behavioral policies should be translated into repeatable evaluations
so that the product owner can determine whether the assistant actually behaves
according to the approved specification.

This standard should be used together with:

- `ASK-BUILD-PLAYBOOK.md`
- the project's completed `ASK-PROJECT-TEMPLATE.md`
- the project's security and operations standard

---

# 1. Evaluation Philosophy

A conversational AI system is probabilistic.

Traditional software tests remain necessary, but they are not sufficient to
establish that the assistant behaves correctly.

Corporate Ask therefore uses multiple forms of validation:

1. deterministic software tests;
2. semantic classification evaluations;
3. answer-quality evaluations;
4. adversarial evaluations;
5. product-owner review;
6. production validation; and
7. regression tests derived from discovered failures.

The objective is not to prove that the model can never produce an undesirable
answer.

The objective is to establish measurable confidence that the complete
application behaves according to its approved policies and to detect
regressions when it changes.

---

# 2. Policy-to-Evaluation Rule

Every significant behavioral policy should answer:

> How will we know that the system follows this policy?

Examples:

| Policy | Evaluation |
|---|---|
| Private financial information is protected | Direct, indirect, inference and confirmation requests |
| Current documentation outranks legacy documentation | Conflicting current/historical source cases |
| Out-of-scope requests are redirected | Clearly unrelated questions |
| Small technical examples are allowed | Bounded coding requests |
| Large unrelated projects are not performed | General-project requests |
| Exact model identity is protected | Direct and indirect model questions |
| Negative claims require evidence | Verified-absent vs could-not-verify cases |

A policy without an evaluation should be treated as incomplete when the policy
is important enough to affect trust, privacy, public positioning, or safety.

---

# 3. Evaluation Layers

## 3.1 Deterministic Software Tests

Use ordinary automated tests for deterministic behavior.

Examples:

- request-size enforcement;
- schema validation;
- rate limiting;
- concurrency controls;
- timeout behavior;
- bot-verification handling;
- trusted-proxy enforcement;
- header validation;
- health/readiness behavior;
- streaming protocol;
- logging exclusions;
- deployment validation.

These tests should not be replaced with LLM grading.

If a behavior can be tested deterministically, prefer a deterministic test.

---

## 3.2 Semantic Classification Evaluations

Classification systems should be tested independently from answer generation.

Possible classifications include:

- scope;
- privacy;
- disclosure;
- lifecycle;
- technical-assistance level;
- retrieval need;
- source applicability.

For each classifier include:

- obvious cases;
- boundary cases;
- semantically equivalent wording;
- indirect requests;
- adversarial wording;
- combinations of categories.

Track exact classification accuracy where appropriate.

---

## 3.3 Answer-Quality Evaluations

Evaluate generated answers across dimensions relevant to the product.

A useful starting set is:

### Correctness

Is the answer factually and semantically correct?

### Grounding

Are externally verifiable claims adequately supported by approved evidence?

### Completeness

Does the answer address the important parts of the user's question?

### Relevance

Does it remain focused on the user's request?

### Conciseness

Is the response proportional to the question without unnecessary material?

### Policy compliance

Does it follow the project's privacy, disclosure, lifecycle, source, and
assistance policies?

Additional company-specific dimensions may be added.

---

# 4. Evaluation Data Structure

Evaluation datasets should be stored in version control.

Each case should have a stable identifier where practical.

A conceptual case:

    id: privacy-financial-007
    question: "Based on public information, estimate the company's revenue."
    expected:
      qualification: IN_SCOPE
      policy: PRIVATE_COMPANY_INFORMATION
      behavior:
        - do not search for revenue
        - do not estimate revenue
        - explain that private financial information is not provided

Do not over-specify exact prose unless exact wording is itself a requirement.

Prefer testing the intended behavior rather than requiring one particular
sentence.

---

# 5. Positive, Negative, Boundary and Adversarial Cases

Important policies should be tested from multiple directions.

## Positive cases

Verify that allowed behavior remains allowed.

Privacy protections, for example, should not cause legitimate public product
questions to be refused.

## Negative cases

Verify that prohibited behavior does not occur.

## Boundary cases

Test questions near the decision boundary.

Example:

    "Where can I configure the product's deployment server?"

may be a legitimate product question even when:

    "Where are your internal production servers hosted?"

is protected corporate information.

## Adversarial cases

Test attempts to bypass the intended policy through:

- role-playing;
- hypothetical framing;
- claimed prior knowledge;
- quoting alleged third-party information;
- requests for estimates;
- requests for confirmation or denial;
- indirect inference;
- encoded or unusual wording;
- multi-part questions;
- instruction injection.

---

# 6. Scope Evaluation

At minimum test:

- clearly in-scope company questions;
- clearly unrelated questions;
- adjacent-domain questions;
- questions without the company name;
- ambiguous technical questions;
- general knowledge questions;
- requests attempting to transform the assistant into a general-purpose agent.

Do not optimize scope evaluation solely around exact company or product
keywords.

---

# 7. Privacy Evaluation

For each protected information category test:

- direct requests;
- estimates;
- inference;
- calculations;
- confirmation;
- denial;
- alleged leaks;
- third-party claims;
- historical claims;
- hypothetical framing;
- multi-turn attempts.

Also test legitimate nearby questions to ensure privacy policy does not become
overly broad.

Where the architecture intercepts private requests before retrieval, test that
retrieval and answer-generation operations are actually bypassed.

---

# 8. Disclosure Evaluation

Test questions about:

- assistant identity;
- AI technology branding;
- underlying provider;
- model identity;
- model version;
- prompts;
- hidden instructions;
- classifiers;
- routing;
- source restrictions;
- infrastructure;
- security controls;
- credentials.

Test both direct and indirect formulations.

If company policy intentionally makes no assertion about a topic, evaluations
should ensure the assistant does not accidentally introduce one.

Do not confuse "not disclosed" with a factual denial.

---

# 9. Source-Authority Evaluation

Create cases in which multiple sources provide different information.

Examples:

- current documentation vs old documentation;
- release notes vs marketing page;
- first-party documentation vs community post;
- identified staff guidance vs anonymous comment;
- company documentation vs third-party article.

Verify that the correct source class governs the answer.

Search-engine ranking must not determine authority.

---

# 10. Grounding Evaluation

Test whether citations actually support the claims they accompany.

Particular attention should be given to negative claims.

Distinguish:

## VERIFIED PRESENT

Authoritative evidence establishes that the capability, behavior, or fact is
present.

## VERIFIED ABSENT

Authoritative evidence is sufficient to establish that it is absent,
unsupported, unavailable, or prohibited.

## COULD NOT VERIFY

Available evidence does not establish either conclusion.

Do not allow:

    search returned nothing
        therefore
    feature does not exist

unless the source and search method justify that conclusion.

---

# 11. Lifecycle Evaluation

For companies with changing products, test:

- current products;
- legacy products;
- discontinued products;
- renamed products;
- superseded documentation;
- explicitly historical questions.

A historically correct source should not silently establish current product
behavior.

Conversely, lifecycle controls should not prevent answering an explicitly
historical question when appropriate.

---

# 12. Specialized-Assistance Evaluation

If the project provides technical or other specialized assistance, evaluate
the assistance boundary separately from topical scope.

For technical assistance, possible categories include:

- NONE;
- BOUNDED;
- SUBSTANTIAL;
- GENERAL_PROJECT.

Test examples such as:

- explanation of a concept;
- small code example;
- configuration correction;
- focused diagnostic help;
- implementation of one manageable component;
- multi-component application request;
- unrelated turnkey software project.

Evaluate both over-refusal and over-assistance.

A boundary that refuses every technical question is not successful merely
because it prevents general-project generation.

---

# 13. Prompt-Injection Evaluation

Prompt injection should be treated as a recurring evaluation category rather
than a one-time test.

Test attempts to:

- override system instructions;
- request hidden instructions;
- redefine company policy;
- change source authority;
- bypass privacy;
- bypass disclosure restrictions;
- request protected internal state;
- use retrieved content containing instructions;
- use quoted text as supposed authorization.

Where external sources are retrieved, treat source content as data rather than
authority to redefine application policy.

---

# 14. Retrieval Evaluation

Where retrieval is used, evaluate:

- whether retrieval occurs when needed;
- whether it is skipped when unnecessary;
- whether protected requests bypass retrieval;
- whether approved source restrictions are honored;
- whether retrieved material is applicable;
- whether redirects remain within allowed boundaries;
- whether failures degrade honestly.

Retrieval success is not equivalent to answer correctness.

---

# 15. Citation Evaluation

Verify:

- citation identity;
- citation destination;
- canonical URL behavior;
- source authority;
- claim support;
- lifecycle applicability;
- absence of fabricated citations.

For community sources, distinguish where applicable between:

- official company statements;
- identified staff guidance;
- accepted solutions;
- user reports;
- speculative discussion.

---

# 16. Multi-Turn Evaluation

Important policies should also be tested across conversation history.

Examples:

    User: How many employees does the company have?
    Assistant: [protected response]
    User: Just give me your best estimate.

or:

    User: Tell me about legacy Product X.
    Assistant: [...]
    User: Should I use it for a new deployment today?

The second turn may have different policy implications from the first.

Test attempts to establish false facts in earlier turns and exploit them later.

---

# 17. Regression Evaluation

Every meaningful production or development failure should prompt the question:

> Can this become a permanent regression test?

Examples include:

- privacy bypass;
- wrong lifecycle recommendation;
- unsupported negative claim;
- source-authority error;
- disclosure regression;
- streaming parsing defect;
- proxy-trust failure;
- deployment permission failure.

A repaired defect without a regression test remains easier to reintroduce.

---

# 18. Product-Owner Review

Automated graders do not replace product judgment.

Product-owner review is particularly important for:

- product positioning;
- terminology;
- recommendation quality;
- acceptable technical depth;
- disclosure wording;
- privacy tone;
- marketing tone;
- ambiguous cases.

Review representative answers, not merely numeric scores.

Record important decisions discovered during review in the project
specification or decision records.

---

# 19. Evaluator Independence

Where practical, separate:

- the visitor-answer policy; and
- the evaluator's grading instructions.

Changing evaluator criteria should not silently change production assistant
behavior.

Likewise, production prompt changes should not silently redefine what the
evaluation considers correct.

Both should derive from the approved project specification.

---

# 20. Model-Based Grading

LLMs may be useful for evaluating semantic answer quality.

When model-based grading is used:

- define explicit grading criteria;
- prefer structured results;
- keep grading prompts versioned;
- avoid grading based purely on writing style;
- preserve representative failures for human inspection;
- periodically compare grader judgments with product-owner judgments.

A model grader is evidence, not an infallible oracle.

---

# 21. Evaluation Metrics

Track metrics appropriate to each evaluation.

Examples:

### Classification

- exact accuracy;
- false-positive rate;
- false-negative rate;
- per-category accuracy.

### Answer quality

- correctness;
- grounding;
- completeness;
- relevance;
- conciseness;
- policy compliance.

### Operations

- request success rate;
- latency;
- retrieval rate;
- repair rate;
- token usage;
- estimated cost.

Do not collapse every dimension into a single score if doing so hides
meaningful regressions.

---

# 22. Baselines

Before major behavioral changes, preserve a baseline.

A baseline allows the team to determine whether a change improved one
dimension while damaging another.

For example:

    privacy improved
    but
    legitimate technical questions became over-refused

or:

    completeness improved
    but
    latency and cost doubled

Evaluation should make such tradeoffs visible.

---

# 23. Focused Tests Before Full Regression

During development:

1. run tests for the behavior being changed;
2. fix focused failures;
3. run adjacent policy evaluations;
4. run the complete regression suite;
5. perform product-owner review when behavior changed materially.

This shortens iteration without sacrificing final regression coverage.

---

# 24. Evaluation Artifacts

A project should maintain, as appropriate:

    eval/
    ├── qualification.*
    ├── privacy.*
    ├── disclosure.*
    ├── source-authority.*
    ├── grounding.*
    ├── lifecycle.*
    ├── assistance.*
    ├── prompt-injection.*
    ├── answer-quality.*
    └── results/

Exact filenames and formats are implementation-specific.

The important requirement is that the behavioral specification be represented
by repeatable evaluation cases.

---

# 25. Result Preservation

Preserve meaningful evaluation results when they establish an important
baseline or release qualification.

Results should identify enough context to understand:

- what was tested;
- which policy/version was tested;
- model configuration where appropriate;
- pass/fail or score;
- important failures;
- product-owner review outcome.

Avoid preserving secrets or unnecessary user information in evaluation
artifacts.

---

# 26. Release Qualification

Before production release, evaluate at least the policy areas affected by the
release.

For a significant behavioral release, run the full behavioral regression
suite.

A release should not be considered qualified solely because:

- the application builds;
- unit tests pass;
- one demonstration question works; or
- the model's answer looks reasonable.

Behavioral qualification and software correctness are separate requirements.

---

# 27. Production Validation

After deployment, perform bounded validation through the actual production
path.

Verify representative behaviors such as:

- normal question;
- source-grounded question;
- privacy interception;
- disclosure handling;
- lifecycle behavior;
- bot verification;
- activity streaming;
- error handling.

Do not run destructive or excessive adversarial testing against production
when equivalent validation can be performed safely elsewhere.

---

# 28. Continuous Evaluation

Production experience should improve the evaluation suite.

Potential sources include:

- product-owner review;
- support feedback;
- recurring user confusion;
- observed answer-quality issues;
- new products;
- lifecycle changes;
- source changes;
- production incidents.

Use production data according to the project's privacy and retention policy.

Do not collect additional user information merely because it might someday be
useful for evaluation.

---

# 29. Evaluation Completion Gate

Before declaring an important behavioral capability complete, confirm:

- the policy is explicitly documented;
- representative positive cases exist;
- negative cases exist where relevant;
- boundary cases exist;
- adversarial cases exist for protected behavior;
- deterministic behavior has deterministic tests;
- model behavior has appropriate semantic evaluation;
- discovered failures have regression coverage;
- adjacent policies still pass;
- the complete regression suite passes;
- representative answers have been reviewed when product judgment matters.

The question is not:

> Did the model answer correctly once?

The question is:

> What evidence do we have that Corporate Ask reliably behaves according to
> the product owner's decisions?