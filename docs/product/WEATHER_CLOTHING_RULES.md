# Weather and Clothing Rules

## Status

These rules are a **draft hypothesis**, not a finalized clothing policy. Final rules require photographs and attributes for Doug's actual wardrobe, observation across representative weather, and confirmation that both offered choices are comfortable and usable.

## Weather information shown

The Daily Readiness weather card should show:

- **Low:** expected minimum temperature for the day;
- **High:** expected maximum temperature for the day;
- precipitation type, probability, and timing;
- wind only when it materially changes the clothing or bring-item recommendation;
- severe-weather alerts from an authoritative source; and
- data age.

The participant-facing card should stay short enough to work the previous night or in the morning. Current temperature and apparent temperature can remain engine inputs or optional detail, but they should not be required to understand the plan.

When a future plan day is selected, Wayfinder should fetch the public forecast for the coarse activity area and selected date. If the forecast is unavailable, stale, or outside the provider window, the card must say so plainly and fall back to activity-based clothing guidance rather than inventing weather.

The outfit engine uses conditions during each outdoor exposure window, not one temperature for the entire day.

## The decision model

A full matrix of temperature × activity × precipitation × wind × venue is combinatorially unmanageable and mostly empty. Wayfinder decomposes it instead.

The reason the decomposition works is an asymmetry the participant already understands: **a top can be taken off, legs cannot.** So the slots are not decided by the same number.

### Step 1: one derived temperature per exposure

```text
effective = actual + activityWarmth − windPenalty
```

| Input | Values |
| --- | --- |
| `activityWarmth` | seated or casual `0` · walking `+2` · vigorous `+8` |
| `windPenalty` | under 20 km/h `0` · 20-34 km/h `−3` · 35 km/h and above `−5` |

Vigorous activity is worth roughly four temperature bands. This is why a 17°C jog must not be dressed like a 17°C errand.

### Step 2: three targets from the outdoor exposures only

| Target | Definition | Purpose |
| --- | --- | --- |
| `warmTarget` | highest effective temperature | Base top must survive the hottest, most active moment |
| `legTarget` | lowest effective temperature | Bottoms stay on all day, so they take the colder end |
| `outerTarget` | lowest still-air temperature | The outer layer is worn while standing around, not while moving |

Indoor periods contribute nothing to these targets.

### Step 3: each slot is one lookup

Every garment declares the slot it fills and the temperature range it suits. Rules ask for *a slot at a temperature*; they never name a garment. Adding a new item to the wardrobe therefore requires no rule change.

| Slot | Target used | Preference applied |
| --- | --- | --- |
| Base top | `warmTarget` | — |
| Bottom | `legTarget` | Long legs required when the indoor-seated proxy applies |
| Outer | `outerTarget` | Water resistance when rain is likely, wind resistance when windy |
| Footwear | `outerTarget` | Grip required when snow or ice is present, otherwise matched to activity |
| Accessory | `outerTarget` | Only below 0°C |

When several items would work, prefer the **lightest** one — the item with the highest minimum. This is the "err lighter and add a layer that comes off" principle expressed as a tiebreak.

### Step 4: caps and overrides

- **Above 25°C real air temperature at any outdoor exposure, no outer layer at all.** The cap uses real temperature, not the activity-adjusted value, so a warm active afternoon can never cancel a jacket that a cold morning genuinely requires.
- Offer an outer layer whenever `outerTarget` is below 18°C.
- Rain at 50% or above, or wind at 25 km/h or above, prefers a water- and wind-resistant shell over a soft layer of the same warmth.
- Snow or ice requires footwear with grip.

### Step 5: state the wardrobe gap, never substitute

If no item can fill a required slot — for example snow boots when none are owned — Wayfinder names the gap in the special items list rather than recommending footwear that is unsafe. The rest of the outfit still stands.

### Step 6: the explanation cannot grow

Only **one** driver is named, chosen by priority: snow → rain → wind → temperature spread → vigorous activity → indoor seated → plain conditions. An action line is added only when a layer is meant to come off. Rules may keep growing; the participant-facing output must not.

### Deliberately out of scope

| Excluded | Reason |
| --- | --- |
| Time spent outdoors | Temperature and activity dominate it |
| Sun and UV | Belongs to the future health module, alongside eczema care and medication |
| Humidity | Noise at Canadian shoulder-season temperatures |
| Swimming and full-day sports kit | These are bring-items, not worn-outfit decisions |
| Household chores | Belongs to a separate daily-chores module |

