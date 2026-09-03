# Product Foundation

## Product vision

Project Wayfinder is a Personal Independence Operating System for the Neurodiverse. It reduces avoidable executive-function load and helps a person complete practical daily activities with greater confidence and less prompting.

The first promise is intentionally small:

> Open Wayfinder in the morning and understand what today looks like, what to wear, what to bring, and what to expect.

## Product principles

1. **Independence before engagement.** Optimize for completed real-world activities, not screen time.
2. **Presume competence.** Use adult-respectful language, imagery, and choices.
3. **Nothing about me without me.** Co-design and test with neurodiverse adults.
4. **Support without surveillance.** Supporter access is granular, visible, logged, and revocable.
5. **Predictable before clever.** Stable layouts and explainable rules beat novelty.
6. **Personalizable, not "one accessible mode."** People choose language, visuals, density, pacing, sensory settings, and help level.
7. **Local first.** Core morning readiness works offline and without an account.
8. **AI is optional assistance.** AI may reduce setup effort; it never becomes a prerequisite or hidden decision-maker.
9. **Safety through graceful uncertainty.** Ask or show "not sure" rather than inventing an answer.
10. **Practical value over scope.** Reject work that does not improve the independence outcome.

## User personas

Personas describe needs, not diagnoses.

| Persona | Context and goals | Needs | Risks to avoid |
| --- | --- | --- | --- |
| **Jordan, independent adult** | Lives with light family support and wants fewer morning prompts | Fast visual plan, concrete language, routine, control over supporter access | Childlike tone, hidden monitoring, too many choices |
| **Maya, variable-energy adult** | Manages ADHD, sensory preferences, and inconsistent executive function | Flexible reminders, low-friction capture, sensory-aware clothing, recovery from missed steps | Shame, streak pressure, noisy notifications |
| **Sam, emerging-independent adult** | Practices daily living skills with a supporter | Guided choices, pictures, repetition, gradual fading of prompts | Supporter taking over, abrupt removal of help |
| **Riley, family supporter** | Helps prepare activities and wardrobe data | Delegated editing, clear status, rapid corrections | Becoming the product's primary user, overbroad access |
| **Alex, professional supporter** | Works with several people under explicit consent | Separate relationships, auditability, bounded notes | Clinical records creep, cross-person data leakage |
| **Taylor, community contributor** | Builds accessible modules or translations | Clear contracts, test fixtures, governance, accessible contribution path | Architecture complexity, inaccessible review process |

## Jobs to be done

- When I wake up, help me see a calm summary of today so I can start without asking someone what to do.
- When weather or plans change, tell me only what changed and what action I should take.
- When I choose clothes, show options that are available, weather-suitable, activity-suitable, and sensory-compatible.
- When I leave home, help me remember required items without making me scan a long list.
- When I need support, let me ask a trusted person without giving up control of my plan.
- When I need less help over time, allow prompts to fade gradually.

## MVP user stories and acceptance outcomes

### Morning plan

- As a participant, I can open directly to today's plan without navigating a dashboard.
- I can understand each section using text plus optional icons or photos.
- I can see data freshness and the source of a recommendation.
- I can mark a section done, choose another option, or ask for help.
- If data is missing, Wayfinder says what is missing and offers a safe next action.

### Activities and weather

- I can add an activity using a short form with title, time, location, and bring-items.
- I can optionally import device-calendar events after granting permission.
- I can see current conditions, high/low temperature, precipitation, and notable changes.
- Weather unavailability does not prevent me from seeing activities and saved wardrobe guidance.

### Digital wardrobe

- I can photograph or select a photo of clothing and confirm the suggested category.
- I can record category, warmth, rain suitability, formality, sensory tags, and preferred combinations.
- I can mark an item available, in laundry, wet, damaged, or unavailable.
- Recommendations exclude unavailable items and explain each choice in plain language.
- I can save an outfit template and choose it again.

### Support circle

- I invite a supporter and choose exactly what they can view or change.
- I can see supporter changes in an understandable activity history.
- I can revoke access at any time.
- A supporter can add an activity or note only when granted that capability.
- A supporter cannot silently change accessibility, privacy, or consent settings.

### Personalization

- I can choose text size, reading level, icon style, density, contrast, motion, audio, and prompt level.
- A preview shows the effect before applying a change.
- Settings follow me only when optional sync is enabled.

## MVP scope

### Must have

| Capability | Outcome |
| --- | --- |
| Today screen | One calm, complete morning plan |
| Manual activities | Useful without external integrations |
| Weather adapter and cache | Clothing and bring-list weather context |
| Wardrobe capture and editing | Personal, recognizable clothing choices |
| Availability and laundry state | Recommendations reflect reality |
| Rule-based readiness engine | Predictable, explainable output |
| Accessibility profile and preview | Experience adapts to the person |
| Local encrypted storage | Offline, private core experience |
| Optional supporter delegation | Assistance without loss of agency |
| Plan feedback | User can correct recommendations |
| Export/delete data | User controls personal information |

### Should have if capacity permits

- Device-calendar read-only import.
- Optional encrypted cloud sync.
- Multiple visual themes and community-translatable icon packs.
- Gentle change alerts when weather or activities materially change.
- Supporter web PWA.

### Explicitly later

- Dynamic plug-in installation.
- Open-ended generative assistant.
- Automatic purchasing or fashion scoring.
- Location tracking, geofencing, or background surveillance.
- Clinical assessment, diagnosis, treatment recommendations, or behavior scoring.
- School, employer, insurer, or service-provider reporting.
- Public profiles, leaderboards, streaks, or social feeds.

