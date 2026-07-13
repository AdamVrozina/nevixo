# Nevixo — STATUS (handoff)

Last updated: 2026-07-13. Hub of original instant browser games (playnevixo.com).
See CLAUDE.md for brand/roadmap rules. IDs below (GA4, Clarity, AdSense pub) are
public identifiers embedded in the shipped HTML — not secrets. No passwords/tokens here.

## Done & deployed
- **Hub homepage** (`index.html`) — games rendered from a `GAMES` array; About section; footer with real Tally forms (feedback + email signup).
- **4 games, all live & playable**, each self-contained plain HTML/JS/canvas, with save/progress (localStorage), share hook, `Ads` abstraction, `Sound` abstraction (Web Audio, no files, mute toggle), and GA4 events (game_start, game_over, ad_impression, revive_used):
  - `games/flip/` — one-tap gravity arcade; coins + 6 cosmetic skins.
  - `games/hue/` — daily 6-color mixing puzzle; streak; emoji share.
  - `games/cosmos/` — completable idle toy (Particle→Universe); offline growth.
  - `games/swarm/` — survivors-like arena shooter roguelite; level-up upgrades.
- **Legal**: `privacy.html`, `terms.html`, `404.html`.
- **Analytics on every page**: GA4 `G-YK8LGZ2VRJ` + Microsoft Clarity `xj0mjlnxrb`.
- **Ads groundwork**: AdSense snippet `ca-pub-6776426263711336` + `ads.txt` on all pages. FLIP/HUE/COSMOS/SWARM use Google H5 `adBreak` with a simulated fallback.

## File structure
```
index.html  privacy.html  terms.html  404.html
ads.txt  wrangler.jsonc  CLAUDE.md  STATUS.md
assets/            logos + mark (svg)
games/flip|hue|cosmos|swarm/index.html
portals/crazygames/flip/
  index.html    CrazyGames build (CrazyGames SDK v3 only, no Google scripts)
  covers.html   generates 3 cover sizes (1920x1080, 800x1200, 800x800)
  autodemo.html self-playing FLIP for recording preview videos
  listing.md    store listing copy
  (flip-crazygames.zip — leftover, unused; uploader takes raw files)
```

## Live URLs
- Production: **https://playnevixo.com** (and **www** 301-redirects to it)
- Cloudflare fallback: **https://nevixo.adam-vrozina.workers.dev**

## Deploy
- **GitHub repo**: `AdamVrozina/nevixo` (public), branch `main`.
- **Hosting**: Cloudflare **Workers** static assets (NOT Pages), project **nevixo**, connected via Git. Config in `wrangler.jsonc` (serves repo root, 404-page handling).
- **Publish flow**: commit + push to `main` → Cloudflare auto-deploys in ~30–60s. No build step. Verify with a cache-busted curl (`?v=timestamp`) or hard-refresh (Cmd+Shift+R) since browsers cache the HTML.
- **Domain**: playnevixo.com registered at czechia.com, nameservers moved to Cloudflare (`aitana`/`justin.ns.cloudflare.com`); www→root via a Cloudflare Page Rule.

## In progress / awaiting
- **CrazyGames review**: FLIP submitted as **Full launch** (2026-07-12), in their QA. If they request changes, edit `portals/crazygames/flip/index.html` and re-upload (raw files, not zip). See memory `crazygames-flip-submission`.
- **AdSense review**: Czech account, site in "Preparation". Once approved: place ONE manual display unit in homepage `.adslot` (do NOT enable Auto ads); finish payment/tax (W-8BEN, Czech bank/Wise) — US details were a placeholder, use real Czech info.

## Not built / deferred
- Sprite/character shooter version of SWARM (owner wanted it; needs external art — parked).
- TINY COSMOS v2 (automation, prestige, accounts/cloud-save).
- HUE "Archive pass" premium; any payments (site is no-accounts, ad-first).
- Only FLIP has a portal build; HUE/COSMOS/SWARM not yet prepared for portals.

## Known issues / notes
- **Safari audio in iframe**: portal FLIP has a Safari/iOS Web Audio `unlock()` (silent buffer on first gesture); the live-site games have the resume fix but NOT the silent-buffer unlock — worth propagating if iOS players report no sound.
- **CrazyGames SDK audio-mute** not integrated in the portal build (checkbox left off) — deferred polish.
- Mobile-first: test touch on iOS Safari / Android Chrome before calling changes done.
- Keep each game self-contained (no shared JS) so portal builds stay portable.
