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
| **Doug, primary fit persona** | Adult living with family support. Independently completes most morning and household routines, sometimes with a prompt. Adept with an iPad. Clothing selection tends to repeat the previous day's pattern unless guidance is clear. | Short readable instructions paired with his own clothing photos; optional spoken prompts; exactly two acceptable choices when a change is needed; cotton against skin and tag-free garments; a participant-initiated **"Finished, please check"** handoff | Childlike tone; treating limited speech as limited understanding or consent; too many choices; abrupt correction; hidden family control; recommending a sensory-incompatible item |
| **Maya, variable-energy adult** | Manages ADHD, sensory preferences, and inconsistent executive function | Flexible reminders, low-friction capture, sensory-aware clothing, recovery from missed steps | Shame, streak pressure, noisy notifications |
| **Riley, family checker** | Helps configure wardrobe and schedule information, remains available when Doug asks, and performs a final check after Doug says he is finished | A bounded review request, the reason for a recommendation, ability to flag safety or missing information, and no need to redo completed steps | Becoming the product's primary user; routine approval gates; overriding an acceptable choice; overbroad access |
| **Alex, professional supporter** | Works with several people under explicit consent | Separate relationships, auditability, bounded notes | Clinical records creep, cross-person data leakage |
| **Taylor, community contributor** | Builds accessible modules or translations | Clear contracts, test fixtures, governance, accessible contribution path | Architecture complexity, inaccessible review process |

### Fit-model boundary

Doug is the primary fit model for the first Daily Readiness clothing flow. This means the first release should work exceptionally well for his confirmed functional needs; it does not mean one person's preferences represent all autistic or neurodiverse adults.

The fit model was described through family observation. Product decisions must also be validated with Doug using accessible choice-making, task observation, and his actions or communication as evidence. Wayfinder must not interpret limited speech as agreement, refusal, comprehension, or incapacity.

### Doug-derived interaction requirements

1. **Preserve competence.** Begin with the assumption that Doug will complete the task himself.
2. **Use a stable sequence.** Show weather, activities, two outfit choices, special item exceptions, dressing steps, then the optional check request in the same order.
3. **Make the instruction concrete.** Pair short text with photos of Doug's actual clothing. Spoken playback is available but not required.
4. **Offer two valid choices.** When today's needs differ from yesterday's pattern or a plan changes, show exactly two sensory-safe, weather-safe alternatives.
5. **Respect self-advocacy.** Changing clothes, pointing, or repeating a short phrase may communicate a choice or objection. The interface must provide a visible way to select, reject, or ask for help without requiring a sentence.
6. **Treat sensory rules as constraints.** Garments touching skin must match the configured cotton requirement, and tags must be recorded as removed before recommendation.
7. **Keep checking participant-initiated.** Doug completes the flow, then chooses **"Finished, please check."** Family review does not silently change his selection.
8. **Explain necessary changes.** If neither preferred choice is safe or suitable, say why in one short statement, show two replacements, and make family help available.

## Jobs to be done

- When I wake up, help me see a calm summary of today so I can start without asking someone what to do.
- When weather or plans change, tell me only what changed and what action I should take.
- When I choose clothes, show options that are available, weather-suitable, activity-suitable, and sensory-compatible.
- When today's clothing should differ from yesterday's pattern, show me two acceptable choices instead of only telling me that my choice is wrong.
- When I have made my choice, let me say "Finished, please check" without giving someone else control of the entire routine.
- When I leave home, show only day-specific items or exceptions so I do not scan a list of default items I already take every day.
- When I need support, let me ask a trusted person without giving up control of my plan.
- When I need less help over time, allow prompts to fade gradually.

## MVP user stories and acceptance outcomes

### Morning plan

- As a participant, I can open directly to today's plan without navigating a dashboard.
- I can choose another upcoming day so I can prepare tomorrow's clothing the previous evening.
- I can understand each section using text plus optional icons or photos.
- I can play a short spoken instruction without making audio mandatory.
- I can respond through touch, pointing, changing my selection, or asking for help; speech is never required.
- I can see data freshness and the source of a recommendation.
- I can mark a section done, choose another option, or ask for help.
- If data is missing, Wayfinder says what is missing and offers a safe next action.

