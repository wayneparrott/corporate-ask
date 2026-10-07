# Corporate Ask Security and Operations Standard

## Purpose

This standard defines reusable security, reliability, privacy, cost-control,
deployment, and operational principles for a production Corporate Ask
application.

It should be used together with:

- `ASK-BUILD-PLAYBOOK.md`
- `ASK-PROJECT-TEMPLATE.md`
- `ASK-EVALUATION-STANDARD.md`

A Corporate Ask application exposes paid AI capabilities to anonymous or
semi-anonymous Internet users.

Production architecture must therefore assume that requests may be malformed,
automated, abusive, adversarial, expensive, or intentionally designed to
bypass application policy.

Security and operational controls should protect the application without
making legitimate use unnecessarily difficult.

---

# 1. Security Principles

## 1.1 Treat the Browser as Untrusted

Information supplied by the browser must not automatically be trusted.

This includes:

- request headers;
- client IP claims;
- forwarding headers;
- origin-related headers;
- conversation history;
- content type;
- request size;
- bot-verification tokens;
- uploaded content;
- application state.

Validation should occur at an appropriate trusted boundary.

---

## 1.2 Reject Cheaply Before Processing Expensively

Prefer the processing order:

    inexpensive validation
        ↓
    bot / admission checks
        ↓
    resource admission
        ↓
    classification / policy
        ↓
    retrieval
        ↓
    model generation
        ↓
    validation / repair
        ↓
    response

Do not consume scarce model, retrieval, or concurrency resources for requests
that can already be rejected deterministically.

---

## 1.3 Minimize Trusted Components

Every component trusted to establish security-sensitive information should be
explicitly identified.

Examples:

- which proxy establishes client identity;
- which component terminates public TLS;
- which component authenticates the application origin;
- which service may access model credentials;
- which process may write operational logs.

Trust should arise from architecture and validation, not header names.

---

## 1.4 Minimize Secrets

Secrets should exist only where required.

Never expose server credentials to browser-delivered code.

Examples of server-side secrets include:

- AI provider API keys;
- bot-verification secret keys;
- origin-authentication secrets;
- private service credentials.

Public browser configuration should be clearly distinguished from secrets.

---

## 1.5 Privacy Is an Operational Property

Privacy policy applies to infrastructure as well as model responses.

Review:

- application logs;
- reverse-proxy logs;
- CDN/edge logs;
- provider logs;
- monitoring systems;
- error reports;
- deployment logs;
- evaluation results.

A privacy-conscious application can still leak unnecessary information through
operational tooling if those systems are ignored.

---

# 2. Production Trust Model

Document the complete production request path.

Example:

    Browser
       ↓
    Public edge / CDN
       ↓
    Origin reverse proxy
       ↓
    Corporate Ask application
       ↓
    AI and retrieval services

For every hop record:

- whether the component is trusted;
- what identity it establishes;
- what headers it may create;
- which incoming headers it must remove;
- how the next component authenticates it;
- where TLS terminates;
- what network paths are permitted.

Do not deploy until this model is explicit.

---

# 3. Origin Protection

The application origin should not be unintentionally reachable through a path
that bypasses the public security layer.

Possible controls include:

- firewall restrictions;
- private networking;
- authenticated origin requests;
- mutual TLS;
- reverse-proxy authentication;
- cloud-provider origin controls.

The exact mechanism is deployment-specific.

The important property is:

> A requester should not be able to bypass required edge controls simply by
> discovering the origin address.

Test this property.

---

# 4. Canonical Client Identity

Rate limiting and abuse controls often require a client identifier such as an
IP address.

Forwarding headers are dangerous when their provenance is unclear.

Do not trust arbitrary browser-supplied values such as:

- `X-Forwarded-For`;
- `X-Real-IP`;
- `Forwarded`;
- provider-specific connecting-IP headers.

A trusted edge or reverse proxy should establish one canonical client identity
for the application.

The application should accept that identity only when the immediate upstream
connection is trusted.

Reject malformed or ambiguous canonical identity values.

---

# 5. Header Sanitization

At a trusted proxy boundary:

1. remove security-sensitive forwarding headers supplied by the requester;
2. derive trusted values from the authenticated upstream connection or trusted
   edge metadata;
3. create canonical application headers;
4. forward only the values the application is designed to trust.

Do not append trusted identity to an untrusted forwarding chain and assume the
result is safe.

---

# 6. Origin Authentication

Where appropriate, the reverse proxy or trusted upstream component should
authenticate itself to the application.

The mechanism may use:

- a server-generated shared secret;
- signed metadata;
- mTLS;
- private network identity;
- another deployment-specific mechanism.

The credential must:

- never originate in browser code;
- never be accepted from an untrusted public path;
- not be unnecessarily logged;
- be validated before protected application routes are processed.

