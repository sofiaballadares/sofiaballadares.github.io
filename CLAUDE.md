# CLAUDE.md — Personal academic website (Sofía Balladares)

> Project memory for Claude. Read at the start of every session in this repo;
> update the **Current Status**, **Key Decisions** and **Open Issues** sections
> at the end of every session. This repository is **public**, so never write
> anything private here (no unpublished results, no restricted-data details,
> no personal information beyond what is already on the website).

---

## Communication Guidelines

- Refer to the user as **Sofía** (Sofía Balladares, economics PhD student at
  UB/IEB; applied micro, public finance).
- She is not a web developer: explain website changes in plain words, and
  tell her what changed visibly, not just which lines changed.
- No collaborators on this repo. People named on the site (coauthors,
  supervisors, referees) are listed only from public sources: her CV PDF and
  her old Google Site.

---

## Project Overview

Sofía's personal academic website. In economics, the personal site is where
hiring committees, coauthors, conference organisers and journalists look for
a researcher's papers, CV and contact details. It matters most on the job
market at the end of the PhD. The goals are:

1. **Findable**: shows up when someone searches her name; links to and from
   her profiles (UB, IEB, LinkedIn, Bluesky, later Google Scholar, ORCID, RePEc).
2. **Credible at a glance**: a clean, restrained, document-like design in the
   style of economics job-market sites. The reference site she liked is
   Sebastian Ritter's (https://sebastianritterg.github.io/), a fellow UB PhD.
   We copied its *structure*, not its look, so the two sites don't read as
   copies.
3. **Easy to maintain**: plain HTML + one CSS file, no build step, no
   framework. Any page can be edited in a text editor or on github.com.

- **Live site**: https://sofia-bh.github.io (GitHub Pages, user site)
- **Repository**: github.com/Sofia-BH/sofia-bh.github.io (local folder:
  `Documents/GitHub/website`)
- **Old site** (to be retired): https://sites.google.com/view/sofiaballadares/home

### Site map

| Page | File | Contents |
|------|------|----------|
| Home | `index.html` | Intro + photo, profile links, *Recent updates*, *Featured publication*, *At a glance* grid, contact |
| Research | `research.html` | Publications, work in progress, book chapters, reports & policy notes; each item is a card with status label, expandable abstract, topic tags, link chips |
| CV | `cv.html` | Compact HTML résumé, references, download button, embedded PDF |
| Conferences | `conferences.html` | Presentations and organised workshops (dated lists) |
| In the News | `news.html` | Press coverage (Spanish-language articles) |
| 404 | `404.html` | Shown by GitHub Pages for missing URLs (uses absolute `/` paths on purpose) |

---

## Key Files

- **Stylesheet (all pages)**: `assets/css/style.css`. Colours and fonts are
  CSS variables in `:root` at the top.
- **CV PDF**: `assets/pdf/CV_Sofia_Balladares.pdf`. Linked from home and the CV
  page, and embedded in `cv.html`.
- **Photo**: `assets/img/personal_photo.jpg` (800×800). Also used for link
  previews (`og:image`).
- **Favicon**: `assets/img/favicon.svg` ("SB" monogram).
- **Jekyll config**: `_config.yml`. It only excludes this file from the
  published site. Pages have no front matter, so Jekyll copies them unchanged.
- Fonts: Google Fonts *Source Serif 4* (headings) and *Inter* (body). There
  are no other external dependencies.

---

## How to make common updates (recipes)

All pages share an **identical header and footer**. When changing the nav,
footer, email or "Last updated" date, edit **all five pages** (plus nav links
in `404.html`). Only the `aria-current="page"` attribute differs per page.

