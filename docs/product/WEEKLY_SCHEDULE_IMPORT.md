# Weekly Schedule Import

## Independence outcome

A participant should not need to interpret a crowded location schedule, find their name repeatedly, copy activities into a calendar, and determine what each activity means for clothing.

Wayfinder turns a location-provided weekly schedule into:

1. the participant's own clear weekly activities;
2. approved events in their preferred calendar;
3. activity context for Daily Readiness; and
4. explainable clothing and bring-item requirements.

The participant remains the owner of the resulting schedule even when a supporter or location supplies the source.

## Preserve a familiar schedule pattern

When a participant already understands a location's schedule format, Wayfinder should preserve that visual grammar after filtering it to the participant.

For Doug's Today view, use the same stable two-by-two pattern every day:

| Morning | Morning activity |
| --- | --- |
| Afternoon | Afternoon activity |

This is a four-quadrant reading experience: the period remains in the left cell and the recognizable source activity remains in the right cell. Wayfinder may add a short translated context line, but it must not turn the familiar schedule into an unrelated timeline, agenda list, carousel, or conversational summary.

If a day has multiple activities in one period, keep them within that period's activity cell in source order. If the source uses a full-day activity, show a clearly labelled full-day row rather than manufacturing morning and afternoon duplicates.

## Doug example

The supplied Hub schedule is a visual table containing activities for many people. Wayfinder filters it to rows where **Doug** is named.

| Day | Period | Doug's activity | Clothing context |
| --- | --- | --- | --- |
| Monday, August 31 | Morning | Summer lake messages | Outdoor possibility; confirm activity details |
| Monday, August 31 | Afternoon | August hand weight challenge | Active; breathable clothing and supportive shoes |
| Tuesday, September 1 | Morning | Frosty Tuesday | Indoor/social; standard comfortable clothing |
| Tuesday, September 1 | Afternoon | 2000 Steps into September | Active walking; breathable layers and walking shoes |
| Wednesday, September 2 | Morning | BU Cafe visit | Community outing; comfortable casual clothing |
| Wednesday, September 2 | Afternoon | August Hand Weight Challenge | Active; breathable clothing and supportive shoes |
| Thursday, September 3 | Morning | Film.ca Scoob movie morning | Indoor seated activity; comfortable layer |
| Thursday, September 3 | Afternoon | Trafalgar Park | Outdoor walking; weather layer and walking shoes |
| Friday, September 4 | Full day | Hamilton Bayfront picnic lunch | Outdoor full-day outing; weather protection and walking shoes |

The source provides periods rather than exact start and end times. Wayfinder must preserve that uncertainty and request a location-specific period mapping or show `Morning`, `Afternoon`, or `Full day`. It must not invent exact times.

## Supported source formats

### MVP

- phone photo or screenshot;
- PDF;
- image-based email attachment saved by the user;
- CSV, XLSX, or ICS supplied by the location; and
- manual entry when extraction is not reliable.

### Preferred source order

Use structured data before optical character recognition:

1. ICS calendar feed;
2. CSV or XLSX template;
3. accessible PDF with selectable text;
4. image or scanned PDF; and
5. manual entry.

Locations receive a documented template with date, period/start/end, activity, participant identifier, location, clothing context, bring-items, and update/cancellation fields.

## MVP flow: import, review, publish

1. **Choose source.** Participant or authorized supporter selects the location and uploads a schedule.
2. **Choose identity.** Wayfinder uses the participant's approved matching names or location-specific participant ID. Fuzzy name matching is never silently accepted.
3. **Extract privately.** The importer detects table boundaries, dates, activity titles, periods, and participant lists.
4. **Minimize immediately.** Non-matching participant names and activities are discarded after extraction. They are not added to Doug's profile or logs.
5. **Normalize.** Dates and periods are converted using the selected location's schedule profile.
6. **Classify activity context.** Deterministic rules suggest indoor/outdoor, activity level, water exposure, formality, temperature exposure, footwear, layers, and bring-items.
7. **Review exceptions.** The user confirms ambiguous names, uncertain text, missing times, duplicates, cancellations, and clothing requirements.
8. **Publish once.** Approved activities are written to Wayfinder and, if selected, Outlook, Google Calendar, or an ICS file.
9. **Generate readiness.** Weather, activity context, sensory needs, wardrobe availability, and travel combine into the daily outfit and bring-list.
10. **Render familiarly.** The participant's Today view preserves the approved location schedule pattern.

