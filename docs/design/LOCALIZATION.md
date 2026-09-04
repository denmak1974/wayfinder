# Localization Architecture

## Initial locales

| Locale | Display name | Purpose |
| --- | --- | --- |
| `en-CA` | English | Initial authoring and Canadian date/measurement conventions |
| `ja-JP` | 日本語 | Japanese interface, guidance, accessibility labels, and spoken prompts |
| `fr-CA` | Français | Canadian French interface, guidance, accessibility labels, and spoken prompts |

The participant selects the interface language. A supporter may use a different language on their own device without changing the participant's preference.

## What is localized

- navigation, headings, buttons, forms, settings, and help;
- weather and clothing guidance;
- generated activity context and bring-item reasons;
- status, error, confirmation, and accessibility announcements;
- dates, times, temperatures, numbers, and plural-sensitive messages;
- screen-reader labels; and
- optional text-to-speech prompts.

## What is preserved

Proper names and source-controlled text remain as received unless an approved source translation exists:

- participant and supporter names;
- organization and place names;
- calendar titles such as `Film.ca Scoob movie`; and
- location-provided activity names such as `2000 Steps into September`.

Wayfinder may show a translated explanation beside a preserved source title. It must not silently rewrite a title that a participant or location may need to recognize.

## Production implementation

- Keep source strings outside application components in versioned locale resources.
- Use stable message identifiers rather than English text as keys.
- Use ICU MessageFormat for plurals, grammatical variants, and complete sentences.
- Format dates, times, numbers, and measurements with platform locale APIs.
- Store domain values such as `morning`, `activeWalking`, and `outlook` as stable codes; translate only their presentation.
- Keep the participant's locale separate from source-document locale, calendar locale, and speech voice.
- Fall back by message, not by entire screen: selected locale, language fallback, then `en-CA`.
- Record missing translations during development without exposing diagnostics to the participant.
- Never send personal content to an external translation service without separate consent and a reviewed data-processing agreement.

The self-contained HTML prototype uses inline resources so it works from a downloaded file without a server. Production applications should load bundled locale resources.

## Japanese requirements

- Use clear, literal, adult-respectful Japanese.
- Avoid unnecessary kanji when a common, readable alternative is clearer.
- Test line breaks, font fallback, text-to-speech pronunciation, and mixed Japanese/Latin proper names.
- Do not assume Japanese language implies Japan-based dates, addresses, or units; those are separate preferences.

## Canadian French requirements

- Use Canadian terminology and conventions where they differ materially.
- Avoid translating from English word-by-word; review complete instructions in context.
- Test grammatical agreement and plural handling through ICU messages.
- Verify speech with a `fr-CA` voice where the device provides one.

## Translation workflow

1. Product and accessibility reviewers approve the source message and interaction.
2. A translator produces the locale resource with context notes and screenshots.
3. A second qualified reviewer checks meaning, adult tone, cognitive simplicity, and terminology.
4. A participant or accessibility advisor tests the message in the actual flow.
5. Automated checks verify key completeness, interpolation variables, markup safety, and layout expansion.
6. The locale ships with reviewer provenance and a translation version.

Machine translation may create a draft but cannot approve safety, consent, schedule, clothing, or supporter-access messages.

## Definition of done

- The complete core flow works in all supported locales without mixed-language interface text.
- Dates and status messages update immediately after switching.
- Dynamic messages preserve variables and names.
- Screen-reader labels use the selected language.
- Text-to-speech requests the selected locale and fails without blocking the task.
- At 200% text size, Japanese and French content remains readable without clipped actions.
- Source activity titles remain recognizable.
- A locale can be added without changing domain or recommendation logic.