| Task | What to do |
|------|------------|
| Replace the CV | Overwrite `assets/pdf/CV_Sofia_Balladares.pdf`, keeping the same name. If the content changed, sync `cv.html` (the HTML résumé is written by hand). |
| Add a paper | Copy an `<article class="paper">` block in `research.html`. Status classes: `status-published`, `status-wip`, `status-report`. A template comment at the top of the file shows how to add a figure (`has-figure`). Also update the CV list in `cv.html` and, if relevant, *Featured publication* / *Recent updates* on `index.html`. |
| Add a talk | Add an `<li>` at the top of the list in `conferences.html` (newest first). Add it to *Recent updates* on home if it's recent. |
| Add a press article | Add an `<li>` at the top of `news.html`. |
| Recent updates (home) | Keep 4–6 items, newest first. Remove the oldest when adding. |
| Add Google Scholar / ORCID / RePEc | Uncomment the placeholders in the `profile-links` list in `index.html` and add the URL to the JSON-LD `sameAs` list in the `<head>`. |
| Change email | Search and replace `sofia.balladares@outlook.es` across all `.html` files (header JSON-LD, home contact, every footer). |
| Change site URL / custom domain | Search and replace `https://sofia-bh.github.io` (canonical, `og:` tags, JSON-LD). For a custom domain also add a `CNAME` file and set it under repo Settings → Pages. |
| Publish | `git add -A && git commit -m "..." && git push`. GitHub Pages rebuilds in about 1–2 minutes. Browsers may cache the CV for up to about 10 minutes. |

### Previewing locally
Double-click `index.html`. All links are relative (`research.html`, not
`/research/`), so the site works from the file system. GitHub Pages also
serves extensionless URLs (`/research` → `research.html`).

### Visual check (do this after any layout change)
Render with headless Edge and look at the PNGs (desktop 1280px, phone 375px).
Phone width must show **no horizontal scroll**. Headless Edge clamps very
narrow windows, so test phone width by putting the page in a 375px `<iframe>`
inside a wider harness page, then screenshot that.

```powershell
$edge = "C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe"
& $edge --headless=new --disable-gpu --hide-scrollbars --virtual-time-budget=6000 `
  --window-size=1280,2900 --screenshot="$env:TEMP\home.png" "file:///C:/Users/sofiaballadares/Documents/GitHub/website/index.html"