## Fit-model temperature bands

Select the band from the **warmest temperature during an outdoor exposure**, then apply modifiers. Do not select clothing from the overnight low alone, and never hardcode an outfit to a calendar date.

| Forecast high | Starting recommendation |
| --- | --- |
| 25°C and above | T-shirt and shorts; no jacket |
| 20 to 25°C | T-shirt and shorts; light layer only if the morning is much cooler |
| 15 to 20°C | T-shirt or thin long sleeve with long pants; light layer only for rain or a cool morning |
| 10 to 15°C | Thin long sleeve, long pants, and a light jacket |
| 5 to 10°C | Long sleeve, long pants, and a fleece or light down layer |
| 0 to 5°C | Warm long sleeve, warm pants, light down, and winter socks |
| Below 0°C | Warm long sleeve, winter pants, heavy down or parka, and winter socks |

A cool-morning modifier applies only when the high is 15°C or above, the low is 12°C or below, and the spread is at least 6 degrees. Rain at 50% probability or higher replaces the soft layer with a wind- and water-resistant shell.

Boundary values require an explicit convention before implementation. Until validated, a boundary or uncertain forecast should produce two acceptable choices rather than an abrupt hidden switch.

## Exposure windows, not day averages

A daily high and low describe the day. They do not describe what the person will actually feel. Wayfinder evaluates each period separately.

1. **Read hourly temperatures.** Take the coldest hourly value in the morning window and the warmest hourly value in the afternoon window from the forecast provider. When hourly data is unavailable, fall back to the daily low for the morning and the daily high for the afternoon, because that errs toward warmer clothing.
2. **Know which periods are outdoors.** An indoor morning does not need outdoor clothing, and an indoor afternoon does not justify a summer outfit.
3. **Choose the band from the warmest outdoor exposure.** This prevents overdressing for a day that ends warm.
4. **Protect the coldest outdoor exposure.** If any outdoor period is below 18°C, use long legs and add a layer the person can remove. Standing or walking outside below 18°C in a T-shirt and shorts is uncomfortable, even when the afternoon is warm.
5. **Say both numbers.** The explanation states the morning temperature and the afternoon temperature so the removal instruction makes sense.

### Worked example: cold start with a warm afternoon

| Input | Value |
| --- | --- |
| Forecast | Low 13°C, high 24°C, 1% rain |
| Morning | Community errand, outdoors, about 15°C |
| Afternoon | Outdoor active game, about 24°C |

- Using the daily high alone gives a T-shirt and shorts. That is wrong at 15°C in the morning.
- Using the daily low alone gives a jacket and warm pants. That is wrong at 24°C in the afternoon.
- Correct output: **T-shirt, thin long pants, light jacket, running shoes**, with the explanation "It is 15°C outside in the morning and 24°C in the afternoon. Wear the light jacket when you leave and take it off when you get warm."
- The jacket is worn rather than carried here, because the first outdoor exposure is genuinely cold. That differs from a hot day with an indoor morning, where no jacket is offered at all.

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

- low `10°C`;
- high `15°C`;
- rain after 1:00 PM;
- wind `22 km/h`;
- an indoor movie followed by outdoor walking at Trafalgar Park;

the first draft choice is:

> Long-sleeved cotton top, long jogging pants, light waterproof jacket, and walking shoes.

The second valid choice can use a removable cotton hoodie under a waterproof shell. This supports the cooler apparent temperature, indoor/outdoor transition, wind, rain, and walking activity.

## Explainability

The participant-facing explanation should identify no more than the facts needed to understand the recommendation:

> Low 10°C. Rain after lunch. Wear the grey long-sleeved top, grey jogging pants, light jacket, and walking shoes.

Avoid generic claims such as "dress warmly" and avoid presenting a recommendation as certain when wardrobe comfort has not been validated.

## Progressive wardrobe capture

The app must not require a perfect photo of every garment before it becomes useful. Use a progressive capture model:

1. **Inventory pass:** a supporter can take a small number of group photos by category, such as tops, pants, jackets, shoes, socks, and sportswear.
2. **Crop and confirm:** Wayfinder suggests item cards from the group photos. A participant or supporter confirms the crop, category, plain-language label, warmth, fabric, tag status, and sensory constraints.
3. **Improve only when needed:** retake individual photos only for items that are frequently recommended, visually confusing, safety-relevant, or important to the participant.
4. **Reuse cards:** once an item card is confirmed, daily recommendations reuse the saved card and never ask for a fresh photo unless the user chooses to update it.
5. **Allow unknowns:** items with incomplete attributes can remain in the wardrobe but are excluded from recommendations that depend on the missing attribute.

