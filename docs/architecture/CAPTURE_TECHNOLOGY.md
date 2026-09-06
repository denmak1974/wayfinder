# Capture technology: barcode, tag text, and garment recognition

## Status

Research complete. Nothing has been installed. The prototype's scanning, tag reading, and garment classification are simulated, and this document records which real implementations we would adopt and why.

Research date: September 6, 2026.

## Constraints

These are requirements, not preferences.

1. **On device.** A photograph of a participant's clothing must not be uploaded to a third-party service.
2. **Offline capable.** Capture happens in a bedroom or a shop, where connectivity is unreliable.
3. **Permissively licensed.** MIT, Apache-2.0, or BSD. No GPL or AGPL, no paid tier.
4. **Actively maintained.** A dependency that has announced it will not be fixed is not a dependency we adopt.
5. **Verified before adoption.** Repository, licence file, and recent commit history checked directly. No package is added because it appears in a tutorial.

## Barcode and QR

### Choice

| Target | Library | Licence |
| --- | --- | --- |
| HTML prototype | `Sec-ant/barcode-detector` (ponyfill), backed by `zxing-wasm` | MIT |
| React Native | `expo-camera`, using `onBarcodeScanned` | MIT |

`barcode-detector` implements the W3C Barcode Detection API shape, so the native browser API can replace it later without a rewrite. It covers EAN-13, EAN-8, UPC-A, UPC-E, QR, Data Matrix, and Code 128, which is everything a retail clothing tag carries. Expo already depends on this same library for its web target, so the prototype and the eventual app converge on one decoder.

Use the **ponyfill** entry point rather than the polyfill. The native `BarcodeDetector` API is unsupported in Firefox and disabled by default in Safari and iOS Safari, and Chrome's implementation is partial, so relying on it would produce inconsistent results on exactly the devices we care about.

### Rejected

| Library | Reason |
| --- | --- |
| `@zxing/library` | Self-declared "maintenance mode only... no active development or roadmap". Seeking new maintainers. |
| `html5-qrcode` | Maintenance mode, seeking new owner, and states pull requests will not be merged. |
| `serratus/quaggaJS` | Abandoned, last commit July 2023. Also 1D only, so it cannot read a QR code. |
| `vision-camera-code-scanner` | Archived, roughly three years dormant. |

### Required configuration

`zxing-wasm` fetches its WebAssembly binary from the jsDelivr CDN by default. Override `locateFile` to serve the roughly 1 MiB binary locally. Without this, a "privacy preserving, offline" feature makes a third-party network request on every scan.

## Reading a clothing tag

### Choice

| Target | Library | Licence |
| --- | --- | --- |
| HTML prototype | `tesseract.js` v7 with `eng+fra` | Apache-2.0 |
| React Native | `@react-native-ml-kit/text-recognition` | MIT wrapper over Google ML Kit |

ML Kit returns structured blocks and lines with bounding boxes rather than a flat string. Canadian care tags print English and French as spatially separate blocks, so geometry lets us segment by language instead of guessing where one language ends.

### Required configuration

- **Prototype:** point `workerPath`, `corePath`, and `langPath` at local assets. Left unset, tesseract.js downloads several megabytes of WebAssembly and language data from a CDN.
- **Android:** use the bundled `com.google.mlkit:text-recognition` artifact rather than the unbundled Play Services variant. It costs roughly 4 MB per architecture but removes both the first-run model download and the Google Play Services dependency. This is what makes the app genuinely offline on Android.

### Two honest caveats

**ML Kit is not open source.** It is free and runs on device, and Google's terms state that input data is not sent to Google servers, but it ships under proprietary API terms rather than a permissive licence, and it reports telemetry. If we later decide every dependency must be permissively licensed, the fallback is Apple Vision on iOS and native Tesseract on Android. That is a real cost and should be a deliberate decision rather than a discovery.

**Prototype OCR accuracy is not product OCR accuracy.** tesseract.js is a document OCR engine being asked to read small, wrinkled, low-contrast print. ML Kit and Apple Vision are scene-text detectors and should do better on the same photograph. Do not judge the concept on prototype results. Before committing, run a bake-off on roughly twenty real Canadian care tags.

## Product lookup from a barcode

**Do not build this.** Open product databases have effectively no apparel coverage. Open Products Facts holds about 45,000 products in total and roughly 224 in its clothing category. A lookup that fails almost every time is worse than no lookup, because it trains the user to distrust the feature. Its data is also ODbL, which carries share-alike obligations.

The useful alternative is entirely local: store the scanned barcode number on the garment record, and let the person name the item once. Scanning an identical second item then fills the name in automatically. That is offline, private, and completely accurate for this person's own wardrobe.

If a real lookup is ever added, it must be behind an explicit opt-in, because it would be the only feature that sends anything off the device.

## Garment classification from a photograph

Not yet researched. The prototype uses a filename keyword check as a placeholder, and it deliberately reports low confidence rather than guessing, which is the behaviour the real implementation should preserve.

## Unverified claims

Recorded so that nobody treats them as settled.

- Apparel coverage figures for UPCitemdb and Barcode Lookup could not be tested; both endpoints refused requests from the research environment.
- `expo-text-extractor` declares MIT in `package.json` but ships no licence file. Resolve with the author before depending on it.
- `@react-native-ml-kit/text-recognition` has had no commits in about a year. It works and it is a thin bridge, so forking is cheap, but treat continued maintenance as an assumption rather than a fact.
- The relative OCR accuracy claim above is architectural reasoning, not a measured benchmark.
