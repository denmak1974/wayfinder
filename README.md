# Wayfinder

> Building independence one successful day at a time.

Wayfinder is an open-source Personal Independence Operating System for the Neurodiverse.

Its purpose is to help neurodiverse individuals build greater independence, confidence, executive functioning, life skills, and self-determination through practical, accessible technology.

The focus is not disability.

The focus is capability.

The focus is helping individuals navigate everyday life with greater confidence and less dependence on others.

---

## Why Wayfinder Exists

Wayfinder began with a simple question:

> How can technology help a neurodiverse adult become more independent?

Many daily activities that neurotypical individuals perform automatically involve dozens of small decisions:

- What should I wear today?
- Do I need a jacket?
- What is the weather?
- What should I bring?
- What activities do I have planned?
- What should I expect today?

For individuals with executive-function challenges, these seemingly simple decisions can create unnecessary stress, confusion, and dependence.

Wayfinder aims to reduce that friction.

Not by replacing caregivers or the people connection.

But by providing practical tools that help individuals successfully navigate everyday life and build connections.

---

## Our Belief

We believe that independence is built through small victories.

A successful morning.

A successful trip.

A successful conversation.

A successful day.

These moments compound over time and can lead to greater confidence, capability, and self-determination.

Wayfinder exists to support those moments.

---

## The First Capability: Daily Readiness

The first Wayfinder module is the **Daily Readiness Assistant**.

Its mission is simple:

> Help a neurodiverse adult successfully start each day.

The assistant combines information such as:

- Weather
- Daily schedule
- Activities
- Clothing availability
- Personal preferences
- Support requirements

to provide a simple daily plan.

Example:

### Good Morning

**Weather**
- 12°C
- Rain expected this afternoon

**Today's Activities**
- Dentist at 10:00 AM
- Grocery shopping at 2:00 PM

**What to Wear**
- Blue jeans
- Grey shirt
- Waterproof jacket
- Running shoes

**Don't Forget**
- Umbrella
- Health card

The goal is not fashion advice.

The goal is helping someone get ready successfully.

---

## Long-Term Vision

Wayfinder is designed as an extensible platform.

Future capabilities may include:

- Reading Coach
- Writing Coach
- Math Coach
- Daily Living Skills
- Transportation Assistant
- Social Skills Coach
- Employment Readiness
- Household Management
- Visual Scheduling
- Executive Function Support

Every capability should support a common objective:

> Helping neurodiverse individuals build greater independence.

---

## Open Source First

Wayfinder is intended to be developed openly and collaboratively.

We welcome contributions from:

- Neurodiverse individuals
- Families
- Caregivers
- Educators
- Therapists
- Researchers
- Designers
- Developers
- Accessibility advocates

Technology alone cannot solve these challenges.

The best solutions will come from people who live them every day.

---

## Project Foundation

The initial product and engineering foundation is now available:

| Area | Document |
| --- | --- |
| Product vision, personas, stories, backlog, and 90-day roadmap | [Product foundation](docs/product/PRODUCT.md) |
| Location schedule import, preferred calendars, and future email agent | [Weekly schedule import](docs/product/WEEKLY_SCHEDULE_IMPORT.md) |
| Draft temperature bands and weather-driven clothing rules | [Weather and clothing rules](docs/product/WEATHER_CLOTHING_RULES.md) |
| Solution architecture, technology stack, Azure, local-first, mobile, and AI | [Solution architecture](docs/architecture/ARCHITECTURE.md) |
| Domain entities and data ownership | [Data model](docs/architecture/DATA_MODEL.md) |
| Barcode, tag OCR, and garment recognition options | [Capture technology](docs/architecture/CAPTURE_TECHNOLOGY.md) |
| API contract | [OpenAPI](openapi/wayfinder-v1.yaml) |
| Accessibility requirements | [Accessibility architecture](docs/design/ACCESSIBILITY.md) |
| English, Japanese, and Canadian French behavior | [Localization architecture](docs/design/LOCALIZATION.md) |
| Privacy and threat model | [Privacy and security](docs/security/PRIVACY-THREAT-MODEL.md) |
| Engineering and documentation standards | [Engineering standards](docs/community/STANDARDS.md) |
| Governance | [GOVERNANCE.md](GOVERNANCE.md) |