This keeps onboarding realistic for families while still building toward accurate, recognizable clothing choices.

For higher-quality individual photos, use a plain contrasting background, even lighting, one item per image, no faces or room details, and a close crop with a small margin. JPEG working copies are preferred for compatibility, while original photos remain private masters.

## Future low-friction wardrobe import

Taking a full wardrobe photo set is too onerous to be the only path. Future versions should support multiple intake methods and let families choose the lowest-effort path that still creates recognizable, safe recommendations.

| Intake method | What it can provide | Limitation |
| --- | --- | --- |
| Clothing tag photo | Fabric, size, care instructions, and brand text | Still needs confirmation; tags may be faded, cut out, or too generic |
| Barcode, QR, SKU, or style number | Possible product lookup when present | Use only if it resolves the exact garment or a useful official image |
| Retailer order history or receipt | Product name, colour, size, and sometimes official image | Requires account/file permission and user review |
| One quick garment photo | Participant-recognizable card image | Still manual, but should be needed only for unclear or high-use items |
| Group photo | Fast inventory seed | Requires crop and attribute confirmation |

Do not support RN-number-only lookup as a wardrobe intake path. In North America, an RN number usually identifies the manufacturer or importer, not the exact garment Doug needs to recognize and wear.

The best product experience is a hybrid: tag/OCR/import data suggests attributes, one recognizable photo or crop anchors the participant-facing card, and a supporter confirms only uncertain fields. Wayfinder must never silently trust a tag lookup for sensory constraints, warmth, rain/snow suitability, or participant preference.

## Canadian wardrobe decision tags

Use Canadian weather realities as the default tagging frame, then tune from Doug's observed comfort. Tags should describe when an item is useful, not whether it is fashionable.

### Core item tags

| Tag group | Allowed tags | Meaning |
| --- | --- | --- |
| Category | `top`, `bottom`, `outerwear`, `footwear`, `underwear`, `accessory`, `specialBag` | What kind of item it is |
| Layer | `base`, `mid`, `outer`, `bottom`, `footwear`, `carry` | How the item is worn or carried |
| Warmth | `hot`, `mild`, `cool`, `cold`, `freezing` | The coldest comfortable use before modifiers |
| Precipitation | `dryOnly`, `lightRain`, `rain`, `snow` | Whether the item works in Canadian rain/snow |
| Wind | `notWindReady`, `windResistant` | Whether it helps on windy days or open areas |
| Activity | `indoor`, `walking`, `running`, `exercise`, `swimming`, `communityOuting`, `outdoorExtended` | Where the item is appropriate |
| Sensory | `cottonTouchingSkin`, `tagRemoved`, `tagless`, `preferred`, `avoid` | Hard constraints and known preference signals |
| Availability | `available`, `laundry`, `wet`, `damaged`, `unavailable` | Current state |

### Canadian warmth defaults

| Forecast band | Primary tags to prefer |
| --- | --- |
| Above 25°C | `hot`, breathable `base`, shorts if approved |
| 15-25°C | `mild`, cotton base, light optional outer layer |
| 10-15°C | `cool`, long sleeves or light mid layer, long pants |
| 1-10°C | `cold`, insulated outerwear, warm socks, toque/gloves available |
| Below 0°C | `freezing`, winter coat, toque, gloves, scarf, warm socks, winter footwear |

### Example tags for Doug's first cards

| Plain label | Suggested tags |
| --- | --- |
| Grey long-sleeved top | `top`, `base`, `cool`, `dryOnly`, `indoor`, `walking`, `cottonTouchingSkin`, `tagRemoved` |
| Cotton T-shirt | `top`, `base`, `hot`, `mild`, `dryOnly`, `indoor`, `communityOuting`, `cottonTouchingSkin`, `tagRemoved` |
| Grey jogging pants | `bottom`, `cool`, `cold`, `dryOnly`, `indoor`, `walking`, `preferred` |
| Long stretch pants | `bottom`, `mild`, `cool`, `dryOnly`, `running`, `exercise`, `walking` |
| Light jacket | `outerwear`, `outer`, `cool`, `lightRain`, `windResistant`, `walking`, `communityOuting` |
| Running shoes | `footwear`, `dryOnly`, `running`, `exercise`, `walking` |
| Walking shoes | `footwear`, `lightRain`, `walking`, `communityOuting` |
| Warm socks | `accessory`, `cold`, `freezing`, `footwear`, `cottonTouchingSkin` when confirmed |

