# Weather and Clothing Rules

## Status

These rules are a **draft hypothesis**, not a finalized clothing policy. Final rules require photographs and attributes for Doug's actual wardrobe, observation across representative weather, and confirmation that both offered choices are comfortable and usable.

## Weather information shown

The Daily Readiness weather card should show:

- **Now:** current measured temperature;
- **Feels like:** apparent temperature accounting for wind and humidity;
- **High:** expected maximum temperature;
- precipitation type, probability, and timing;
- wind speed and, when relevant, gusts;
- severe-weather alerts from an authoritative source; and
- data age.

The outfit engine uses conditions during each outdoor exposure window, not one temperature for the entire day.

## Draft fit-model temperature bands

Use the coldest relevant `feels like` value during an outdoor activity as the starting band.

| Feels-like temperature | Draft starting recommendation |
| --- | --- |
| Below 0°C | Down jacket, toque, gloves, scarf, warm socks |
| 1–10°C | Lighter down jacket; keep toque, gloves, scarf, and warm socks available |
| 10–15°C | Light jacket, long-sleeved cotton top, long jogging pants |
| 15–25°C | Cotton T-shirt and long pants; add a rain shell only when conditions require it |
| Above 25°C | Cotton T-shirt and shorts |

Boundary values require an explicit convention before implementation. Until validated, a boundary or uncertain forecast should produce two acceptable choices rather than an abrupt hidden switch.

## Conditions that materially alter clothing

Apply these after selecting the starting temperature band:

| Condition | Rule effect |
| --- | --- |
| Rain | Add a waterproof outer layer and suitable footwear |
| Strong wind or gusts | Prefer a wind-resistant outer layer; apparent temperature may move the recommendation to a colder band |
| Snow or ice | Add winter footwear, gloves, and appropriate traction considerations |
| Long outdoor exposure | Increase warmth or add a removable layer |
| Short vehicle-to-building exposure | Avoid unnecessary heavy insulation when the participant will remain indoors |
| Vigorous exercise or running | Prefer breathable layers and reduce insulation while active; provide a warm layer for before and after |
| Mostly seated outdoors | Increase warmth relative to active movement |
| Swimming or water activity | Add swimwear, towel, dry clothing, and water-safe footwear |
| Large morning-to-afternoon change | Use removable layers and explain when to add or remove them |
| Unknown activity or forecast | Preserve a safe familiar option and request clarification |

Hard sensory constraints—such as cotton touching skin and tag status—apply before all weather ranking.

## Example

For:

- now `12°C`;
- feels like `10°C`;
- high `15°C`;
- rain after 1:00 PM;
- wind `22 km/h`;
- an indoor movie followed by outdoor walking at Trafalgar Park;

the first draft choice is:

> Long-sleeved cotton top, long jogging pants, light waterproof jacket, and walking shoes.

The second valid choice can use a removable cotton hoodie under a waterproof shell. This supports the cooler apparent temperature, indoor/outdoor transition, wind, rain, and walking activity.

## Explainability

The participant-facing explanation should identify no more than the facts needed to understand the recommendation:

> It feels like 10°C. Trafalgar Park is outside, and rain and wind are expected. Wear a long cotton top, long jogging pants, a light waterproof jacket, and walking shoes.

Avoid generic claims such as "dress warmly" and avoid presenting a recommendation as certain when wardrobe comfort has not been validated.

## Validation after wardrobe photography

For every garment, record:

- recognizable participant-facing photo;
- garment category and layer;
- warmth level;
- fabric materials and fabric touching skin;
- tag status;
- rain and wind resistance;
- suitable activities;
- footwear grip and water resistance;
- laundry/availability state; and
- known preferred combinations.

Then test each temperature band using two complete outfits from Doug's wardrobe. Adjust the bands from observed comfort and successful independent use, not fashion norms.
