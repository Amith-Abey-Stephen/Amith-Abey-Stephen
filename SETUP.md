# SETUP — GET THIS LIVE IN ~10 MINUTES

This repo is a complete GitHub profile README in a **neo-brutalist** theme:
hand-written animated SVGs (hero, mission control, terminal, footer, icons),
three GitHub Actions that keep it alive, and dark/light support everywhere.

---

## 1 · Create the profile repository

A profile README only renders from a repo **named exactly like your username**.

```bash
# on GitHub: create a new PUBLIC repo called  Amith-Abey-Stephen
# then, from this folder:
git init
git add .
git commit -m "feat: brutalist profile readme"
git branch -M main
git remote add origin git@github.com:Amith-Abey-Stephen/Amith-Abey-Stephen.git
git push -u origin main
```

> Using a different username? Find-and-replace `Amith-Abey-Stephen` across
> `README.md` and you're done — the workflows use `github.repository_owner`
> automatically.

## 2 · Enable and run the workflows once

The arcade (snake + pac-man) and metrics images live on generated branches
(`output`, `metrics`) and will **404 until each workflow runs once**.

1. Repo → **Actions** tab → enable workflows if prompted.
2. Run **arcade** → *Run workflow*. Creates the `output` branch.
3. Run **metrics** → *Run workflow*. Creates the `metrics` branch
   (needs the secret from step 3 first).
4. Run **blog-posts** → *Run workflow*. Fills the LATEST DROPS section.

## 3 · Add the metrics token (one secret)

`lowlighter/metrics` needs a read-only classic PAT:

1. GitHub → Settings → Developer settings → Personal access tokens (classic).
2. Generate with scopes: `public_repo`, `read:user`. No expiry drama: pick 1 year.
3. Repo → Settings → Secrets and variables → Actions → **New repository secret**
   - Name: `METRICS_TOKEN`
   - Value: the token.

## 4 · Point the blog feed at yourself

Edit `.github/workflows/blog-posts.yml` → `feed_list`. Any RSS works
(Dev.to, Hashnode, Medium, Ghost, even YouTube). It's pre-filled with
`https://blog.inovuslabs.org/rss/`.

## 5 · Fix the project links

The bento cards in `README.md` link to guessed repo slugs
(`fixmystore-ai`, `expo-shop-mini`, `readrite`, `syncbatch`, `docgen`,
`inomail`, `Project-Dora`). Point each `<a href>` at the real repo or a
live URL, and tune the one-liners/progress bars — they're plain text.

## 6 · Optional: Spotify "ON ROTATION" card

1. Deploy [kittinan/spotify-github-profile](https://github.com/kittinan/spotify-github-profile)
   to your own Vercel (one-click button in their README) and authorize Spotify.
2. It gives you a personal card URL containing your `uid`.
3. In `README.md`, uncomment the **ON ROTATION** block and replace
   `YOUR_SPOTIFY_UID` / `YOUR_SPOTIFY_USERNAME`.

## 7 · Optional: Holopin board

Claim badges at [holopin.io](https://holopin.io), then in `README.md`
uncomment the Holopin block and set your board URL (`holopin.me/<username>`).

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
| Full metrics | `lowlighter/metrics` (terminal template) | maintained |
| Trophies | `ryo-ma/github-profile-trophy` | maintained |
| Snake | `Platane/snk` | maintained, v3 |
| Pac-Man | `abozanona/pacman-contribution-graph` | maintained |
| Blog RSS | `gautamkrishnar/blog-post-workflow` | stable, the standard |
| Badges | `shields.io` | evergreen |

## Repo map

```
README.md                     ← the landing page
SETUP.md                      ← you are here
.github/workflows/
  arcade.yml                  ← snake + pac-man → `output` branch, daily
  metrics.yml                 ← metrics terminal card → `metrics` branch
  blog-posts.yml              ← RSS → README, every 6h
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