### Special item handling

Do not tag default daily items as daily recommendations. Put them in the participant's default-item profile:

- Hub bag;
- water bottle;
- lunch box;
- wallet/card or other always-carried items.

The daily plan only shows exceptions created by weather or schedule parsing, such as umbrella, sunscreen, grocery list, swim bag, towel, change of clothes, or "no lunch box."

## Reasoning with proxies when facts are missing

Wayfinder will often lack a measured fact. Indoor temperature, venue air conditioning, and how long a person will sit are rarely in a location schedule. The correct response is neither to invent the fact nor to ignore the need. Use an explicit, documented proxy.

A proxy is acceptable only when all of these hold:

1. **It is stated, not hidden.** The participant-facing explanation says what is assumed, in plain language.
2. **It is a general pattern, not a specific claim.** Say "indoor rooms are usually cooler than a warm day outside", not "Film.ca will be 21°C".
3. **The failure mode is mild.** If the proxy is wrong, the person is slightly less comfortable, not unsafe.
4. **It can be replaced by evidence.** Once a participant or supporter confirms the real attribute, the stored fact overrides the proxy permanently.

### Asymmetry of risk

When two exposures conflict, weight the more serious outcome. Overheating while walking outdoors in high heat is a safety concern. Feeling chilly in an air-conditioned room is a comfort concern. The recommendation should protect against the safety concern first.

### Prefer one workable outfit over an extra carried item

An added jacket on a hot day creates two new failure modes: the participant may keep it on outdoors and overheat, or may set it down and lose it. When a single garment choice can satisfy both exposures, choose that instead. Covering the legs with thin long pants solves indoor cooling without adding anything to carry, remove, or remember.

### Worked example: indoor movie followed by an outdoor park

| Input | Value |
| --- | --- |
| Forecast | Low 19°C, high 28°C, 20% rain |
| Morning | Indoor seated activity, roughly two hours |
| Afternoon | Outdoor walking |

- Band from the daytime high is `hot`, so the base outfit is a T-shirt with light legs and walking shoes.
- Naive output is a T-shirt and shorts. That is right for the park and probably cold for a long seated indoor session.
- Adding a jacket would be wrong: it is warm enough outdoors that a worn jacket is a heat risk, and a carried jacket adds management burden.
- The proxy applies: an indoor seated activity on a day at or above 20°C is usually cooler indoors than outdoors.
- Result: **T-shirt, thin long pants, walking shoes**, with shorts offered as the second choice.
- The explanation states the assumption so the participant and supporter can disagree with it.

### Implemented rule

Cover the legs with thin long pants instead of shorts when the activity context includes a seated indoor session and the forecast high is 20°C or above. Below 20°C the recommendation already uses long pants, so the rule changes nothing. This rule never adds an outer layer on a warm or hot day.

### Capture in bursts, sort once

The friction in wardrobe setup is not the number of taps per garment. It is standing in front of a closet holding forty items while the app asks four questions about each one. People abandon that.

So capture and classification are separated:

1. **Keep shooting.** Photograph the tag if there is one, then the garment. Several garments can be captured in a single pass. No typing, no dropdowns, no confirmation while hands are full.
2. **Review once.** Every captured item appears in a grid with category and warmth already filled in. The person corrects only what is wrong.
3. **Flag rather than guess.** When classification is uncertain the item is still kept, but it is marked "not sure — please check" so the person's attention goes where it is needed.

A tag photo taken immediately before a garment photo is paired with it, so the fabric and care details attach to the right item.

### The tag is data; the photo is identity

These answer different questions and neither replaces the other.

| Source | Provides |
| --- | --- |
| Tag or barcode | fabric, colour name, size, warmth class |
| Photograph of the garment | recognition — the specific object in this person's closet |

Retailer stock photography is deliberately **not** used for wardrobe items. A catalogue image shows a styled garment on a model in ideal light, which is not what the participant is looking for on a hook in their room. Stock imagery is appropriate when shopping for something not yet owned; that is a different module.

### Never offer a bulk replace

"Add or replace the whole wardrobe?" asks the person to think in database terms and makes one wrong tap catastrophic. It also conflates four different intentions:

| Actual situation | Correct behaviour |
| --- | --- |
| Bought new clothes | Add |
| First-time setup | Add, since the list is empty |
| Storing clothes for the season | Mark unavailable |
| Worn out or given away | Remove that one item |

