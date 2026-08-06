# SETUP — GitHub Profile README

This repository contains **Amith Abey Stephen's** GitHub Profile README (`README.md`).

It features a **Sleek Modern Minimalist** design with an animated coding banner, dynamic typing SVG, authentic project showcase, Dracula-themed GitHub stats telemetry, and an automated Ghost blog RSS workflow.

---

## 1 · Profile Repository Setup

A profile README only renders from a repo **named exactly like your GitHub username**:

```bash
# Repo name: Amith-Abey-Stephen/Amith-Abey-Stephen
git add .
git commit -m "refactor: modern minimalist profile readme"
git push origin master
```

---

## 2 · Blog Posts Automation Workflow

The repository includes an automated GitHub Action workflow (`.github/workflows/blog-posts.yml`) that fetches the newest published articles from **[blog.inovuslabs.org](https://blog.inovuslabs.org/author/amith/)** every 6 hours and updates the image cards between the markers:

```html
<!-- BLOG-CARDS:START -->
<!-- Rendered HTML cards -->
<!-- BLOG-CARDS:END -->
```

No external secrets required — the workflow runs using the default `GITHUB_TOKEN`.

---

## 3 · Repository Architecture

```
README.md                     ← Main GitHub profile landing page
SETUP.md                      ← Setup and repository documentation
.github/workflows/
  blog-posts.yml              ← RSS feed → auto-renders blog cards every 6 hours
assets/
  svg/
    terminal.svg              ← Scripted terminal animation SVG
```
