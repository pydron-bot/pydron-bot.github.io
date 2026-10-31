# deeek.org

The GitHub Pages **user site** for the `pydron-bot` account, served at
https://deeek.org (custom domain in `CNAME`; DNS at GoDaddy: four A records
for `@` → 185.199.108–111.153, CNAME `www` → `pydron-bot.github.io`).

Every other repo on this account with Pages turned on appears under this
domain at `deeek.org/<repo>/`, e.g. **Curbside** at
https://deeek.org/curbside/ (`pydron-bot/curbside`, deployed by its own
GitHub Actions workflow). Don't set a custom domain on those repos; they
inherit this one.

## What's here

Plain static files, no build step:

- `index.html`: the hub page (inline CSS, no JavaScript). Projects are
  posters on a wall; Curbside is the featured one.
- `404.html`: served by Pages for any unknown path at any depth.
- `img/`: screenshots, each as WebP plus a JPEG fallback.
- `og.jpg` (1200×630, the link-preview card), `favicon.svg`, `favicon.ico`,
  `apple-touch-icon.png`.
- `.nojekyll`: serve the files as they are, without Jekyll.

## Adding a project

1. In `index.html`, copy the commented template card at the end of
   `<ul class="posters">` and paste it above the comment, without the comment
   markers. Fill in the copy and leave the template commented out for next
   time. It numbers itself (No. 02, No. 03, …), the "More soon" flyer moves
   along, and a poster left alone on the last row widens to fill it.
2. Replace `NAME` with a short id (it also makes the heading's `id`
   unique) and `REPO` with the repo name, so PLAY goes to `/REPO/` in the
   same tab. Put the project's name in PLAY's hidden text, so screen readers
   hear "Play <name>" rather than several plain "Play" links.
3. Add the screenshot as `img/NAME-480` and `img/NAME-760`, each as `.webp`
   and `.jpg`, 16:9. Keep `width`/`height`, `loading="lazy"` and the `sizes`
   from the template (the featured poster's art is the only image that loads
   eagerly; the photo prints are lazy too).
4. Keep every URL root-absolute (`/img/…`, `/REPO/`), because `404.html`
   shares the look and is served at any depth. Never add a folder named
   after a repo: it would collide with that project's own site.
5. Keep the list hand-written. Generating it from the GitHub API would hit
   rate limits, has no screenshots or pitches, and would list repos that
   aren't web projects.

## Same origin

Every project shares the `https://deeek.org` origin with this hub. That
means one localStorage, one Cache Storage, one IndexedDB and one storage
quota for all of them, and service workers that can overlap. So:

- The hub registers **no service worker**. If one is ever needed, scope it
  narrowly and give it no `navigateFallback`; a root-scoped worker would
  answer a first visit to `/curbside/` before Curbside's own worker
  installs.
- The hub links **no web manifest** at `/`. A manifest with scope `/` would
  pull `/curbside/` into the hub's installed-app window. That's also why PLAY
  opens in the same tab: iOS Add to Home Screen then picks up the game's own
  manifest.
- Nothing here (or in any project) calls `localStorage.clear()`,
  `caches.delete()` on caches it didn't create, or clears site data broadly.
- Each project prefixes its storage keys and cache names with its own name
  (Curbside uses `curbside.*` keys and caches scoped to `/curbside/`).
