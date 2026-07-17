# SETUP — GET THIS LIVE IN ~10 MINUTES

This repo is a complete GitHub profile README in a **neo-brutalist** theme:
hand-written animated SVGs (hero, mission control, terminal, footer, icons),
two GitHub Actions that keep it alive, and dark/light support everywhere.

---

## 1 · Create the profile repository

A profile README only renders from a repo **named exactly like your username**.

```bash
# on GitHub: create a new PUBLIC repo called  Amith-Abey-Stephen
# then, from this folder:
git init
git add .
git commit -m "feat: brutalist profile readme"
git branch -M master
git remote add origin git@github.com:Amith-Abey-Stephen/Amith-Abey-Stephen.git
git push -u origin master
```

> ⚠️ This repo's default branch is **master** — the README raw URLs and
> the workflow push-triggers all reference `master`. If you ever rename
> the default branch, find-and-replace `master` in README.md and
> `.github/workflows/*.yml` too.

> Using a different username? Find-and-replace `Amith-Abey-Stephen` across
> `README.md` and you're done — the workflows use `github.repository_owner`
> automatically.

## 2 · Enable and run the workflows once

The snake images live on the generated `output` branch and will
**404 until the workflow runs once**.

1. Repo → **Actions** tab → enable workflows if prompted.
2. Run **arcade** → *Run workflow*. Creates the `output` branch.
3. Run **blog-posts** → *Run workflow*. Renders the LATEST DROPS cards.

No secrets required — both workflows run on the default `GITHUB_TOKEN`.

## 3 · The blog feed

The blog-posts workflow renders the **3 newest posts as image cards**
(feature image + title + date) from your author-filtered Ghost feed —
`https://blog.inovuslabs.org/author/amith/rss/`. To change the source or
count, edit `FEED` / `MAX_POSTS` at the top of the script inside
`.github/workflows/blog-posts.yml`.

## 4 · Holopin board

Already live in the ACHIEVEMENTS section via `holopin.me/amithabeystephen`.
New badges you claim at [holopin.io](https://holopin.io) appear
automatically — the board image is rendered fresh on every page load.

---

## How the theming works

- Every custom visual ships as a **dark + light SVG pair** (or a single
  self-contained one, like the terminal), switched with:
  ```html
  <picture>
    <source media="(prefers-color-scheme: dark)"  srcset="...-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="...-light.svg">
    <img src="...-dark.svg" alt="...">
  </picture>
  ```
  GitHub natively respects `prefers-color-scheme` in READMEs.
- Third-party widgets get the palette via URL params
  (`border_radius=0`, acid hex colors) — square corners enforced everywhere.
- Palette: `#FFDE00` `#FF90E8` `#ADFF2F` `#00F0FF` `#FF4911` + black/white.

## Why these widgets (2026 audit)

| Widget | Project | Status |
| :-- | :-- | :-- |
| Stats + top languages | `anuraghazra/github-readme-stats` | 65k★, actively maintained |
| Streak | `streak-stats.demolab.com` (DenverCoder1) | maintained (avoid the dead herokuapp URL) |
| Activity graph | `ashutosh00710/github-readme-activity-graph` | maintained |
| Trophies | `ryo-ma/github-profile-trophy` | maintained |
| Holopin board | `holopin.me` | maintained |
| Snake | `Platane/snk` | maintained, v3 |
| Blog cards | custom Python in `blog-posts.yml` | ours — no dependency |
| Badges | `shields.io` | evergreen |

## Repo map

```
README.md                     ← the landing page
SETUP.md                      ← you are here
.github/workflows/
  arcade.yml                  ← snake → `output` branch, daily
  blog-posts.yml              ← RSS → image cards in README, every 6h
assets/
  svg/
    hero-dark.svg             ← animated hero (marquee, typing, stickers)
    hero-light.svg
    mission-control-dark.svg  ← live-ops dashboard
    mission-control-light.svg
    terminal.svg              ← 13s scripted shell session
    footer.svg                ← giant marquee tape
  icons/                      ← 12 animated sticker icons (28×28)
  animations/
    separator.svg             ← crawling hazard tape
```

All animation is CSS keyframes + SMIL inside the SVGs — GitHub's image
proxy (camo) renders both. No JavaScript, no external fonts, no PNGs.
