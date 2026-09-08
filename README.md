# Asim Ashfaq: CV

A single-page CV site. Plain HTML and CSS, no build step and no framework.
The only JavaScript is the text-size control in the header.

```
index.html                     the whole CV, edit text here
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

Six `TODO(Asim)` comments mark the roles still missing bullets: Jarvis, EverReal,
Wefresh, Expanse.tech, Zigron and DHA. The 0xEquity role and every project were
written from the actual repositories; those older roles predate anything on this
machine, so they need your memory:

    grep -n "TODO(Asim)" index.html

**Text size.** The header carries A- / Reset / A+ buttons. They set `zoom` on the
card (which reflows, unlike `transform: scale`) and remember the choice in
`localStorage`, guarded so a private window or blocked site data still renders.
The control is `no-print`, so it never reaches the PDF.

**Colours and type** are CSS custom properties at the top of `assets/css/style.css`:

```css
--accent:  #54b689;   /* the green, change this one to re-theme the page */
--text:    #4f4f4f;
--heading: #292929;
```

**Adding a job**: copy an `.item` block inside the Experience section:

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

**Adding a project**: same `.item` shape, with `<span class="badge">Tech</span>`
tags inside a `.badge-list`.

## Printing

`Cmd/Ctrl+P` gives a four-page A4 PDF. The print stylesheet is a separate
design, not a squeezed copy of the page, and four decisions carry it:

- **One column.** The web page is 75/25. In print that fails twice over: Chrome
  will not fragment a flex container across pages (it moves the whole thing to
  the next page, leaving page one empty), and floats fragment but place the
  second column after the first is laid out, so a tall main column pushes the
  aside to page two. One column at full measure also means most bullets cost one
  line instead of two.
- **`break-inside: avoid` on small blocks only.** A section is taller than a
  page, so telling a section not to break forces a break *before* it and
  overflows anyway. Long entries flow across the boundary with `orphans`/`widows`
  holding the shape; only short entries stay whole.
- **Stack tags as text, not pills.** A page of green lozenges reads as
  decoration. The same words at 9.5px read as data.
- **Skills as label plus run.** Eight stacked lists become eight lines.

Projects marked `print-brief` drop their prose in print and keep name and stack;
the web page keeps everything.

## Deploying

Any static host works, since there is nothing to build.

**GitHub Pages**

Already set up and live at **https://asimashfaq.github.io**. To update:

```bash
git add -A && git commit -m "..." && git push
```

Pages rebuilds in under a minute.

**Regenerate the PDF after editing** (it is committed, not built on the fly):

```bash
python3 -m http.server 8000 &
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless \
  --no-pdf-header-footer --print-to-pdf=assets/files/asim-ashfaq-resume.pdf \
  http://localhost:8000/index.html
```

**Netlify / Vercel / Cloudflare Pages**: drag the folder in, or point it at the
repo. Build command: none. Publish directory: `/`.

## Design lineage

The visual language (green accent, uppercase letterspaced headings with a left
rule, white card on a light ground) was modelled on the DevResume template by
Xiaoying Riley. No code from it is used here: the stylesheet is written from
scratch, with no Bootstrap and no Font Awesome, and the icons are inline SVG.
