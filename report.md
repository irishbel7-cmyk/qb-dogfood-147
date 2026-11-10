# Dogfooding Report — Chrome extension (Frantic #147)

## What was done
- Built a minimal but complete Chrome MV3 extension ("QB Dogfood Probe" v1.0.0): `manifest.json` + `popup.html`.
- Loaded it into a real Chrome session: Google Chrome for Testing **156.0.8078.4**, launched with `--load-extension`, headless=new, isolated `--user-data-dir`.
- Interrogated the browser through the Chrome DevTools Protocol (`chrome://extensions` page → `chrome.developerPrivate.getExtensionsInfo()`).

## What to inspect first
1. `dogfood_ext_popup.png` — actual rendered popup: header "QB Dogfood Probe", body "Extension loaded OK".
2. `evidence.json` — machine-readable proof: exact extension ID, state, error count, commands, HTTP/CDP call path.

## Proof
- Extension registered as **ENABLED**, extension id `jnaceifbmbnelpebnafedjipeopgmjpb`, **0 runtime errors**:
  `[{"id":"jnaceifbmbnelpebnafedjipeopgmjpb","name":"QB Dogfood Probe","state":"ENABLED","version":"1.0.0","errors":0}]`
- Popup DOM text read back from the live page: `QB Dogfood Probe | Extension loaded OK`.
- Popup render captured as a PNG screenshot (see repo).

## Limitations
- Probe extension is minimal by design (single-purpose verification artifact); unpacked load, not a Web Store install.
- `document.title` of the popup is empty (no `<title>` element in popup.html) — cosmetic only, noted for completeness.