```

---

## Content sources and verified facts

Every claim on the site comes from one of these sources. **Do not invent
content** (no made-up abstracts, figures, job titles, dates or locations).
If something is missing, leave a commented placeholder and ask Sofía.

| Item | Source / verification (date checked) |
|------|--------------------------------------|
| Bio, research interests | Old Google Site home page, lightly edited (2026-11-06) |
| *Fiscal drag with microsimulation* | Crossref, DOI 10.1111/1475-5890.70021: *Fiscal Studies* 47(2): 113–137, online 9 Apr 2026, print June 2026; authors Balladares & García-Miralles. Abstract from old Google Site. Working-paper version on the IEB site. (2026-11-06) |
| Book chapter | laviedesidees.fr: book *L'Europe : du marché à la puissance publique ?*, É. Monnet & A. Vauchez (dir.), PUF / La Vie des idées, 2024. French chapter title « Des sanctions contre les oligarques à un cadastre financier européen ». The site uses the English title from the old Google Site. (2026-11-06) |
| BdE Occasional Paper 2422; Digital Service Taxes note | Old Google Site + CV PDF hyperlinks (2026-11-06) |
| Talks, workshops, courses, experience, references | CV PDF (version of 2026-11-06) |
| Press articles | Old Google Site *In the news* page (2026-11-06) |
| Profile links (LinkedIn, Bluesky, UB, IEB) | Old Google Site + CV PDF hyperlinks |

---

## Key Decisions Made

| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-11-06 | Plain HTML/CSS instead of a Jekyll theme (academicpages, al-folio) | No build step, nothing to break, works offline, easy to edit by hand or with Claude. Can migrate later if the content outgrows it. |
| 2026-11-06 | Five pages modelled on Sebastian Ritter's site (Home / Research / CV / Conferences / In the News), with our own colours and fonts | Standard job-market structure. A distinct look avoids reading as a copy of a departmental colleague's site. "In the News" replaces his "Blog". |
| 2026-11-06 | Flat files (`research.html`) rather than folders (`research/index.html`) | Links work both on GitHub Pages and when opening files locally. |
| 2026-11-06 | Fiscal drag paper shown as **published** (*Fiscal Studies* 2026), not as a working paper | The CV PDF is outdated on this point; Crossref confirms publication. |
| 2026-11-06 | Email shown: `sofia.balladares@outlook.es` | It is the address on the current CV and survives after the PhD. The old site used the UB address. |
| 2026-11-06 | References listed with emails on `cv.html` | Already public in the CV PDF; standard on job-market sites. Easy to remove. |
| 2026-11-06 | American spelling throughout ("organized") | Matches the CV. |

## Dropped Options

- **Keeping Google Sites**: limited layout control, looks less professional, poor
  SEO and link previews.
- **Copying Sebastian's theme/CSS one-to-one**: it would look like a copy.

---

## Current Status

**Phase**: Built. Pending publication (as of 2026-11-06).

- Five pages, stylesheet, favicon and 404 page are written and visually checked
  at 1280px and 375px.
- Repository not yet pushed to GitHub. URL choice pending (see Open Issues).

## Open Issues / Next Steps

1. **Publish** to GitHub Pages and confirm the live URL works.
2. **Fix the CV PDF** (LaTeX source is not in this repo):
   - List *Fiscal drag with microsimulation* as published: *Fiscal Studies*
     47(2): 113–137 (2026), DOI 10.1111/1475-5890.70021.
   - Typos: "Puclic" → Public; "Sectorial Anlysis" → Sectoral Analysis;
     "Occassional" → Occasional; "LaTex" → LaTeX; "García-Miralles, (2024)" →
     "García-Miralles, E. (2024)".
   - Point the "Personal Website" link to the new URL instead of the Google Site.
   - Book chapter title: the CV says "Effective Sanctions Against Oligarchs…",
     the old site "Sanctions Against Oligarchs…", and the published French title
     is « Des sanctions contre les oligarques à un cadastre financier européen ».
     Pick one English title and use it everywhere. Also confirm the chapter's
     author list against the printed book.
3. **Profiles**: create Google Scholar, ORCID and RePEc/IDEAS. Uncomment the
   links on the home page and update the UB and IEB profile pages, LinkedIn and
   Bluesky so they point to the new site.
4. **Retire the Google Site**: replace its content with a one-line link to the
   new site (keeps old links working) or unpublish it.
5. Optional: personal "a little about me" line (placeholder on home); figures
   for research cards; custom domain (e.g. sofiaballadares.com, ~€10–15/year);
   abstracts for work-in-progress papers once she wants them public.
6. Job market (later): add a "Job Market Paper" section at the top of
   `research.html`, a JMP button in the home hero, and an eyebrow line such as
   "On the economics job market 20XX–XX".

---

## Notes for Claude

- **Verify before you publish facts.** Check new publication details (volume,
  pages, year) against Crossref (`https://api.crossref.org/works/<DOI>`) or the
  publisher, not just the CV, which can lag behind.
- **Never fabricate** abstracts, figures, coauthors or affiliations. Use a
  commented placeholder and ask.
- Keep the header and footer identical on every page. After any visual change,
  run the screenshot check above at desktop and phone widths.
- Use relative links everywhere except in `404.html`.
- Work-in-progress titles are public. Don't add a new project without Sofía's
  explicit OK: some projects use restricted administrative data, and
  coauthors may not want them announced.
- Pushing to `main` publishes immediately. Show Sofía the change (screenshot
  or local preview) before pushing anything substantive.
- Windows machine: use PowerShell or Git Bash. `gh` (GitHub CLI) is **not**
  installed. Git authenticates through Git Credential Manager.