---

# 7. Host, Origin and Protocol Validation

Where the deployment architecture permits reliable validation, establish the
expected:

- public host;
- browser origin;
- protocol;
- application upstream.

Reject unexpected values on protected application routes.

Do not assume these checks replace CSRF, authentication, bot protection, or
network security. They are complementary controls.

---

# 8. Request Schema Validation

Define an explicit request contract.

Reject:

- malformed JSON;
- unsupported content types;
- unexpected fields when appropriate;
- invalid message roles;
- invalid history structures;
- oversized values;
- structurally ambiguous requests.

Avoid accepting arbitrary objects and allowing downstream model code to
interpret them.

---

# 9. Input Limits

Define explicit limits for:

- HTTP request body;
- current question;
- individual historical messages;
- conversation turns;
- total conversation history;
- image uploads;
- file uploads.

Limits should be enforced server-side.

Browser-side limits improve usability but are not security controls.

Choose limits according to product purpose rather than the maximum context
window supported by the underlying model.

---

# 10. Upload Security

If screenshots or files are supported, define additional controls.

Consider:

- allowed MIME types;
- extension validation;
- magic-byte/content validation;
- maximum compressed size;
- maximum expanded size;
- image dimensions;
- decompression bombs;
- malformed files;
- metadata handling;
- malware scanning where appropriate;
- retention;
- deletion;
- logging exclusions.

Do not add general file upload merely because the model supports multimodal
input.

Enable only formats justified by the product.

---

# 11. Bot and Automated-Abuse Protection

Public AI endpoints may require a human/bot verification mechanism.

Verification should occur before expensive model processing.

Validate server-side where applicable:

- token authenticity;
- expiration;
- expected hostname;
- expected action/context;
- replay behavior.

Do not log verification tokens.

Development bypasses, test keys, or test modes must not silently weaken
production verification.

---

# 12. Rate Limiting

Use layered limits when appropriate.

Possible dimensions:

- short burst per client;
- sustained requests per client;
- hourly/daily client limits;
- global admission rate.

Rate limits should protect both infrastructure and model spend.

Define response behavior clearly so legitimate clients can distinguish
temporary throttling from application failure.

Do not depend solely on edge rate limiting when application-side controls are
important to cost protection.

---

# 13. Concurrency Control

Rate and concurrency limits solve different problems.

A client sending several long-running requests simultaneously can consume
significant resources without exceeding a simple requests-per-minute limit.

Consider:

- per-client concurrent request limit;
- global concurrent paid-pipeline limit;
- retrieval concurrency;
- verification concurrency.

Prefer bounded concurrency over an unbounded server queue.

---

# 14. Resource Admission

Acquire scarce resources only after inexpensive validation succeeds.

A conceptual sequence:

    request received
        ↓
    schema / size checks
        ↓
    bot verification
        ↓
    paid-pipeline admission
        ↓
    policy classification
        ↓
    retrieval / generation

Document exactly when a request begins consuming scarce capacity.

---

# 15. Timeouts

Every external dependency should have bounded waiting behavior.

Consider separate timeouts for:

- bot verification;
- retrieval;
- page fetch;
- AI provider request;
- total request;
- deployment validation;
- health probes.

A timeout should result in predictable cleanup.

Avoid one timeout value controlling unrelated operations when their failure
characteristics differ.

---

# 16. Cancellation and Aborted Requests

A disconnected browser does not necessarily mean upstream work has stopped.

Understand whether each external operation supports cancellation.

If work cannot reliably be cancelled:

- avoid immediately releasing concurrency capacity if the expensive work may
  still be executing;
- consider a bounded quarantine period;
- prevent repeated disconnects from creating unbounded invisible work.

Test aborted-request behavior.

---

# 17. Cost Controls

Treat model spend as a production resource.

Track where appropriate:

- model calls per request;
- retrieval calls;
- input tokens;
- output tokens;
- estimated request cost;
- repair calls;
- request duration.

Set operational budgets or alerts.

Do not rely solely on provider account limits as the application's cost
control.

---

# 18. Model and Provider Configuration

Model/provider selection should be server-side configuration.

The browser should not determine arbitrary model identity unless the product
explicitly supports such behavior.

Production configuration should allow controlled model changes without
requiring disclosure of protected implementation details.

Provider/model changes should trigger relevant behavioral regression testing.

---

# 19. Retrieval Security

External content is untrusted input.

Retrieved pages may contain:

- malicious instructions;
- prompt injection;
- misleading claims;
- stale information;
- third-party copyrighted content;
- redirects;
- unexpectedly large responses.

Retrieval systems should define:

- allowed source boundaries;
- redirect rules;
- timeout;
- maximum response size;
- accepted content types;
- source identity;
- applicability rules.