Editable architecture diagrams are in [`docs/diagrams`](docs/diagrams). They can be opened with [Microsoft Excalidraw](https://aka.ms/excalidraw).

### Interactive prototype

Open the self-contained [Daily Readiness Assistant prototype](prototypes/daily-readiness.html). It uses the Doug Hub example and demonstrates:

- the calm five-section Today screen;
- a selectable plan day for previewing tomorrow's clothing the previous evening;
- participant-filtered weekly schedule review;
- a second imported Hub schedule example from the Sep. 8 screenshot;
- the familiar Hub morning/activity and afternoon/activity quadrant;
- Low, High, rain timing, and explainable clothing changes;
- Outlook, Google, device, Wayfinder, or ICS destination selection;
- activity-aware clothing recommendations;
- two sensory-safe outfit choices and a participant-initiated "Finished, please check" handoff;
- live English, Japanese, and Canadian French switching with localized dates and speech;
- outfit alternatives with plain-language explanations;
- bring-item tracking;
- display personalization; and
- a bounded help flow that keeps the participant in control.

The normalized, privacy-minimized Doug example is available as [JSON](examples/doug-hub-week-2026-08-31.json).

#### What is real and what is simulated

The prototype is a design artifact, not a working application. Some parts run for real and some are deliberately stubbed, so it is worth being explicit before anyone builds on it.

| Behaviour | Status |
| --- | --- |
| Weather forecast | **Real.** Live daily and hourly data from the public Open-Meteo API for the selected date. |
| Outfit recommendations | **Real.** Computed from the forecast, the activity context, and the wardrobe by the rules in [Weather and clothing rules](docs/product/WEATHER_CLOTHING_RULES.md). |
| Wardrobe add, edit, remove | **Real.** Stored in browser local storage and used immediately by the recommendation engine. |
| Barcode and QR scanning | **Simulated.** The button returns a fixed example so the confirmation flow can be evaluated. No scanner is wired up. |
| Reading a clothing tag (OCR) | **Simulated.** Photographing a tag returns fixed example text. No text recognition runs. |
| Classifying a garment from its photo | **Simulated.** A filename keyword check stands in for image classification, and it deliberately reports low confidence rather than guessing. |
| Schedule import | **Simulated.** Two prepared examples stand in for parsing an uploaded image or PDF. |
| Weekly schedule photographs and wardrobe photographs | Held outside this repository. The prototype references them by relative path, so anyone else sees text labels instead of images. |

Barcode scanning, OCR, and on-device garment classification are the three capabilities that need real implementations. They should run on the device without uploading a participant's clothing photographs to a third-party service. Candidate libraries have been researched and recorded in [Capture technology](docs/architecture/CAPTURE_TECHNOLOGY.md); nothing has been installed yet.

---

## Guiding Principle

Every proposed feature should answer a single question:

> Does this help a neurodiverse person become more independent?

If the answer is no, it probably does not belong in Wayfinder.

---

## Current Status

Project Status: Early Foundation

Current focus:

- Validate the MVP with neurodiverse adults
- Build Daily Readiness Assistant
- Implement the offline vertical slice
- Establish the first community advisory group

---

## Contributing

Wayfinder is in its foundation stage.

If this mission resonates with you, we would love your ideas, feedback, and future contributions.

Read [CONTRIBUTING.md](CONTRIBUTING.md), the [Code of Conduct](CODE_OF_CONDUCT.md), and the [accessibility reporting guide](ACCESSIBILITY.md) before contributing.

---

## Final Thought

Wayfinder is not about technology.

Technology is simply a tool.

Wayfinder is about helping people build confidence, capability, and independence one successful day at a time.
