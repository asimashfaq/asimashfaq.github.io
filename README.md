# Asim Ashfaq — CV

A single-page CV site, in the spirit of [hamzaahmed.dev](https://www.hamzaahmed.dev/).
Plain HTML + CSS — no build step, no framework, no JavaScript.

```
index.html                     the whole CV — edit text here
assets/css/style.css           all styling (design tokens at the top)
assets/files/…-resume.pdf      the PDF behind the "Download CV" button
```

## Preview locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Or just open `index.html` in a browser.

## Editing

**Text** lives in `index.html` and is grouped by section (`Profile`, `Experience`,
`Projects`, `Skills`, `Education`, `Volunteering`, `Languages`, `Quote`).

Six `TODO(Asim)` comments mark the roles still missing bullets — Jarvis, Everreal,
Wefresh, Expanse.tech, Zigron and DHA. The 0xEquity role and every project were
written from the actual repositories; those older roles predate anything on this
machine, so they need your memory:

    grep -n "TODO(Asim)" index.html

**Colours and type** are CSS custom properties at the top of `assets/css/style.css`:

```css
--accent:  #54b689;   /* the green — change this one to re-theme the page */
--text:    #4f4f4f;
--heading: #292929;
```

**Adding a job** — copy an `.item` block inside the Experience section:

```html
<div class="item">
  <div class="item-heading">
    <h3 class="item-title">Job title</h3>
    <span class="item-meta">Company &nbsp;|&nbsp; Location &nbsp;|&nbsp; Dates</span>
  </div>
  <ul class="item-list">
    <li>What you shipped, with a number in it where you can.</li>
  </ul>
</div>
```

**Adding a project** — same `.item` shape, with `<span class="badge">Tech</span>`
tags inside a `.badge-list`.

## Printing

The page has a dedicated print stylesheet — `Cmd/Ctrl+P` gives a clean two-page
A4/Letter PDF with the "Download CV" button and other screen-only chrome removed.

## Deploying

Any static host works, since there is nothing to build.

**GitHub Pages**

```bash
git init && git add . && git commit -m "CV site"
git branch -M main
git remote add origin git@github.com:asimashfaq/asimashfaq.github.io.git
git push -u origin main
```

Then Settings → Pages → Source: `main` / root. Lands at `asimashfaq.github.io`.

**Netlify / Vercel / Cloudflare Pages** — drag the folder in, or point it at the
repo. Build command: none. Publish directory: `/`.

## Credit

The layout follows the [DevResume](http://themes.3rdwavemedia.com) design by
Xiaoying Riley, released under CC BY 3.0. The stylesheet here is written from
scratch (no Bootstrap, no Font Awesome), but the attribution stays in the footer
per that licence.
