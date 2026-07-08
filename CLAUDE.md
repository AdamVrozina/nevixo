# Nevixo — playnevixo.com

Hub of original instant browser games. Global audience, English only, hosted in the US.
Owner is a beginner: explain steps clearly, keep code lean, verify functionality after changes.

## Approved brand (do not change without owner approval)
- Identity: "Night arcade" — dark, clean, Apple-informed geometry
- Colors: bg #0E0F13 · panel #15171D · line #23262E · ink #F2F2F5 · muted #8A8F9C
  accent teal #2BE4C6 · violet #8B7CFF · coin gold #FFC24B
- Typography: system stack (-apple-system, Segoe UI, Roboto) — never load webfonts
- Logo: assets/nevixo-logo.svg (dark), nevixo-logo-light.svg (light surfaces), nevixo-mark.svg (icon)
- Signature detail: bottom-anchored elements teal, top-anchored violet (see FLIP obstacles)

## Project structure (target)
- index.html — hub homepage (games rendered from the GAMES array; adding a game = adding one object)
- games/flip/index.html — game 1 (approved gameplay, do not alter feel/difficulty without approval)
- assets/ — logos, icons, og-image
- privacy.html, terms.html — required before ads go live

## Roadmap
1. FLIP (live) → submit to CrazyGames with their SDK, 2-month launch exclusivity (+50% rev share)
2. HUE — daily color-mixing puzzle (next build)
3. TINY COSMOS — minimalist idle game
Wave 2 (month 3–6): Lemmings-like original, single-player arena shooter — decide by traffic data.

## Monetization (approved plan)
- Own site: Google H5 Games Ads (Ad Placement API) — interstitial max 1×/2 min between runs,
  rewarded video = revive + coin doubler; AdSense display around the game page
- Portals: same placements via CrazyGames SDK; ads code sits behind the `Ads` abstraction
  in each game — swap backends per host, never call ad SDKs directly from game logic
- Later (after traction): Stripe one-time "Remove ads" ($2.99), premium skins
- No payments at launch; audience first

## Infra & tools
- Hosting: Cloudflare Pages (US), deploys from GitHub main branch
- Analytics: GA4 + Microsoft Clarity on all pages incl. games
- Feedback: Tally form linked from footer
- Keep total per-game payload small (portals expect ~5–8 MB initial download max; FLIP is <50 KB)

## Working rules
- Mobile first: test touch on iOS Safari and Android Chrome before calling anything done
- No frameworks unless justified — plain HTML/CSS/JS keeps games portal-compliant and fast
- English UI text, sentence case; owner communication in Czech
- Every game must ship with: save/progress, share hook, Ads abstraction, GA4 events
  (game_start, game_over, ad_impression, revive_used)
