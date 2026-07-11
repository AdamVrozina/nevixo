# CrazyGames portal builds

Portal-specific builds of Nevixo games for submission to CrazyGames.
These are **separate** from the versions served on playnevixo.com.

## What's different from the playnevixo.com build

- **No Google scripts** — AdSense (`adsbygoogle.js`), GA4 (`gtag`), and
  Microsoft Clarity are removed. Portals disallow external ad/analytics
  scripts; only the CrazyGames SDK is allowed.
- **CrazyGames SDK** (`crazygames-sdk-v3.js`) is loaded instead, and the
  game's `Ads` abstraction calls `SDK.ad.requestAd('midgame' | 'rewarded')`.
- **Gameplay lifecycle** wired: `SDK.game.gameplayStart()/gameplayStop()`
  and `loadingStop()`.
- **No external links** (the header logo no longer links to the hub) and no
  dev-facing footer.
- Rewarded ads grant the reward only on `adFinished`; on `adError`
  (no fill / ad blocked) nothing is granted and play continues.

## How to package for upload

CrazyGames wants a single `.zip` of the game's files with `index.html` at
the root. Each game here is one self-contained `index.html`, so:

```
cd portals/crazygames/flip
zip flip-crazygames.zip index.html
```

Upload that zip in the CrazyGames developer portal
(developer.crazygames.com) when creating the game.

## Testing locally

Served over http, the SDK reports `environment: "local"` and **simulates**
ads (you'll see its own ad overlay), so the full ad flow is testable without
being on crazygames.com.