Retrieved instructions do not override Corporate Ask policy.

---

# 20. Output Validation

Where policy requires it, validate generated answers before delivery.

Possible checks include:

- citation validity;
- source applicability;
- lifecycle consistency;
- disclosure compliance;
- grounding;
- answer-size limits.

If repair is supported, bound the number of repair attempts.

Avoid open-ended model self-correction loops.

---

# 21. Response Streaming

If the application streams activity or answers, define the transport contract.

For activity streaming:

- emit complete framed events;
- tolerate network chunk boundaries;
- do not assume one transport chunk equals one logical event;
- distinguish activity from final answer;
- handle cancellation and parse failures.

Do not expose hidden reasoning or chain-of-thought as activity.

Activity messages should represent user-understandable workflow states.

---

# 22. Security Headers

Public web applications should define appropriate browser security headers.

Consider:

- Content-Security-Policy;
- frame restrictions;
- MIME sniffing protection;
- referrer policy;
- permissions policy;
- HSTS where appropriate.

The exact policy depends on application resources and third-party integrations.

Test important headers through the actual public serving path.

---

# 23. Production Logging

Define the purpose of every retained field.

Potentially useful fields include:

- timestamp;
- request outcome;
- classification decisions;
- timing;
- model usage;
- estimated cost;
- retrieval/citation information;
- final answer where product policy permits;
- error category.

Do not retain data merely because it is available.

---

# 24. Logging Exclusions

Explicitly identify information that must not be retained.

Candidates include:

- credentials;
- authorization headers;
- bot-verification tokens;
- origin-authentication secrets;
- raw provider responses;
- provider request identifiers;
- hidden model reasoning;
- unnecessary cookies;
- unnecessary IP addresses;
- unnecessary browser fingerprints;
- conversation history not required for the stated logging purpose.

Apply the same review to reverse-proxy and edge logs.

---

# 25. Retention

Every persistent operational dataset should have a retention policy.

Define:

- retention duration;
- deletion mechanism;
- access controls;
- backup implications;
- exceptions required for incidents or legal obligations.

Do not state that data expires after a period unless an actual deletion
mechanism enforces that policy.

Verify retention operationally.

---

# 26. Health and Readiness

Health and readiness answer different questions.

## Health

Typically answers:

> Is the application process alive?

Health endpoints should be inexpensive and should not depend unnecessarily on
external services.

## Readiness

Typically answers:

> Is this instance correctly configured to serve application traffic?

Readiness may verify important local configuration or dependencies.

Do not expose secrets or excessive diagnostic information through either
endpoint.

---

# 27. Graceful Shutdown

On shutdown:

1. stop accepting new work;
2. allow bounded in-flight work to complete where practical;
3. stop background resources;
4. flush required operational data;
5. exit within a defined deadline.

Deployment tooling and service managers should understand this deadline.

---

# 28. Least-Privilege Runtime

Run the application under a dedicated non-root identity where possible.

Limit:

- filesystem access;
- writable directories;
- environment access;
- network access;
- service-manager permissions.

Separate deployment privileges from application-runtime privileges.

---

# 29. Secret Storage

Production secrets should not be stored in:

- source control;
- browser bundles;
- public build artifacts;
- ordinary application logs.

Use an appropriate server-side secret mechanism.

Protect configuration-file ownership and permissions when files are used.

Document secret rotation procedures.

---

# 30. Build Integrity

Production deployment should use a reproducible process.

Consider:

- dependency lockfiles;
- deterministic installation;
- required runtime versions;
- production build validation;
- static checks;
- artifact validation.

A developer workstation's existing dependency tree should not define the
production release.

---

# 31. Release Structure

Prefer immutable or timestamped releases over modifying the active application
directory in place.

A conceptual structure:

    application/
        releases/
            release-A/
            release-B/
            release-C/
        current -> releases/release-C
        previous -> releases/release-B

This enables:

- atomic activation;
- rollback;
- release inspection;
- bounded retention.

Equivalent mechanisms provided by containers or deployment platforms are also
valid.

---

# 32. Pre-Activation Validation

Before activating a release verify as appropriate:

- source revision;
- dependency installation;
- build success;
- required configuration;
- artifact existence;
- artifact permissions;
- secret absence from public bundles;
- runtime compatibility;
- service-account readability;
- web-server readability.

Do not activate a release known to be unusable.

---

# 33. Filesystem Permissions

Production files may be consumed by more than one identity.

Examples:

- deployment user;
- application service account;
- reverse proxy/web server.

Validate access from the identity that actually consumes the file.

A successful application process does not prove that the web server can read
static assets.

Avoid unnecessarily broad permissions while ensuring required traversal and
read access.

---

# 34. Atomic Activation

Switch from the old release to the new release atomically where possible.

Do not expose users to a partially copied or partially built release.

