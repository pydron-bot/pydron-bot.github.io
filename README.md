# deeek.org

The GitHub Pages **user site** for the `pydron-bot` account, served at
https://deeek.org (custom domain in `CNAME`; DNS at GoDaddy: four A records
for `@` → 185.199.108–111.153, CNAME `www` → `pydron-bot.github.io`).

Every other repo on this account with Pages turned on appears under this
domain at `deeek.org/<repo>/` — e.g. **Curbside** at
https://deeek.org/curbside/ (`pydron-bot/curbside`, deployed by its own
GitHub Actions workflow). Don't set a custom domain on those repos; they
inherit this one.

## To do

- Replace the placeholder `index.html` with a proper landing page: a hub for
  all projects (Curbside first, with a screenshot, a one-line pitch and a
  "Play" button), room for more projects as they land, works on phones and
  desktop. Plain static HTML/CSS is enough; no build step needed unless one
  is wanted later.
