# CoBeing Capability Sharing V1 — Seed Network

Status: **design + private Claw Connect spike**. No production cross-user execution.

## Product principle

Reuse mature platforms and resources that the user already owns. Do not build a
new Agent runtime, require the user to move accounts, or depend on CoBeing for
local Agent execution. The first visible product value is *useful shared tasks*
through Companion / WorldDesk / an invited web link, not a public compute
marketplace.

Three different things:
1. Platform integration: permitted, official interfaces to QwenPaw/OpenClaw/
   Local Bridge/MCP services.
2. Bring your own capability: reuse your existing connected Agents privately.
3. Offer one bounded capability: another person uses a specific task with
   explicit owner permission. Sharing is **off by default**.

## Seed providers and geography

| Seed | Region | Source | Intended first Offer |
| --- | --- | --- | --- |
| QwenPaw (AgentScope Platform) | Alibaba Cloud, **Singapore** | Dedicated shared Agent / Channel plugin if hosted installation permits | Public-text summary |
| Local Bridge + home service | Shanghai Telecom (dynamic IPv4, optional IPv6) | Private model or separate low-privilege service | Public-text summary |

CoBeing's optional Cloudflare control plane retains account, Offer and Grant
metadata. The provider initiates authenticated outbound WSS; its changing IP is
not its identity. Do not reveal private IP, endpoints, workspace paths or model
credentials in the public catalog. Privacy, region, latency and provider terms
are eligibility constraints, not automatic cross-border fallbacks.

## Identity and state boundaries

Account: individual/organization identity and App permissions only.
Network: provider node, capability declaration, Offer, Grant, Invocation.
Mesh: connection transport and address rotation.
Local Bridge: reuses existing local app/model/Agent but does not import CoBeing
identity or know a specific product's business rules.

Represent lifecycle with distinct states:
- **Detected**: installed or listed, not verified callable.
- **Connected**: authenticated node handshake, not shared.
- **Callable privately**: local owner can invoke with local permissions.
- **Offered**: owner publishes a bounded task and terms.
- **Granted**: named requester has an unexpired, revocable specific permission.
- **Invoked**: gateway and provider each recheck authorization at execution time.

## Minimal service model

`capability_source`: node_id, platform, runtime, owner_id, region.
`capability`: source_id, stable kind, input/output schema, version, side_effects.
`offer`: capability_id, owner_id, audience, limits, region_policy,
data_policy, availability, price_mode (first version: free).
`grant`: offer_id, subject_id, scope, expiry, approval, revoked_at.
`invocation`: grant_id, task_id, deadline, idempotency_key, status, usage.

One capability can have different Offers. No automatic permission follows a
friend relationship, OAuth login, provider registration, or node pairing.
Third-party platform subscription and account credentials are never Offers.

## Minimal user flow

1. The provider discovers its existing Agent/Tool through official APIs.
2. Owner deliberately selects a safe, named task (not an entire workspace).
3. Owner shares it with one or more named partners: quota, concurrency, timeout,
   public-data-only, no outbound write; ability to pause/revoke any time.
4. Recipient opens a link in an existing messaging app, signs in only when
   requesting a protected capability, and accepts data region and terms.
5. Network checks Offer/Grant/region/budget; provider checks again before work.
6. Task executes in a dedicated sandbox/session and returns visible result and
   minimal audit metadata; failures do not silently call a new data recipient.

A shared link is an invitation to claim access, **not a permanent bearer
execution token**. Sensitive or side-effect tasks need a separate approval.
Default routes: own local Agent -> own other resources -> explicitly authorized
partner Offer -> optionally approved seed Offer. Do not infer data permission
from the user's choice of task.

## Minimal API / interoperability (design, not deployed)

- `POST /network/providers/pair` — signed key challenge / approval
- `POST /network/capabilities` — provider declares one bounded task
- `POST /network/offers` — owner explicitly publishes terms
- `POST /network/offers/:id/request` — requester asks for access
- `POST /network/grants/:id/revoke` — owner revokes
- `POST /network/invocations` — eligible authorized task
- `GET /network/invocations/:id` — caller's status and result

Transport candidates: outbound Claw Connect WSS or authorized HTTPS, protocol
versioned separately from upstream Claw Gateway and ACP. ACP stdio is useful
locally but not a built-in public network transport. MCP tool schemas may be
reused for a narrow task; never reuse third-party auth cookies/tokens.

## Minimum viable security

- Pairing key proof, explicit owner approval, short-lived audience-bound signed
  task grants, durable replay and revocation checks, no token passthrough.
- Both sides enforce capability allowlists and input limits; isolate Agent
  memory, tools, workspace, run identity and logs.
- Originating instruction is *untrusted user input*: never let it change grants,
  exfiltrate private data, read arbitrary files, or approve side effects.
- CPU/cost/usage quotas, bounded response size, per-owner concurrency, global
  abuse prevention and simple provider pause.
- Only necessary task data and metadata leave devices. Data leaving mainland
  China for Singapore requires explicit user awareness and valid permissions.
- No guarantees derived solely from personal residential broadband; ensure
  ISP terms and service availability are acceptable.
- Free/model subscription conditions must permit *this* delegated use; never
  pool personal plan credits for third-party SaaS without permission.

## Release / acceptance gates

- **R0.5 Seed:** named test requester invokes one public-text task with a
  dedicated Singapore QwenPaw Agent, with the owner able to revoke. Hosted
  plugin permission and licensed model use MUST be verified.
- **R1:** repeat through an independent provider, initially Shanghai via
  Local Bridge or a dedicated service; IP rotation does not affect identity.
- **R2:** another contributor joins without modifying CoBeing Core code,
  invites and revocation work, and the network accurately reports offline.
- Later: public discovery, commercial credits and community exchange only
  after trusted supply/demand, safety, billing and provider terms are proven.

A private [integrations-lab](https://github.com/CoBeing/cobeing-integrations-lab)
draft PR contains a synthetic-only protocol test harness and experimental
OpenClaw/QwenPaw adapters. This **does not** mean either hosted provider is
connected or that cross-user execution has been released.
