# Accessibility Architecture

Accessibility is a release requirement and a system property, not a final audit.

## Standards baseline

- WCAG 2.2 Level AA for mobile and web core flows.
- WAI-ARIA Authoring Practices for web interaction patterns.
- EN 301 549 where public-sector or European procurement applies.
- Platform guidance for iOS VoiceOver, Android TalkBack, Switch Control, and keyboard access.
- W3C cognitive accessibility guidance as product design input beyond conformance.

Critical morning tasks target enhanced readability and interaction beyond AA where practical.

## Cognitive accessibility contract

1. Show one primary decision or action at a time.
2. Keep the five Today sections in a stable order.
3. Use concrete, literal, adult-respectful language.
4. Pair icons/photos with text; never require interpreting an icon alone.
5. Reveal detail progressively instead of presenting long forms.
6. Preserve context after errors; explain the next action.
7. Preview changes before applying them.
8. Make help available without blocking independent action.
9. Announce meaningful changes and ignore inconsequential refreshes.
10. Let the person choose prompt strength and reduce it gradually.
11. Never equate limited speech with limited comprehension, consent, or decision-making.
12. When a familiar plan must change, present exactly two valid choices before escalating to supporter help.

## Visual and interaction requirements

- Minimum touch target: 48 by 48 density-independent pixels with adequate spacing.
- Support 200% text scaling without loss of content or action.
- Never encode meaning by color, position, sound, or animation alone.
- Provide light, dark, high-contrast, and low-stimulation themes.
- Respect reduced motion and disable non-essential animation.
- Maintain visible focus and logical focus order.
- Use native headings, lists, buttons, toggles, status, and dialog semantics.
- Provide persistent labels; placeholders are examples, not labels.
- Avoid time limits. If unavoidable for security, warn and extend.
- Avoid carousels, drag-only interactions, hidden gestures, autoplay, and toast-only errors.

## Language system

Default content uses:

- common words and short sentences;
- one instruction per sentence;
- active voice;
- specific times and actions;
- positive guidance rather than warnings;
- no idioms, sarcasm, shame, or infantilizing language.

Example:

- Prefer: "Bring your umbrella. Rain may start after lunch."
- Avoid: "Don't get caught out later!"

Controlled message templates are localized as complete phrases, not concatenated fragments. Every locale is reviewed by native speakers and, where possible, neurodiverse reviewers.

## Personalization profile

| Dimension | Example settings |
| --- | --- |
| Reading | concise, standard, detailed; symbol support; text-to-speech |
| Visuals | item photos, neutral icons, text only |
| Density | one card, compact five-section summary |
| Guidance | direct answer, two choices, guided steps |
| Sensory | fabric exclusions, color intensity, sound, haptics, motion |
| Time | analog/digital, relative plus exact time, transition warnings |
| Interaction | touch, keyboard, switch, voice input where supported |
| Confirmation | immediate with undo, explicit confirm, supporter review |

Accessibility preferences are functional data, not diagnostic labels.

## Primary fit-model interaction pattern

The first clothing flow is optimized for an adult who independently completes routines when instructions are precise and predictable.

1. Show one short instruction and a recognizable clothing photo.
2. Offer optional spoken playback of the same words.
3. If today's needs differ from the familiar or previous-day pattern, show two acceptable alternatives.
4. Accept a touch choice, pointing-supported choice, changed selection, or help request without requiring spoken explanation.
5. Exclude any garment that violates configured fabric-contact or tag-status rules.
6. Let the participant complete all visible steps.
7. End with an optional **"Finished, please check"** action that requests bounded family review.

The check is not a routine approval gate. The participant's choice remains selected unless a concrete safety, weather, availability, or sensory conflict is explained.

## Today screen semantics

- Page title: "Today, Thursday, September 3."
- Each section has a semantic heading and short summary.
- Outfit photos have user-supplied labels; AI-generated alt text requires confirmation.
- Two-choice outfit cards expose a complete spoken and text label, not only a photo.
- Completion controls state item name and current status.
- Weather includes numbers and words: "12 degrees Celsius. Cool. Rain likely after 1 PM."
- Changed-plan notices identify what changed, when, and what action is needed.
- A screen-reader summary presents the same four answers without traversing decorative content.

## Definition of done

A user-facing change is incomplete until:

- tested with keyboard, VoiceOver, and TalkBack on the affected flow;
- tested at maximum supported text size and both orientations;
- checked in high contrast, dark mode, and reduced motion;
- understandable without color or icon recognition;
- usable with network disabled where the flow is core;
- automated semantic checks pass;
- a manual cognitive walkthrough finds no unexplained state or dead end;
- advisory users have reviewed material interaction changes.
- the flow can be completed without expressive speech;
- hard sensory constraints cannot be bypassed by recommendation ranking; and
- supporter review begins only after an explicit participant action.

Automated tools find only a subset of barriers. A release requires manual and lived-experience testing.

## Accessibility issue policy

Label accessibility regressions as defects, not enhancements. A blocker in the Today, activity, wardrobe, consent, or supporter-revocation flows blocks release. Public reports may use the accessibility contact in `ACCESSIBILITY.md`; reports involving privacy or abuse use the security process.
