# Privacy and Security Architecture

## Privacy principles

- Core readiness works locally without an account.
- Collect the minimum data needed for a user-selected capability.
- Ask at the moment a permission is needed and explain the consequence of declining.
- Separate consent by purpose: sync, calendar, images, AI classification, diagnostics, and supporter access.
- Default diagnostics off for the MVP; use privacy-preserving operational health metrics only after opt-in.
- No advertising, data brokerage, cross-context tracking, or model training on personal data.
- Make export, correction, supporter review, revocation, and deletion understandable.

## Trust boundaries

1. Participant device and platform keystore.
2. Supporter device and browser.
3. Wayfinder public edge and API.
4. Data stores and internal workers.
5. Weather, calendar, identity, and optional AI providers.
6. Community modules and content packages.

Data crossing a boundary requires an authenticated actor, authorized purpose, encrypted transport, validated schema, minimal payload, and auditable decision.

## Threat model

| Threat | Example | Required mitigation |
| --- | --- | --- |
| Unauthorized supporter access | Former supporter still edits activities | Expiring granular grants, periodic review, immediate revoke, session invalidation |
| Coercive configuration | Supporter hides or changes participant choices | Non-delegable consent/accessibility controls, visible history, participant confirmation |
| Schedule/location exposure | Logs contain appointment details | Structured redaction, coarse location, short log retention, no payload logging |
| Wardrobe image disclosure | Public blob URL leaks images | Private containers, per-object authorization, short-lived scoped access |
| Device loss | Local plan and schedule exposed | OS device security, encrypted DB, keystore key, remote cloud-session revoke |
| Sync replay or duplication | Operation applied twice | UUID operation IDs, payload hash, idempotency ledger, monotonic cursor |
| Malicious calendar content | Event text attempts code/markup injection | Treat provider content as untrusted, encode output, sanitize controlled notes |
| Supply-chain compromise | Contributor dependency executes malicious code | Lockfiles, provenance, review, scanning, minimal CI permissions, signed release |
| Plug-in overreach | Module reads unrelated schedules | Capability manifest, isolated storage, deny-by-default API, registry review |
| AI privacy loss | Image retained by provider | Separate opt-in, metadata stripping, no training, retention contract, delete after inference |
| Account enumeration | Login reveals participant accounts | Uniform responses, rate limits, passkeys, abuse monitoring |
| Denial of service | API outage blocks morning plan | Local-first plan generation and cached inputs |

## Authentication and authorization

- Device-only mode uses platform device security and an optional app PIN/biometric convenience gate.
- Hosted accounts prefer passkeys; email magic links are a recoverable fallback.
- Supporter web sessions use phishing-resistant MFA where available.
- API authorization evaluates participant, relationship, capability, entity, purpose, and grant status.
- Never infer permission from family relationship, shared email domain, device ownership, or calendar access.
- Reauthentication is required to add a supporter, broaden access, export all data, or delete cloud data.

## Cryptography and secrets

- TLS 1.2+ in transit; modern managed defaults and rotation.
- Encrypt cloud data and backups at rest; use application-level envelope encryption for highly sensitive fields when the operational model supports safe recovery.
- Store local database keys in iOS Keychain or Android Keystore, not AsyncStorage.
- Use Azure managed identities and Key Vault. CI uses GitHub OIDC, not long-lived deployment secrets.
- Passwords, tokens, keys, precise schedules, and raw note text never enter analytics or application logs.

## Secure engineering

- Threat-model changes that add data categories, providers, supporter powers, or plug-in capabilities.
- Validate all external input against versioned schemas and size limits.
- Use parameterized SQL, output encoding, CSRF protection for cookie flows, strict CORS, and Content Security Policy.
- Generate an SBOM, scan dependencies and containers, sign releases, and publish checksums.
- Protect branches, require reviewed pull requests, pin GitHub Actions to immutable revisions, and restrict workflow permissions.
- Use synthetic fixtures in tests and demos. Never copy production records.

## Incident priorities

A participant losing control of supporter access, private schedule/location exposure, or incorrect cross-participant data access is critical. The response process must support rapid token revocation, relationship suspension, participant notification in plain language, audit preservation, and transparent remediation.

## Safety boundaries

Wayfinder is not a medical device, emergency service, substitute decision-maker, or source of severe-weather safety instructions. Provider severe-weather notices link to authoritative local guidance and remain visually distinct from routine outfit advice.