## Prioritized product backlog

| ID | Priority | Epic | Backlog item | Independence test |
| --- | --- | --- | --- | --- |
| WF-001 | P0 | Co-design | Recruit a paid advisory group of neurodiverse adults | Decisions reflect lived experience |
| WF-002 | P0 | Research | Baseline morning comprehension, confidence, and prompt count | Measures actual independence change |
| WF-010 | P0 | Plan | Render today's five-section plan | Person immediately understands today |
| WF-011 | P0 | Plan | Complete, swap, and ask-for-help actions | Person can act and recover independently |
| WF-012 | P0 | Plan | Explain why each recommendation appears | Reduces uncertainty and builds trust |
| WF-020 | P0 | Activities | Create/edit daily activities and bring-items | Plan works without integrations |
| WF-021 | P1 | Activities | Read-only device-calendar connector | Reduces duplicate setup |
| WF-030 | P0 | Weather | Provider adapter, cache, and stale-state UI | Weather informs preparation without fragility |
| WF-040 | P0 | Wardrobe | Capture photo and confirm attributes | Builds usable personal wardrobe |
| WF-041 | P0 | Wardrobe | Availability and laundry state | Avoids impossible recommendations |
| WF-042 | P0 | Wardrobe | Saved outfit templates | Reduces repeated decisions |
| WF-050 | P0 | Engine | Rules for weather, activity, sensory, and availability | Produces practical outfit and bring guidance |
| WF-051 | P0 | Engine | Conflict and uncertainty explanations | Avoids hidden or invented decisions |
| WF-060 | P0 | Accessibility | Personalization profile and preview | Person controls cognitive and sensory load |
| WF-061 | P0 | Accessibility | Screen-reader and switch-control paths | Core task works beyond visual interaction |
| WF-070 | P0 | Privacy | Local encryption, export, and deletion | Person retains data control |
| WF-071 | P1 | Support | Invite, permission, audit, and revoke supporter | Support increases agency |
| WF-080 | P1 | Sync | Optional encrypted change synchronization | Multi-device use without cloud dependency |
| WF-090 | P0 | Quality | Automated accessibility and rule-engine tests | Critical behavior remains dependable |
| WF-100 | P1 | Community | Translation and content-pack workflow | Community can extend reach safely |

## 90-day implementation roadmap

### Days 1-14: Evidence and foundations

- Form a compensated advisory group with varied communication, sensory, reading, motor, and support needs.
- Conduct task-based research using paper and clickable prototypes.
- Record baseline measures: plan comprehension, time to start, prompts needed, confidence, and distress signals.
- Establish governance, accessibility definition of done, threat model, design tokens, domain language, and architectural decisions.
- Prototype the Today screen and wardrobe capture on representative mobile devices.

**Exit:** five or more adult advisors can explain the prototype's four key answers without coaching; major language and sensory risks are documented.

### Days 15-42: Offline vertical slice

- Implement local profile, activities, wardrobe, weather cache, recommendation rules, and Today screen.
- Implement alternate outfit selection, missing-data recovery, and recommendation explanations.
- Add local encryption, consent records, data export/delete, telemetry opt-in, and accessibility settings.
- Test with screen readers, large text, reduced motion, high contrast, keyboard/switch paths, poor connectivity, and low-end devices.

**Exit:** a participant can prepare for a scripted day entirely offline after weather is cached.

### Days 43-70: Real-life pilot

- Add calendar import behind explicit permission.
- Add supporter delegation, audit history, and revocation.
- Add optional sync service and conflict-safe change log.
- Pilot with 8-12 participant/supporter pairs for two weeks.
- Fix comprehension failures before adding features.

**Exit:** at least 80% of pilot mornings communicate all four key answers correctly, with no critical accessibility or privacy defects.

### Days 71-90: Open-source alpha

- Publish reproducible development setup, API/schema contracts, contributor guide, good-first issues, roadmap, and release process.
- Complete independent accessibility review and privacy/security review.
- Add translation workflow and two sample locales.
- Package alpha builds, migration tests, backup/restore, incident process, and community feedback channels.

**Exit:** alpha is installable from documented steps, core flows pass the accessibility definition of done, and pilot evidence supports continued development.

## Success criteria

### Primary outcomes

Measure within the same person over time; do not compare people competitively.

| Measure | MVP target |
| --- | --- |
| Four-answer comprehension | At least 80% of mornings: participant correctly identifies today, outfit, bring-items, and expectations |
| Prompt reduction | At least 25% fewer supporter prompts from the participant's baseline |
| Independent start | At least 20% improvement in mornings started without direct supporter intervention |
| Confidence | Participant-selected confidence improves by at least 1 point on a 5-point visual scale |
| Recommendation usefulness | At least 75% of suggested outfits accepted or changed with an understandable reason |

### Guardrail measures

- No critical WCAG 2.2 AA failure in a core flow.
- No unresolved high-severity privacy or security finding at release.
- Fewer than 1% of plans contain a recommendation using an unavailable wardrobe item.
- Zero required analytics, advertising identifiers, location tracking, or data sale.
- Supporter access changes are always visible to the participant.
- App remains useful when cloud sync, AI, calendar, or weather is unavailable.

### Research ethics

Participation is voluntary and compensated. Consent is understandable and renewable. A supporter cannot consent on behalf of an adult who can provide or communicate consent with appropriate accommodations. Do not infer anxiety, emotion, diagnosis, or capability from usage data.
