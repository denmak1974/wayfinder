# Data Model

## Ownership rules

- `Participant` owns their profile, plan, wardrobe, activities, and consent.
- A `SupportRelationship` delegates capabilities; it does not transfer ownership.
- Every supporter mutation records actor, source, time, and affected fields.
- Images are separate objects with independent retention and sync consent.
- Sensitive free text is minimized. Structured attributes are preferred.

## Core entity model

```mermaid
erDiagram
  PARTICIPANT ||--|| ACCESSIBILITY_PROFILE : configures
  PARTICIPANT ||--o{ DEVICE : uses
  PARTICIPANT ||--o{ SUPPORT_RELATIONSHIP : grants
  PARTICIPANT ||--o{ ACTIVITY : plans
  PARTICIPANT ||--o{ WARDROBE_ITEM : owns
  WARDROBE_ITEM ||--o{ WARDROBE_STATE_EVENT : changes
  PARTICIPANT ||--o{ OUTFIT_TEMPLATE : saves
  OUTFIT_TEMPLATE }o--o{ WARDROBE_ITEM : contains
  PARTICIPANT ||--o{ READINESS_PLAN : receives
  READINESS_PLAN ||--o{ PLAN_SECTION : contains
  READINESS_PLAN }o--o{ ACTIVITY : summarizes
  READINESS_PLAN ||--o{ BRING_ITEM : includes
  READINESS_PLAN ||--|| INPUT_SNAPSHOT : explains
  PARTICIPANT ||--o{ CONSENT_GRANT : controls
  DEVICE ||--o{ SYNC_OPERATION : emits
  PARTICIPANT ||--o{ AUDIT_EVENT : can_view
```

## Entity catalog

### Participant

`id`, preferred name, locale, timezone, unit system, local-only/account-linked state, created/updated timestamps.

Do not store diagnosis as a required or default field. Functional preferences belong in the accessibility profile.

### AccessibilityProfile

`participantId`, reading level, text scale, information density, icon mode, photo mode, contrast theme, reduced motion, audio preference, input method, prompt level, transition warning, confirmation style, color-use preference.

### SupportRelationship

`id`, participant ID, supporter ID, status, granted capabilities, start/end, last reviewed, created by participant, revoked timestamp.

Capability examples: `activity.read`, `activity.write`, `wardrobe.read`, `wardrobe.state.write`, `plan.read`, `note.write`. Consent and accessibility writes are never delegable in the MVP.

### Activity

`id`, participant ID, source, external source ID, title, controlled description, start/end, all-day, location label, preparation minutes, bring-items, clothing requirements, sensory notes, status, provenance.

### WardrobeItem

`id`, participant ID, local image reference, optional synced object reference, category, layer, warmth, rain suitability, activity suitability, sensory tags, color label, user label, favorite, classifier suggestion metadata, archived timestamp.

### WardrobeStateEvent

Append-only event: `itemId`, state (`available`, `laundry`, `wet`, `damaged`, `unavailable`), effective time, actor, note. Current state is a projection.

### OutfitTemplate

`id`, participant ID, name, item IDs, applicable weather bands, applicable activity types, sensory context, preference rank, last accepted.

### WeatherSnapshot

`id`, geospatial area at coarse precision, provider, observed/forecast times, temperature, apparent temperature, precipitation probability/type, wind, severe-weather flag, fetched time, expiry time. Exact location is not retained by default.

### ReadinessPlan

`id`, participant ID, local date, status, ruleset version, generated time, weather freshness, sections, input snapshot hash, participant feedback.

### PlanSection

`id`, plan ID, type (`weather`, `activities`, `outfit`, `bring`, `notes`), display order, summary, visual references, explanation, completion state, source.

### ConsentGrant

`id`, participant ID, purpose, data categories, recipient/service, status, version, granted/revoked time, expiry. Consent is purpose-specific; a single broad consent flag is prohibited.

### SyncOperation

`operationId`, device ID, entity type/ID, action, base version, payload, payload hash, local time, server cursor, applied time.

### AuditEvent

`id`, participant ID, actor, action, entity type/ID, changed fields, timestamp, device/source. Never include access tokens, raw image bytes, or unnecessary note content.

## Data classification

| Class | Examples | Controls |
| --- | --- | --- |
| Public | Documentation, code, generic icon packs | Integrity and provenance |
| Personal | Preferences, wardrobe metadata, activities | Encryption, access control, minimization |
| Highly sensitive | Support relationships, free-text notes, precise schedule/location | Stronger audit, short retention, no analytics |
| Secret | Tokens, encryption keys | Platform keystore/Key Vault only; never database logs |

## Retention defaults

- Local personal data: until user deletion or profile reset.
- Cloud synchronized domain data: until sync disabled and cloud copy deleted, subject to a short recovery window disclosed to the user.
- Deleted object tombstones: 30 days or until all active devices acknowledge deletion.
- Security audit events: 90 days by default; configurable for self-hosting.
- Operational logs: 30 days, with personal fields removed.
- AI transient images: deleted immediately after inference; not retained for training.

## Portable export

Export a ZIP containing versioned JSON, user-owned images, manifest, checksums, and human-readable HTML. Export must not include secrets, supporter contact details beyond what the participant can already view, or server-only abuse-prevention signals.