### Activities and weather

- I can add an activity using a short form with title, time, location, and special item exceptions.
- I can optionally import device-calendar events after granting permission.
- I or an authorized supporter can upload a location's weekly image, PDF, spreadsheet, or calendar file and review only my extracted activities.
- Approved imported activities appear as selectable plan days so I can preview future clothing and special item exceptions.
- Wayfinder keeps routine default items, such as Hub bag, water bottle, lunch box, and everyday wallet/card items, in a default-item profile instead of repeating them every day.
- Wayfinder parses the schedule for exceptions: swimming adds swim bag, towel, and change of clothes; pizza party or hot-dog day can say no lunch box; grocery list adds the list; rain can add umbrella.
- I can choose Wayfinder, Outlook, Google Calendar, a device calendar, or ICS as my preferred schedule destination.
- If a source says only morning or afternoon, Wayfinder preserves that label rather than inventing a time.
- My activity type contributes explainable clothing, footwear, and special item requirements.
- I can see Low, High, rain timing, and only weather details that change what I should wear or bring.
- When I choose a future day, Wayfinder loads that day's public forecast when available and clearly says when it cannot.
- My daily activities use the familiar Hub morning/activity and afternoon/activity quadrant after unrelated participants are removed.
- Weather unavailability does not prevent me from seeing activities and saved wardrobe guidance.

See [Weekly Schedule Import](WEEKLY_SCHEDULE_IMPORT.md) for the Doug example, review workflow, calendar publication, and future inbound email Scheduling Agent.
See [Weather and Clothing Rules](WEATHER_CLOTHING_RULES.md) for the draft temperature bands, exposure modifiers, and wardrobe-photo validation.

### Digital wardrobe

- I am told what kind of top, bottom, and socks to wear, and I choose which particular ones. Being told which t-shirt is not help; it removes a decision I can make.
- I am told which jacket or coat to wear, and which shoes, because those choices are hard and getting them wrong is uncomfortable or unsafe.
- I can set up quickly, because only jackets, coats, and footwear need a photograph each. A few pictures taken once is enough.
- I can photograph or select one item when I need a clearer card, but individual retakes are not required for initial setup.
- I can reuse a saved clothing card without taking a new photo each time the item appears in an outfit.
- I can record category, warmth, rain suitability, formality, sensory tags, fabric touching skin, tag status, and preferred combinations.
- I can mark an item available, in laundry, wet, damaged, or unavailable.
- Recommendations exclude unavailable items and explain each choice in plain language.
- Recommendations exclude items that violate hard sensory constraints.
- On a day that needs it, I am shown a second outfit to carry in a bag and change into, separately from the things I carry.
- I am told plainly when I do not own something the day needs, rather than being given a substitute that is not safe.
- I can compare exactly two valid outfits when a change from my familiar pattern is needed.
- I can save an outfit template and choose it again.

### Support circle

- I invite a supporter and choose exactly what they can view or change.
- I can see supporter changes in an understandable activity history.
- I can revoke access at any time.
- A supporter can add an activity or note only when granted that capability.
- A supporter cannot silently change accessibility, privacy, or consent settings.
- I can initiate a bounded **"Finished, please check"** request after making my own selections.
- A family checker can confirm the plan or explain a necessary correction without restarting or taking over the routine.

### Personalization

- I can choose text size, reading level, icon style, density, contrast, motion, audio, and prompt level.
- I can switch the interface between English, Japanese, and Canadian French without changing my schedule or choices.
- Proper names and source schedule titles remain recognizable while Wayfinder guidance is translated.
- A preview shows the effect before applying a change.
- Settings follow me only when optional sync is enabled.

## MVP scope

### Must have

| Capability | Outcome |
| --- | --- |
| Today screen | One calm, complete morning plan |
| Manual activities | Useful without external integrations |
| Reviewed weekly schedule import | Converts a complex location schedule into the participant's own plan |
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
- Outlook, Google Calendar, device-calendar, and ICS publication.
- Optional encrypted cloud sync.
- Multiple visual themes and community-translatable icon packs.
- Gentle change alerts when weather or activities materially change.
- Supporter web PWA.

### Explicitly later

