# CoBeing R0 — architecture boundaries / 架构边界

> This describes the intended contract, not an assertion that every component is implemented.

## Network model

**Personal Mesh** connects one person's devices, local services, owned cloud agents and approved tools. IP connectivity should reuse LAN, IPv6, existing VPN/P2P capabilities and safe relay fallbacks when available; CoBeing does not build a mandatory new VPN.

**CoBeing Network** connects people and their agents through mutually agreed relationships, limited shared contexts and revocable permissions.

**CoBeing Basic** provides the common identity, basic memory, relationship and resource registration layer. It is not a centralized model gateway, device proxy, comprehensive personal data warehouse or social messenger.

## Four components

1. **Mobile Entry (required):** lightweight web/mobile entry, shortcuts and supported integrations with existing social tools. A web fallback exists even if native integrations are unavailable.
2. **Local Bridge (optional):** an independent local capability connector for authorized apps, files, agents and providers. CoBeing does not embed the internals of third-party messaging clients.
3. **Cloud Claw / Bot (optional):** existing user-owned or user-authorized agents and services; available APIs and entitlements must be verified per provider.
4. **CoBeing Basic (required):** identity, a user-scoped basic memory space, mutual relationship records, a resource registry and consent/revocation metadata.

A user can join via **1 + 4**. AI tasks require at least one available authorized capability from **2 or 3**. Both may coexist.

## Memory and trust

- Basic Memory is a **private per-user area on shared infrastructure**, not a public shared memory pool.
- User-owned Personal Vaults may contain deeper history; only user-approved information is copied or referenced by Basic.
- Original social messages, credentials, private provider internals and device secrets are not ingested by default.
- External agents receive the minimum selected memory/context needed for the current task; authorization is evaluated by a trusted component, never by untrusted chat text.
- Relationship invitations and shared memory require separate, explicit consent; they never grant blanket device or vault access.
- Users need correction, deletion, export and disconnection paths; model/provider use may have distinct data-processing rules.
- Cloud Basic may need plaintext access for authorized memory retrieval; do not claim end-to-end encryption where that is not true.

## Boundaries and dependencies

Local Bridge and existing providers remain independently maintained. CoBeing does not require users to deploy personal infrastructure to create an account or use Basic Memory. Radio Mesh / Meshtastic is a possible future adapter, not part of the current IP Personal Mesh work.

No third-party API, product entitlement, reliability or compatibility should be described as delivered without actual evidence.
