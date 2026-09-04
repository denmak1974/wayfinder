# Engineering and Documentation Standards

## Repository model

Start as a monorepo. Shared contracts, accessibility primitives, and domain rules should change atomically with their consumers. Split repositories only when independent release, security, or governance needs are demonstrated.

### Ownership

- `apps/mobile`: Mobile working group.
- `apps/web`: Web and supporter-experience working group.
- `apps/api`: Platform and security working group.
- `packages/domain` and `packages/readiness-engine`: Core maintainers plus accessibility approval.
- `packages/ui`: Accessibility working group approval required.
- `docs/product`: Product council and community advisory group.
- `docs/security`: Security maintainers.

## Coding standards

- TypeScript strict mode; no implicit `any`.
- Domain behavior is pure and deterministic where possible.
- Public functions and APIs use stable domain terms from a maintained glossary.
- Validate data at every external boundary.
- Return typed errors with a user-safe message and a diagnostic code.
- Never silently discard invalid data or substitute a success-shaped default.
- Every database change has forward and rollback/recovery guidance.
- Personal data does not appear in logs, test snapshots, examples, or issue templates.
- Dependencies require a clear purpose, active maintenance, compatible license, and accessibility/security review where relevant.

## Test strategy

| Layer | Required tests |
| --- | --- |
| Domain | Unit and property tests for rules, conflicts, dates, units, and missing data |
| Contracts | JSON Schema/OpenAPI compatibility and migration fixtures |
| Storage | Transaction, migration, encryption, export/delete, and sync-idempotency tests |
| UI | Semantic queries, large text, localization expansion, reduced motion |
| End-to-end | Today, activity, wardrobe, supporter grant/revoke, offline recovery |
| Non-functional | Accessibility manual matrix, low-end performance, security abuse cases |

Tests use synthetic personas and dates. Snapshot tests cannot be the only assertion for accessibility or recommendation behavior.

## Pull-request standard

A pull request states:

1. the independence outcome it improves;
2. user-visible behavior and screenshots in relevant accessibility modes;
3. privacy, security, and data changes;
4. accessibility evidence;
5. tests and failure-mode behavior;
6. migration and rollback impact; and
7. whether advisory-group review is required.

At least one code owner reviews each change. Core accessibility, consent, supporter authorization, cryptography, schema, and release changes require a specialist reviewer.

## Documentation standard

- Write for the intended reader and put the outcome first.
- Use plain language, short sections, descriptive headings, and examples with synthetic data.
- Define acronyms on first use.
- Add alt text and a text equivalent for every diagram.
- Record major decisions as Architecture Decision Records (ADRs): context, decision, alternatives, consequences, and review date.
- Version public API, schema, module, and export documentation.
- Treat docs and translations as tested release artifacts.

## Internationalization

- No user-facing strings in application code.
- Use locale-aware date, time, number, temperature, and measurement formatting.
- Do not concatenate sentence fragments.
- Use stable message keys and ICU MessageFormat for complete, plural-aware messages.
- Keep source-controlled activity titles and proper names unchanged unless an approved translation is supplied.
- Keep interface, document, calendar, and speech locales as separate values.
- Support right-to-left layout and at least 40% text expansion.
- Separate translations from clinical or culturally specific assumptions.
- Community locale packs require reviewer provenance and accessibility checks.

See [Localization Architecture](../design/LOCALIZATION.md) for the initial `en-CA`, `ja-JP`, and `fr-CA` requirements.

## Issue taxonomy

- `outcome:*`: readiness, wardrobe, support-circle, accessibility, platform.
- `type:*`: bug, feature, research, documentation, security.
- `priority:*`: p0-p3.
- `good first issue`: bounded, documented, non-sensitive.
- `needs lived-experience review`: changes language or participant interaction.
- `accessibility blocker`: blocks a core flow.

## Release standard

- Semantic versioning before 1.0 with documented breaking changes.
- Signed tags and artifacts, checksums, SBOM, provenance, and reproducible instructions.
- Human-readable release notes: what changed, who benefits, data/accessibility impact, and upgrade steps.
- Staged rollout with rollback criteria.
- No release with a known accessibility blocker, critical privacy issue, or failed migration/restore test.