- Dynamic plug-in installation.
- Unreviewed inbound email automation until sender policies, exception handling, and audit controls are proven.
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
| WF-010A | P0 | Plan | Select an upcoming plan date | Person can preview tomorrow's activities, weather, outfit, and special item exceptions before the day starts |
| WF-011 | P0 | Plan | Complete, swap, and ask-for-help actions | Person can act and recover independently |
| WF-012 | P0 | Plan | Explain why each recommendation appears | Reduces uncertainty and builds trust |
| WF-020 | P0 | Activities | Create/edit daily activities and special item exceptions | Plan works without integrations |
| WF-021 | P1 | Activities | Read-only device-calendar connector | Reduces duplicate setup |
| WF-022 | P0 | Activities | Import and review a participant's rows from a weekly location schedule | Removes repeated schedule interpretation and copying |
| WF-023 | P1 | Activities | Publish approved activities to the preferred calendar without duplicates | Keeps the person's existing planning system current |
| WF-024 | P1 | Activities | Convert activity context into clothing and bring-item constraints | Prepares the person for what they will actually do |
| WF-025 | P2 | Automation | Receive trusted location schedules through a participant-controlled email agent | Removes recurring supporter administration |
| WF-030 | P0 | Weather | Provider adapter, cache, and stale-state UI | Weather informs preparation without fragility |
| WF-040 | P0 | Wardrobe | Model tops, bottoms, and socks as types, and photograph only jackets, coats, and footwear individually | Builds a usable personal wardrobe from a handful of pictures, and leaves the expressive choices with the participant |
| WF-041 | P0 | Wardrobe | Availability and laundry state | Avoids impossible recommendations |
| WF-042 | P0 | Wardrobe | Saved outfit templates | Reduces repeated decisions |
| WF-043 | P0 | Wardrobe | Enforce fabric-contact and tag-status constraints | Prevents unusable or distressing clothing recommendations |
| WF-044 | P0 | Wardrobe | Present two valid choices when changing a familiar clothing pattern | Supports flexibility without creating excessive choice |
| WF-050 | P0 | Engine | Rules for weather, activity, sensory, and availability | Produces practical outfit and bring guidance |
| WF-051 | P0 | Engine | Conflict and uncertainty explanations | Avoids hidden or invented decisions |
| WF-060 | P0 | Accessibility | Personalization profile and preview | Person controls cognitive and sensory load |
| WF-061 | P0 | Accessibility | Screen-reader and switch-control paths | Core task works beyond visual interaction |
| WF-070 | P0 | Privacy | Local encryption, export, and deletion | Person retains data control |
| WF-071 | P1 | Support | Invite, permission, audit, and revoke supporter | Support increases agency |
| WF-072 | P0 | Support | Participant-initiated "Finished, please check" handoff | Keeps task ownership with the participant |
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
- Pilot reviewed weekly schedule extraction and preferred-calendar publication before enabling automatic inbound agents.
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
| Four-answer comprehension | At least 80% of mornings: participant correctly identifies today, outfit, special items or exceptions, and expectations |
| Prompt reduction | At least 25% fewer supporter prompts from the participant's baseline |
| Independent start | At least 20% improvement in mornings started without direct supporter intervention |
| Confidence | Participant-selected confidence improves by at least 1 point on a 5-point visual scale |
| Recommendation usefulness | At least 75% of suggested outfits accepted or changed with an understandable reason |
| Doug fit-model outcome | Doug understands and follows a Wayfinder clothing recommendation on at least 5 of 7 days in a representative week |

### Guardrail measures

- No critical WCAG 2.2 AA failure in a core flow.
- No unresolved high-severity privacy or security finding at release.
- Fewer than 1% of plans contain a recommendation using an unavailable wardrobe item.
- Zero recommendations violate a configured hard sensory constraint.
- Zero required analytics, advertising identifiers, location tracking, or data sale.
- Supporter access changes are always visible to the participant.
- App remains useful when cloud sync, AI, calendar, or weather is unavailable.

### Research ethics

Participation is voluntary and compensated. Consent is understandable and renewable. A supporter cannot consent on behalf of an adult who can provide or communicate consent with appropriate accommodations. Do not infer anxiety, emotion, diagnosis, or capability from usage data.
