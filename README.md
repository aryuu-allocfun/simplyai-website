# SimplyAI.work

Static site for **SimplyAI.work**, deployed via **Cloudflare Pages** (build output directory = `src/`).

## Structure (`src/` = web root)

| URL | File | What |
|-----|------|------|
| `/` | `src/index.html` | **AI Search Visibility agency** (primary brand — GEO/LLMO for aesthetic clinics & law firms) |
| `/bossai/` | `src/bossai/index.html` | **BossAI** — SimplyAI's AI Business Copilot (relocated from root) |
| `/robots.txt` | `src/robots.txt` | AI crawlers explicitly allowed + sitemap ref |
| `/sitemap.xml` | `src/sitemap.xml` | `/` and `/bossai/` |
| — | `src/_redirects` | Cloudflare Pages 301 aliases → `/bossai/` |

Both pages are self-contained plain HTML/CSS (inline styles, CDN fonts/icons). No build step.

## Development
Open `src/index.html` (or `src/bossai/index.html`) in a browser.

## Deployment
- **Production**: https://simplyai.work (deploys from `main`)
- **Preview**: every branch / PR gets an auto-generated Cloudflare Pages preview URL

### ⚠️ Cloudflare dashboard checks (not in this repo)
- Confirm **AI-bot blocking / Bot Fight Mode / pay-per-crawl is OFF** for this zone — this is an AI-visibility business; blocking AI crawlers is self-defeating.
- The BossAI chatbot posts to `https://backend.simplyai.work/boss-ai` (separate Cloudflare Worker) — unaffected by the path change.

## Documentation
- [GA Setup Guide](docs/GAguide.md)
