# Taybuta.com — one-page site

A single-file static site. No build step, no framework. Two files that matter: `index.html` + `styles.css`.

## Design

- **Palette**: charcoal ground (`#0B0F14`) + warm bone text (`#F5F1EA`) + amber accent (`#C8A24C`). Deliberately distinct from Bagpipe Golf's brand-green so a portfolio brand doesn't visually double as the parent.
- **Type**: system stack (Inter / SF Pro / etc.). No web-font network hit.
- **Layout**: single column, ~720px max, mobile-first. Renders identically on iPhone + desktop.
- **Sections**: hero → what we do → under the roof (portfolio: Bagpipe Golf card + placeholder "next project") → contact.

## Local preview

Any static file server works. Pick one:

```bash
# Python (already installed on macOS)
cd /Users/bacon/taybuta-website
python3 -m http.server 8000
# open http://localhost:8000

# Or Node's http-server (npm i -g http-server)
http-server -p 8000

# Or just open the file directly — no server needed
open index.html
```

## Deploy to Cloudflare Pages

Two paths — pick whichever matches your workflow:

### Path A — Direct upload (fastest, no git)

1. Cloudflare dash → **Workers & Pages** → **Create application** → **Pages** → **Upload assets**
2. Project name: `taybuta`
3. Drag the `taybuta-website/` folder into the dropzone
4. Deploy — get a `taybuta.pages.dev` URL to test
5. **Custom domain**: Pages project → **Custom domains** → **Set up a custom domain** → `taybuta.com` and `www.taybuta.com`. Cloudflare wires the CNAME automatically since the zone is on the same account.
6. Once the CNAME goes green, taybuta.com serves this page.

### Path B — GitHub + auto-deploy (recommended long-term)

1. `cd /Users/bacon/taybuta-website && git init && git add -A && git commit -m "chore: initial one-page site"`
2. `gh repo create srymer2134/taybuta-website --public --source=. --push`
3. Cloudflare dash → **Workers & Pages** → **Create application** → **Pages** → **Connect to Git** → pick the `taybuta-website` repo
4. Framework preset: **None** (or **Static HTML** if listed)
5. Build command: leave blank
6. Build output directory: `.` (root — this is a flat static site)
7. Deploy. Every push to `main` auto-redeploys.
8. Add custom domain as in Path A.

## Content edits

Everything is in `index.html`. To add a new portfolio card, copy the `.card--coming` block, remove the `--coming` modifier, update fields, and set `href` to the product URL.

Update the meta description + og tags at the top of `index.html` for SEO if you tune the positioning language later.

## When Google Workspace is live for taybuta.com

The site links to `hello@taybuta.com` — once you've added taybuta.com in Google Workspace admin (as secondary or alias domain) and I've added the DKIM/MX cutover, that mailto: will resolve properly. No site change needed.
