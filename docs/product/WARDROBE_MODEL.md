# Wardrobe model

## Decision date

September 6, 2026. This supersedes the earlier approach, in which every garment was an individually photographed item with its own temperature range.

## The principle

Model a garment individually only when the choice is hard or getting it wrong is unsafe. Everywhere else, model the type and let the person choose the specific item themselves.

Telling an adult which particular t-shirt to wear is not assistance. It removes a decision he is perfectly able to make, and the visible, expressive part of dressing is exactly where that autonomy matters. Telling him he needs a jacket today, and which one, is genuine help.

## Generic types

These are modelled as a small set of types, each with one representative photograph. The photograph exists so the participant recognises what is meant, not so he finds that exact object.

| Slot | Types |
| --- | --- |
| Tops | T-shirt, long-sleeved t-shirt, sweatshirt |
| Bottoms | Shorts, light sweatpants, heavy sweatpants |
| Socks | Short sports socks, regular socks, thick socks |

The participant chooses which t-shirt. The recommendation says "a t-shirt", not "the grey Buffalo t-shirt".

## Specific items

These keep individual photographs and individual attributes.

**Jackets and coats.** This is the decision the participant most needs help with, and we suspect that is true well beyond this one person. Outer layers map closely to temperature and conditions, and two jackets of the same colour can be completely different in warmth.

**Footwear.** Wrong footwear is the failure with real consequences. Running shoes on ice is not a comfort problem.

**Exceptions.** Down bottoms, for a full day outdoors in snow, and dress shirts. Both are worn rarely and chosen for a specific reason.

### A personalisation axis, not a fixed rule

Douglas is the fit model and needs the photographs for jackets. A more independent person might be well served by type names alone. Where the boundary between generic and specific sits should eventually be a per-person setting rather than a constant.

## What this removes

Barcode scanning, tag OCR, retailer product lookup, and per-garment onboarding all existed to support individually modelled items at scale. With only jackets and footwear modelled individually, that machinery is unnecessary. A handful of photographs, taken once, is enough.

This is a significant simplification of both the product and the build.

## Change of clothes

Distinct from special items, and distinct from the day's outfit.

Some days require a **second outfit carried in a bag**, to be changed into partway through the day. An indoor run in winter is the clearest example: the participant leaves the house dressed for the cold, and needs light clothing for the run itself.

> **Wear:** heavy sweatpants, thick socks, parka, winter boots
> **Bring in a bag:** t-shirt, shorts, short sports socks, for the indoor run

This also covers swimming, which needs swimwear, a towel, and dry clothes to change back into.

It is a second outfit, not a bring-item. An umbrella is something you carry; a change of clothes is something you wear later. Presenting them the same way loses that.

## What to expect

This section is for the participant, not for supporters. Supporters may read it, and may ask for a change based on it, but it is written for him.

It must answer **"what about today is not like most days?"** It must not restate the day's activities, which are already on the screen directly above it.

| Case | Example |
| --- | --- |
| A change in routine | "The Hub is closed Monday." |
| Something that needs a decision | "You will change clothes for the swim." |
| An unusual transition | "The boat ride may feel colder than the walk." |
| Something not on the schedule | "Lunch is provided Friday." |
| Nothing unusual | "Today is a normal day." |

The last case is the most important and the easiest to get wrong. A predictable day is itself useful information for someone who finds change difficult. Saying "today is a normal day" is a real answer, and far better than manufacturing an observation to fill the space.

Keep it to one or two short sentences.

## How success is measured

If this builds independence eight or nine times out of ten, it is a success. The goal is not a perfect recommendation every day. It is that the participant can start his day without having to ask.
