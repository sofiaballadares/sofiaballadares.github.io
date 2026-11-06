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
2. **Credible at a glance**: a classic academic look. The current design is
   modelled on **Javier Feinmann's** site
   (https://javierfeinmann.github.io/JavierFeinmann/), which Sofía chose
   because it looks more academic. That means one page, a navy navbar, a round
   photo next to a short bio, centred section titles between thick rules,
   collapsible paper titles, and talk cards with date badges. The design
   reuses his *layout*, with our own fonts, navy shade and CSS, so it doesn't
   read as a copy. He is in her professional circle (PSE / EU Tax Observatory).
   An earlier multi-page version modelled on Sebastian Ritter's site
   (https://sebastianritterg.github.io/) was replaced the same day.
3. **Easy to maintain**: plain HTML + one CSS file, no build step, no
   framework. The page can be edited in a text editor or on github.com.

- **Live site**: https://sofiaballadares.github.io (GitHub Pages, user site)
- **Repository**: github.com/sofiaballadares/sofiaballadares.github.io (local folder:
  `Documents/GitHub/website`)
- **Old site** (to be retired): https://sites.google.com/view/sofiaballadares/home

### Site map

Everything is on **one page**, `index.html`. The navbar links jump to each
section, and a small inline script underlines the section currently in view.

| Section (anchor) | Contents |
|------------------|----------|
| Home (`#home`) | Round photo, two-paragraph bio, and an info list with icons: email, affiliation, CV (PDF) · LinkedIn · Bluesky |
| Research (`#research`) | *Publications*: collapsible `<details>` rows. The title and a meta line show by default; opening a row shows topic pills, links and the abstract. *Work in Progress*, *Book Chapters* and *Reports and Policy Notes* are plain lists. |
| Conferences & Workshops (`#conferences`) | *Presentations* and *Organization*, shown as event cards with a navy month/year badge and a kind label |
| In the News (`#media`) | Press coverage (Spanish-language articles) |
| CV (navbar) | Opens the PDF directly. There is no HTML CV page. |

`404.html` is shown by GitHub Pages for missing URLs. It uses absolute `/`
paths on purpose, so it looks unstyled when opened locally.

---

## Key Files

- **The page**: `index.html`. Each section has a `HOW TO ADD ...` comment with
  the block to copy.
- **Stylesheet**: `assets/css/style.css`. Colours and fonts are CSS variables
  in `:root` at the top.
- **CV PDF**: `assets/pdf/CV_Sofia_Balladares.pdf`. Linked from the navbar, the
  intro info list and the footer.
- **Photo**: `assets/img/personal_photo.jpg` (800×800). Also used for link
  previews (`og:image`).
- **Favicon**: `assets/img/favicon.svg` ("SB" monogram).
- **Jekyll config**: `_config.yml`. It only excludes this file from the
  published site. Pages have no front matter, so Jekyll copies them unchanged.
- Fonts (Google Fonts): *Cormorant Garamond* for the name in the navbar,
  *Source Serif 4* for section titles, *Source Sans 3* for body text. There are
  no other external dependencies: no Bootstrap, and no JavaScript beyond the
  small inline nav-highlight script.

---

## How to make common updates (recipes)

If the navbar changes, also update the nav links in `404.html`.

| Task | What to do |
|------|------------|
| Replace the CV | Overwrite `assets/pdf/CV_Sofia_Balladares.pdf`, keeping the same name. |
| Add a paper | Copy a `<details class="paper">` block into the right subsection of `#research`. Put the title and one meta line (coauthors · venue) in `<summary>`; put pills, links and abstract in `.paper-body`. For a new subsection (e.g. "Working Papers", or a "Job Market Paper" at the top), add an `<h3 class="sub-title">` and a `<div class="papers">`. |
| Add work in progress | Add an `<li>` to the *Work in Progress* `ref-list`: `<span class="t">Title</span> <span class="m">(with …)</span>`. |
| Add a talk | Copy an `<li class="event-card">` to the top of *Presentations* (newest first). Set the month and year in the badge and the kind label (`Conference`, `Workshop`, `Seminar`, `Poster`). |
| Add a press article | Add an `<li>` at the top of the `#media` list. |
| Add Google Scholar / ORCID / RePEc | Uncomment the placeholders in the intro `info` list. Also add them to the footer links and to the JSON-LD `sameAs` list in the `<head>`. |
| Change email | Search and replace `sofia.balladares@outlook.es` in `index.html` (JSON-LD, intro info list, footer). |
| Change site URL / custom domain | Search and replace `https://sofiaballadares.github.io` (canonical, `og:` tags, JSON-LD). For a custom domain also add a `CNAME` file and set it under repo Settings → Pages. |
| Publish | `git add -A && git commit -m "..." && git push`. GitHub Pages rebuilds in about 1–2 minutes. Browsers may cache the CV for up to about 10 minutes. |

### Previewing locally
Double-click `index.html`. All its links are relative or `#anchors`, so it
works from the file system.

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
| 2026-11-06 | **Redesign: single page modelled on Javier Feinmann's site**, replacing the five-page Sebastian Ritter-style version | Sofía found parts of the first version less academic, especially the "At a glance" cards. We dropped *At a glance*, *Recent updates*, the featured-paper card, button-style contact links and the HTML CV page. The old `research.html`, `cv.html`, `conferences.html` and `news.html` were deleted; they had been live for under an hour. |
| 2026-11-06 | Same layout as Feinmann, but our own fonts (Cormorant Garamond / Source Serif 4 / Source Sans 3), navy `#0f1f3d` and hand-written CSS (no Bootstrap) | Close enough to read as the same academic style, distinct enough not to look copied. |
| 2026-11-06 | Papers as `<details>` rows, collapsed by default, with coauthors and venue visible in the row | His accordion look, without JavaScript. Visitors see coauthors and journal without clicking. |
| 2026-11-06 | Fiscal drag paper shown as **published** (*Fiscal Studies* 2026), not as a working paper | The CV PDF is outdated on this point; Crossref confirms publication. |
| 2026-11-06 | Email shown: `sofia.balladares@outlook.es` | It is the address on the current CV and survives after the PhD. The old site used the UB address. |
| 2026-11-06 | American spelling throughout ("organized") | Matches the CV. |
| 2026-11-06 | Address `sofiaballadares.github.io`: GitHub account renamed from `Sofia-BH` to `sofiaballadares` | Name-based URL matches her Bluesky handle. Decided before the URL goes on the CV, because GitHub does not redirect a renamed user's `*.github.io` site. Her other repos' remotes (`github.com/Sofia-BH/...`) keep working through GitHub's redirects but should eventually be updated. |

## Dropped Options

- **Keeping Google Sites**: limited layout control, looks less professional, poor
  SEO and link previews.
- **Copying Sebastian's or Javier's theme/CSS one-to-one**: it would look like a copy.
- **Multi-page "job-market dashboard" style** (first version: At a glance grid,
  Recent updates box, featured-paper card, HTML CV page): Sofía found it less
  academic. Don't reintroduce card grids or dashboard-like summaries.

---

## Current Status

**Phase**: Live at https://sofiaballadares.github.io (published 2026-11-06).

- Single-page design (Feinmann style) built, visually checked at 1280px and
  375px, and pushed (2026-11-06).
- GitHub account renamed `Sofia-BH` → `sofiaballadares`. Public repo
  `sofiaballadares/sofiaballadares.github.io` created and pushed. Pages builds
  from `main` / root with HTTPS enforced. All pages, the CV PDF and the photo
  return 200 on the live site; `CLAUDE.md` and `_config.yml` return 404, as
  intended. The live render matches the local one.

## Open Issues / Next Steps

1. **Other local repos** still have remotes at `github.com/Sofia-BH/...`. These
   work through GitHub's redirect, but should be updated with
   `git remote set-url origin https://github.com/sofiaballadares/<repo>.git`
   (only Sofía's own repos; `ES_LeyBeckham` belongs to dirkforemny).
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
5. Optional: personal "a little about me" line (placeholder in the bio); an
   office address in the intro info list (as Feinmann has); a figure inside an
   opened paper row; custom domain (e.g. sofiaballadares.com, ~€10–15/year);
   abstracts for work-in-progress papers once she wants them public.
6. Job market (later): add a "Job Market Paper" subsection at the top of
   `#research`, opened by default (`<details open>`). Mention it in the bio's
   first line ("I am on the 20XX–XX job market").

---

## Notes for Claude

- **Verify before you publish facts.** Check new publication details (volume,
  pages, year) against Crossref (`https://api.crossref.org/works/<DOI>`) or the
  publisher, not just the CV, which can lag behind.
- **Never fabricate** abstracts, figures, coauthors or affiliations. Use a
  commented placeholder and ask.
- After any visual change, run the screenshot check above at desktop and
  phone widths.
- Use relative links and `#anchors` everywhere except in `404.html`.
- Work-in-progress titles are public. Don't add a new project without Sofía's
  explicit OK: some projects use restricted administrative data, and
  coauthors may not want them announced.
- Pushing to `main` publishes immediately. Show Sofía the change (screenshot
  or local preview) before pushing anything substantive.
- Windows machine: use PowerShell or Git Bash. `gh` (GitHub CLI) is **not**
  installed. Git authenticates through Git Credential Manager.