Capture therefore always adds. Duplicate protection comes from recognising a repeated item and offering to update it, not from wiping the collection.

### Comfort and sensory notes belong elsewhere

Fabric-against-skin preferences, tag irritation, favourites, and items to avoid are **not** collected during capture. They are answered best when the person reacts to a real recommendation, or at the point of purchase where a store associate can help. Collecting them while photographing a closet slows the flow and produces guesses rather than evidence.

### Most clothes span several kinds of day

Forcing a garment into a single warmth bucket is wrong for the majority of a wardrobe. A cotton t-shirt is comfortable from a mild day right through a hot one. A windbreaker covers cool and mild. Only genuinely specialised items — a heavy parka, winter down pants — belong to one band.

So warmth is captured as **every band that applies**, not one choice:

| Band | Range |
| --- | --- |
| Cold | below 3°C |
| Cool | 2 to 12°C |
| Mild | 10 to 20°C |
| Warm | 18 to 28°C |
| Hot | 25°C and up |

The stored range is the union of the selected bands, and adjacent bands overlap deliberately so there is no cliff edge at a boundary. When an existing item is edited, every band its range already covers is shown pre-selected.

This matters for recommendation quality, not just data tidiness. Wide, honest ranges give the engine more valid candidates, so the "lightest item that still works" tiebreak has something to choose between instead of falling back on a single arbitrary match.

### Past days are a record, not a plan

A day that has already happened is still useful. It answers "what did I wear when it was like this?" and it lets a supporter check whether a recommendation actually worked. But it must never be mistaken for the day being prepared for.

- Keep a day for **seven days** after it happens, then drop it.
- Label every past day in the day picker with how long ago it was, show it in a receded style so the eye lands on the current day, and show a plain statement on the plan itself.
- Open on today. If the imported schedule has no entry for today, open on the next upcoming day rather than a day that has gone.
- **Remove** the forward-looking actions on a past day rather than disabling them. A greyed-out "Choose this outfit" reads as something the person failed to do. The weather, activities, and recommendation stay visible, because those are the record.
- Change the closing section from "You are getting ready" to "What you wore", so the whole screen agrees about what it is.

### A day with no activities is still a day

Weekends, holidays, and days the location simply did not send anything are normal. They must not produce a blank screen, an error, or a silent jump to a different day.

On a day with no schedule entry, keep the weather and the outfit and empty only the schedule. Assume a normal amount of going outside rather than assuming the person stays in, because under-dressing is the worse failure.

Distinguish two cases, because they are different facts:

| Case | Wording |
| --- | --- |
| The location is closed and said so | "The Hub is closed today. It is Labour Day." |
| Nothing was scheduled | "Nothing from the Hub today. It is the weekend." |

A closed day is information the location provided. An empty day is the absence of information. Saying "no activities" for a public holiday would discard something the schedule actually told us.

## Adding, editing, and removing clothes

### Add: cheapest reliable signal first

The onboarding flow is ordered by effort, and every step can be skipped.

1. **Scan a barcode or QR code.** Used only when it identifies the exact garment. RN numbers are never used for this, because they identify the maker rather than the item.
2. **Photograph the tag.** OCR reads fabric, care, and size text when there is no usable barcode.
3. **Confirm the details.** Anything suggested by a lookup is shown as a proposal with its source named. Nothing is stored until the person approves it.
4. **Add a photo and comfort notes.** Both optional. The photo helps the participant recognize the item; the comfort notes record cotton-against-skin, tag status, favourites, and items to avoid.

Manual entry is always available and is never treated as a failure path.

### Edit and remove: by category

Management is browsed by category rather than as one long list. Editing pre-fills the existing values and saves in place. Removing hides an item from recommendations without destroying it, the count of hidden items stays visible, and a single action restores them.

Built-in and user-added items behave identically. Edits to built-in items are stored as overrides, so an original definition is never lost.

### Photos are not a prerequisite

An item can exist and be recommended before a photo is taken. The plan notes that the picture is missing rather than withholding the item. This matters for things that are owned but awkward to photograph, such as boots stored away out of season.

### Representative items, not an inventory

Where a category contains many interchangeable duplicates, model the **decision** rather than the objects. Doug owns dozens of pairs of socks but only three decisions: regular for most days, short for active days, thick for cold days. One representative photo per decision is enough for recognition, and the everyday default is suppressed from the plan entirely.

## Validation after wardrobe capture

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
