# REALMBOUND — Round 2 preview deployment

This is an **incomplete experimental Round 2 preview**, packaged from the interrupted AI Studio partial artifact. It is authorized for preview deployment as-is; it is **not** a completed Round 2 build, a production release, or an Android certification/build. The actual game logic and its existing cheat/god powers are intentionally preserved.

## PWA packaging scope

- `index.html` is the supplied partial HTML with packaging-only changes: the embedded data-URI manifest/SVG icon were replaced with relative files, and a non-blocking service-worker registration was added.
- `manifest.webmanifest` uses `./` `start_url` and `scope`, so it remains safe when hosted below a domain subpath.
- `icon-192.png` and `icon-512.png` are simple programmatic PNG icons (not sprites).
- `sw.js` uses a versioned cache (`realmbound-round2-preview-v2`) and cache-first app-shell behavior. After the first successful online visit/install, the app shell can launch offline; this does not make every runtime asset or external request offline-capable.
- This package is intended for free GitHub Pages hosting.

The page references Google Fonts for the pixel face. If that request is unavailable, the existing CSS falls back to `Courier New`, UI monospace, or the system sans-serif stack; gameplay does not depend on the font download.

## Risks and saves

The source is incomplete and carries known unverified areas from the source audit: full browser boot/rendering, real touch/multitouch dispatch, runtime save/load and reset/reload atomicity, quota/corruption recovery, and all gameplay paths were not proven here. Existing local save behavior remains the source behavior; users should assume saves may be experimental and keep backups/export data where the game provides them. Do not treat this preview as a durable save migration target or as a replacement for the immutable checkpoint.

The service worker can serve a cached stale preview until its cache version changes. Clear site data/unregister the worker when testing a fresh package. The worker caches only app-shell files and falls back to `./index.html` for failed navigations; it does not cache external Google Fonts or guarantee offline network-backed features.

## Source integrity

Input: `/workspace/realmbound-five-rounds/round-02/aistudio-partial/partial-index.html`  
Input SHA-256: `4056b0683cef69614820bfaf7ce1021912bd41c271dcec9a812eef06d4a70ce6`  
The source checkpoint was not modified. The packaged HTML necessarily has a different SHA-256 because of the documented PWA metadata changes.
