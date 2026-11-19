# Portfolio — how to edit it

Open `index.html` in a browser to view it. Everything you'll want to change lives in **one block** near the bottom of the file, between these two markers:

```
EDIT EVERYTHING IN SECTIONS 1-8 — THAT IS YOUR WHOLE SITE.
...
END OF EDITABLE CONTENT
```

Below that marker is wiring. You shouldn't need to touch it.

## Files in this folder

| File | What it is |
|------|-----------|
| `index.html` | The entire site — HTML, CSS and JS in one file |
| `Gaurangi-Tyagi-Resume.pdf` | Your resume. "View PDF" opens it in a built-in viewer |
| `README.md` | This file |

## The eight sections

| # | Name | What it controls |
|---|------|------------------|
| 1 | `ME` | Name, tagline, email, phone, LinkedIn, GitHub, résumé file, photo, footer line |
| 2 | `BIO` / `TERMINAL` / `EDU` / `SKILLS` / `LEARNING` / `EXPERIENCE` / `CERTS` | The whole About page |
| 3 | `REACH` | Contact page: status line, roles you're open to, closing note |
| 4 | `HEADS` | The big italic heading + subtitle on each of the four pages |
| 5 | `CATS` | The filter buttons on the Work page |
| 6 | `PROJECTS` | The project cards, newest first |
| 7 | `SIDE` | What each object on the desk scene opens |
| 8 | `V` | The SVG illustrations |

## Adding a project

Copy the last block inside `PROJECTS` and change the fields:

```js
{id:'myproject', title:'Title', kind:'Short label', cat:['sql'], year:'Jan 2027', vis:'scatter',
 blurb:'One or two sentences — the question it answered.',
 points:['Bullet one.','Bullet two.'],
 stack:['Python','SQL'], links:[['GitHub','https://github.com/...']]}
```

- `cat` must use keys from `CATS` — currently `dashboards`, `sql`, `stats`, `ml`, `llm`.
- `vis` must be a key in `V`. One spare is ready to use: **`'scatter'`** (green scatter plot). Use `null` for a plain coloured panel with the title on it.
- The project name shows on the thumbnail in a yellow highlighted pill, with the year top-right. No hovering needed.
- Order in the list = order on the page. Newest first.
- `links:[]` (empty) hides the links row entirely — better than a `'#'` link that goes nowhere.

## The resume viewer

`ME.resume` points at `Gaurangi-Tyagi-Resume.pdf`. Clicking **View PDF** on the Contact page opens an in-page viewer with "Open in new tab" and "Download" buttons.

To swap in a newer resume: drop the new PDF in this folder and either name it `Gaurangi-Tyagi-Resume.pdf` (nothing else to change) or update `ME.resume`.

Note: some browsers refuse to preview a PDF inside a page when you open `index.html` straight off your disk (`file://`). It works normally once the site is hosted, and the "Open in new tab" button works either way.

## Certifications

Each entry in `CERTS` can carry a `link:` — when present the name becomes a clickable, verifiable link. Three are wired up already (NPTEL Elite, HackerRank SQL Advanced, Meta on Coursera), taken from your resume. McKinsey Forward and The Big Code have no link because there's no certificate URL yet; add `link:'...'` when you have one.

## The desk scene (Side Quests)

Each clickable object in the SVG carries `data-id="..."`, which looks itself up in `SIDE`:

| Object | id | Opens |
|--------|----|-------|
| Monitor | `aistack` | **AI & Systems** — gallery of five projects (AI Gateway, Task Queue, Failure Forensics, AskData, WhereShouldWe) |
| Clipboard | `howiwork` | **How I Work** — the analysis checklist |
| Easel chart | `oops` | **Things I Got Wrong** — mistakes and what changed |
| Books | `shelf` | **Shelf** — reading list — **placeholder, edit this** |
| Plant | `sqlpractice` | SQL deep dives (Oracle HR schema + HackerRank) |
| Sticky notes | `notes` | nothing — hover says "The to-do pile" |
| Mug | `mug` | nothing — hover says "Always overly caffeinated" |
| Cat | `cat` | nothing — it's asleep |

Certifications, McKinsey Forward and The Big Code used to live here too. They were the same list as `CERTS` on the About page, so the desk was repeating it. Credentials now live **only** in `CERTS`; the desk holds what a resume cannot.

**`shelf` is the one entry you must edit before publishing.** I filled it with four well-known data books and blogs as a shape to work against — replace them with what you have actually read, or the section claims something untrue on your behalf.

### Two kinds of side quest

A normal entry has `points:[...]` and opens a single project modal.

An entry with **`group:[...]`** instead opens a **gallery** first — each project in the group gets a thumbnail, a blurb and its first three bullets, and clicking one opens the full project modal with prev/next arrows. The monitor (`aistack`) is the only one using this today; copy its shape to make another. It holds five projects: three infrastructure builds, then AskData and WhereShouldWe.

An object with **no `SIDE` entry** is hover-only. Give it `data-toast="..."` in the SVG and that text appears as a toast when clicked — that's how the mug and the cat work.

To re-point an object, change its `data-id` in the SVG and add a matching key in `SIDE`.

Every side quest links to a real repo. To add another, pick a desk object, give it `data-id="yourkey"` and add `yourkey:` to `SIDE`.

## Colours

All of them are CSS variables at the very top of the file:

```css
--bg --ink --muted --line --hl --red --pink --yellow --green --peri --plum
```

`--hl` is the yellow highlight used by `<mark>` and the project name pills.

## Publishing it

One file, no build step, so anything that serves static files works:

- **GitHub Pages** — push this folder to a repo, Settings → Pages → deploy from branch. You get `gaurangityagi.github.io/<repo>`.
- **Netlify / Vercel** — drag the folder onto the dashboard.

Push the PDF alongside `index.html` or the resume viewer will 404.

## What's on the site right now

**Projects** (newest first): Freight Rate Prediction · Local Visibility Intelligence · E-commerce Revenue Analytics · Fintech App Review Analysis · Dark Kitchen Opportunity Finder · Telecom Churn Prediction · Customer Segmentation & RFM · Quick-Commerce Delivery Insights · Earnings Surprise Event Study.

Every bullet on those cards comes from the repo's own README. If a README changes, update the card to match.

**Repos deliberately left off:** `Email_expense_tracker` (no README, committed `venv/`), `Sorting-visualizer-python`, `CodeSync` (tutorial-shaped MERN app), `multi_modal_rag` (no README), `Visual-QnA`, `PromptIQ`, `AI-resume-Analyzer`, `Temperature_predictor`, `Water-Potability-Analyzer`, `keep-alive`, `Slack-Salesforce-Integration` and the forks. Mostly they're thin, undocumented, or pull away from the analyst story. Say the word if you want any of them in.

**Why the AI/CS work sits in Side Quests, not Projects:** the Projects page is the one a recruiter judges you on, and its signal is weaker if analyst work has to compete with backend and LLM builds. The desk scene's server rack holds the three strongest engineering repos — AI Gateway, Distributed Task Queue, Failure Forensics — so the range is visible without diluting the analyst story. All three have real READMEs; that's the bar for adding another.