After activation, restart or reload only the components that require it.

---

# 35. Post-Activation Validation

A deployment is not successful merely because the application process starts.

Validate multiple layers where applicable:

1. application process;
2. local application health;
3. reverse-proxy path;
4. static frontend;
5. canonical host behavior;
6. public edge path.

At minimum, validate the layers necessary to detect failures that would make
the service unavailable to users.

---

# 36. Automatic Rollback

Where practical, deployment should automatically restore the previous known
working release when post-activation validation fails.

Rollback should itself be validated.

If rollback validation fails:

- report failure clearly;
- do not claim deployment success;
- preserve enough diagnostic information for recovery.

---

# 37. Deployment Locking

Prevent overlapping deployments from modifying shared release state
simultaneously.

Use a deployment lock or equivalent platform mechanism.

---

# 38. Release Retention

Keep enough releases for practical rollback and diagnosis without allowing
unbounded storage growth.

Protect:

- current release;
- previous rollback release;
- releases required by active processes.

Remove older releases according to a defined policy.

---

# 39. Production Monitoring

Monitor the system at several levels.

## Availability

Can users reach the service?

## Application health

Is the application process functioning?

## Infrastructure

Are CPU, memory, disk, and network within acceptable bounds?

## AI usage

Are model requests, tokens, cost, latency, and errors within expected ranges?

## Quality

Are representative answers continuing to meet product expectations?

No single monitoring signal answers all of these questions.

---

# 40. Alerts

Alerts should correspond to conditions that require action.

Examples:

- sustained public outage;
- repeated deployment failure;
- unusual error rate;
- resource exhaustion;
- abnormal model spend;
- retention failure;
- certificate expiration.

Avoid excessive alerts that train operators to ignore them.

---

# 41. Backups

Determine what actually requires backup.

A stateless Corporate Ask application may not need application-server backup
if source, configuration, and deployment artifacts are reproducible.

Persistent data may require backup depending on:

- business value;
- retention policy;
- privacy policy;
- recovery objectives.

Do not back up short-retention data indefinitely by accident.

---

# 42. Failure Modes

Document expected behavior for failures of:

- bot-verification provider;
- AI provider;
- retrieval provider;
- DNS;
- CDN/edge;
- reverse proxy;
- application process;
- logging storage;
- monitoring;
- deployment.

Prefer understandable temporary failure over unsafe fallback.

For example, do not bypass bot verification merely because the verification
provider is unavailable unless that behavior is an explicit product/security
decision.

---

# 43. Production Security Validation

Before launch test:

- direct-origin bypass;
- spoofed client-IP headers;
- malformed canonical client identity;
- missing/invalid origin authentication;
- unexpected host/origin;
- oversized requests;
- malformed JSON;
- rate limits;
- concurrency limits;
- bot-verification failure;
- secret exposure;
- logging exclusions;
- static-file permissions;
- health/readiness;
- rollback.

Use safe testing methods appropriate to the environment.

---

# 44. Operational Decision Record

Important production decisions should be documented.

Examples:

- why a particular edge provider is trusted;
- why a rate limit was selected;
- why an IP address is or is not retained;
- why a specific upload format is allowed;
- why a retention period was chosen;
- why a model/provider change was made.

Operational configuration without rationale becomes difficult to maintain.

---

# 45. Platform Independence

This standard defines required properties, not a mandatory vendor stack.

A valid implementation might use:

    Cloudflare
        ↓
    Nginx
        ↓
    Node
        ↓
    AI provider

Another might use:

    cloud load balancer
        ↓
    container platform
        ↓
    application
        ↓
    AI provider

Another might use a managed serverless architecture.

Each is acceptable if it satisfies the project's trust, security, privacy,
cost, deployment, and operational requirements.

Do not copy infrastructure choices from a reference implementation without
understanding why they were chosen.

---

# 46. Security and Operations Completion Gate

Before production launch confirm:

- the production trust boundary is documented;
- direct-origin bypass is controlled;
- canonical client identity is established safely;
- security-sensitive headers are sanitized;
- secrets remain server-side;
- request schemas and sizes are bounded;
- automated abuse controls exist where required;
- rate and concurrency limits are enforced;
- external operations have timeouts;
- aborted work cannot create unbounded resource use;
- model spend is measurable and bounded;
- retrieval treats external content as untrusted;
- logs follow explicit collection and retention policy;
- health/readiness behavior is defined;
- the runtime uses appropriate least privilege;
- deployment is repeatable;
- activation is atomic or equivalently safe;
- the actual serving path is validated after deployment;
- rollback is proven;
- production monitoring is active;
- important security controls have regression tests.

The goal is not merely to keep the server running.

The goal is to operate Corporate Ask as a controlled public service whose
security, privacy, reliability, and cost characteristics are understood.