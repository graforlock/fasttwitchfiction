# Fast Twitch Fiction — Jekyll site

> Necrofiction in the time it takes to flinch.

A static **Jekyll** site for the Fast Twitch Fiction publication, built on the
FTF design system. The horror *stories* live in the magazine; this site is the
**ward** — dispatches, issue notes, calls for specimens, field reports. Each is
a Markdown file, so you (or a CMS) edit content without touching code.

GitHub Pages builds Jekyll natively — push and it goes live.

---

## Run it locally

Requires Ruby + Bundler.

```bash
cd jekyll-site
bundle install
bundle exec jekyll serve --livereload
# → http://localhost:4000
```

## Publish on GitHub Pages

1. Push this `jekyll-site/` content to a repo (it can be the repo root).
2. Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   pick your branch + `/ (root)`.
3. **If it's a project page** (`username.github.io/REPO`), open `_config.yml` and set:
   ```yml
   url: "https://username.github.io"
   baseurl: "/REPO"
   ```
   (For a user/org page `username.github.io`, leave `baseurl: ""`.)
   Every link uses `relative_url`, so this is the only path change needed.

---

## Add a post

Drop a file in `_posts/` named `YYYY-MM-DD-slug.md`:

```markdown
---
title: The Slab Is Open
author: The Host
date: 2026-06-28
category: Dispatch        # free label shown on the tag
tone: body                # body | cosmic | divine | neutral → tag colour
filed: "NO. 004"          # optional filing number on cards/footer
excerpt: One line shown on cards and the home feature.
---

Body in Markdown. The first paragraph gets the oxblood drop cap automatically.

> A blockquote becomes a display-serif pullquote.
> <cite>attribution shows in mono</cite>
```

- **Read time** ("vital sign", `M:SS`) is computed from word count — no field needed.
- The **home page** features the newest post; **/posts/** lists them all; each
  post links to the next.
- For the corrupted **advertisement** register, wrap copy in
  `<div class="ftf-ad"><div class="ftf-ad__kicker">▦ Advertisement</div>…</div>`.

> **Note:** the three posts in `_posts/` are *sample* dispatches written in the
> brand voice to demonstrate the format and registers. Replace or delete them.

---

## Submissions form

`submit.html` runs in **demo mode** by default (shows a confirmation, sends
nothing — a static site has no server). To collect real submissions, paste a
form-backend endpoint into `_config.yml`:

```yml
submit_endpoint: "https://formspree.io/f/yourid"
```

The form then POSTs there. [Formspree](https://formspree.io) emails you each
submission; [Netlify Forms](https://docs.netlify.com/forms/setup/) is the
built-in option if you host on Netlify instead.

## A real CMS (optional)

For an in-browser editor instead of GitHub's file UI:
- **[Decap CMS](https://decapcms.org)** (formerly Netlify CMS) — add `admin/`
  config; edit posts via a `/admin/` dashboard, commits back to the repo.
- **[Prose.io](https://prose.io)** — zero-setup Markdown editor over your repo.

---

## Structure

```
_config.yml          site config, submit endpoint, reading WPM
Gemfile              github-pages gem + plugins
assets/css/ftf.css   the design system as plain CSS (tokens + components)
assets/grain.svg     riso grain texture
_layouts/            default · post · page
_includes/           head · masthead · footer · postcard
_posts/              dispatches (Markdown) — sample content, replace
index.html           home (hero masthead + featured post)
posts.html           the index (/posts/)
submit.html          submissions form
about.html           what necrofiction is
```

## Design system

`assets/css/ftf.css` is a faithful, standalone translation of the FTF design
system (`../tokens`, `../components`) to plain CSS — same tokens, same
print-shadow / bone-and-ink aesthetic, same light/dark theme (`data-theme`
on `<html>`, toggle persists to `localStorage`). Edit tokens at the top of that
file to retune the whole site.

**Fonts** load from Google Fonts (Bodoni Moda / Newsreader / Space Mono). To run
fully offline, self-host the `woff2` files and swap the `<link>` in
`_includes/head.html` for local `@font-face` rules.