The review presents only Doug's extracted events. It does not reproduce the full multi-person schedule.

## Calendar destination

Each participant selects one preferred destination:

- Wayfinder only;
- Outlook Calendar;
- Google Calendar;
- device calendar; or
- downloadable/subscribable ICS.

Calendar publishing is optional and separately authorized. Wayfinder stores the external event ID, calendar ID, source fingerprint, and last-published version so an updated schedule changes the existing event instead of creating duplicates.

Each published event contains:

- activity title;
- exact time or honest period label;
- location when supplied;
- preparation and departure guidance;
- participant-approved bring-items;
- short clothing context where helpful; and
- source and last-updated provenance.

Other participants' names are never included.

## Clothing-context model

The schedule does not directly choose an outfit. It contributes constraints to the readiness engine.

| Context | Example activity | Recommendation effect |
| --- | --- | --- |
| `activeWalking` | 2000 Steps, Trafalgar Park | Supportive shoes, breathable layer |
| `activeExercise` | Hand weight challenge | Stretch-friendly clothing, secure footwear |
| `outdoorExtended` | Hamilton Bayfront full day | Weather protection, spare layer, sun/rain items |
| `indoorSeated` | Movie | Comfortable layer; account for indoor temperature |
| `communityCasual` | Cafe visit | Comfortable casual outfit |
| `waterActivity` | Pool | Swimwear, change of clothes, towel |
| `unknown` | Ambiguous activity name | Do not guess; use neutral defaults and request clarification |

Weather and sensory preferences can strengthen or remove choices, but never override explicit participant exclusions.

## Future flow: email Scheduling Agents

A participant may enable a dedicated address such as:

```text
schedule+<opaque-id>@inbound.projectwayfinder.org
```

The address contains no participant name. The participant or authorized supporter gives it only to approved locations.

### Automatic processing policy

Automatic, no-touch processing is allowed only when the participant has explicitly enabled it for a specific location and destination. A policy includes:

- trusted sender addresses and domains;
- accepted attachment types;
- expected participant identifier;
- expected schedule format or template version;
- period-to-time mappings;
- preferred calendar destination;
- whether new events, changes, and cancellations may auto-publish;
- confidence thresholds; and
- notification preference.

The agent:

1. verifies email authentication and the trusted-sender policy;
2. scans attachments and strips active content;
3. extracts only the intended participant's rows;
4. checks confidence, dates, duplicates, and unexpected format changes;
5. classifies activity and clothing context;
6. updates Wayfinder and the preferred calendar idempotently;
7. sends a plain-language summary to the participant; and
8. quarantines exceptions instead of guessing.

No human intervention is required for a high-confidence message that matches an active policy. Human review remains required when:

- the sender is new or authentication fails;
- the source format changed materially;
- the participant match is ambiguous;
- dates or periods cannot be resolved;
- an update would delete or move a previously accepted event unexpectedly;
- malware or active content is detected; or
- the confidence threshold is not met.

The participant can pause the agent, revoke a sender, undo an import, change the destination, or require review again at any time.

## Notifications

Default notifications are calm and summary-first:

> Doug's Hub schedule for September 7-11 was added. Five days and nine activities were updated. One activity needs a time.

Do not expose other participants' names or the original multi-person schedule in notifications.

## Acceptance criteria

- Doug's extracted schedule contains only activities where Doug is explicitly associated.
- No exact time is invented from a morning or afternoon label.
- The user can correct every extracted field before MVP publication.
- Re-importing the same source produces no duplicate events.
- A changed or cancelled source event updates its prior calendar event.
- Every outfit explanation identifies both weather and relevant activity constraints.
- Calendar access can be revoked without disabling local readiness.
- The original multi-person source follows a short, disclosed retention policy.
- Future automatic processing operates only under an explicit location-specific policy and produces an auditable result.
