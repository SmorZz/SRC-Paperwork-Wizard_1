# SRC Paperwork Wizard

An interactive paperwork guide for the Central Bucks High School South STEM Research Club (SRC),
covering the BCSRC and PJAS Region 1C packets for the 2026–2027 season.

A member answers eleven questions about their project. The site works out exactly which forms
they owe, in what order, which ones need approval *before* experimentation, and which start date
applies to them — then walks them through filling in every page, with a blank scan and a
completed sample of each form, and finishes with how to physically assemble and hand in the folder.

## The hard dates

| | |
|---|---|
| **Paperwork due to Mrs. Rhodes** | **Thursday, November 13, 2026 — no exceptions** |
| Start date, project needs SRC / IRB / IACUC / IBC approval | 12/23/2026 |
| Start date, no prior approval needed | 12/01/2026 |

Paperwork still filled in incorrectly after November 13 makes a member ineligible to compete
within the club. Paperwork not complete and submitted by November 13 results in dismissal from
the club. Every signature on Forms 1, 1B and 3 must be dated on or before the start date.

## How the folder is handed in

1. BCSRC pages in order, BCSRC Paperwork Checklist on top, held with a **paperclip**.
2. PJAS pages in order, PJAS Submission Checklist on top, held with its own **paperclip**.
3. Both bundles in one **manila folder**.
4. Member's name on the **top lip of the paperwork checklist**.
5. Two sign-offs on the top sheet: the member's **mentor** and **one other club member**,
   each printing their name, signing, and dating it.

## What's here

| Path | What it is |
|---|---|
| `index.html` | The whole site. No build step, no dependencies, no server. |
| `img/logo.png` | The club logo. |
| `img/*__blank.png` | Each official form exactly as you download it. |
| `img/*__filled.png` | The same form completed, from the John Doe sample packets. |
| `img/d_*.png` | Close-ups of the parts people get wrong. |

Fonts load from Google Fonts. Everything else is local.

## Publishing it with GitHub Pages

1. Create a new repository and upload this folder's contents to the root of the `main` branch.
2. Go to **Settings → Pages**.
3. Under **Source**, pick **Deploy from a branch**, then branch `main` and folder `/ (root)`.
4. Save. The site goes live at `https://<your-username>.github.io/<repo-name>/` in a minute or two.

## Running it locally

Open `index.html` in a browser, or serve the folder with `python3 -m http.server 8000`.

## Colours

The palette is sampled from the club logo and its artwork, and is defined once as CSS custom
properties on `:root` near the top of the file, with dark-mode values repeated in the two
following blocks.

| Source colour | Used for |
|---|---|
| `#006CC0` logo blue | accent, links, buttons |
| `#303078` indigo outline | body text and headings |
| `#48C0E4` sky | accent in dark mode |
| `#FCCC60` gold | "conditional" tags and info callouts |
| `#FC7890` coral | deadlines, warnings, "do not fill this in" |
| `#24B490` teal | completed steps and progress |

## Updating the content

All the content lives in two arrays near the top of the `<script>` block in `index.html`:

- `QS` — the questionnaire. Each entry has the question, help text, optional examples,
  an "unsure" line, and an optional `showIf` so a question only appears when it is relevant.
- `FORMS` — one object per form: which fair it belongs to, when it is required (`when`),
  who fills in each part (`roles`), its images, its checklist (`checks`), and its callouts (`notes`).

A checklist line can be conditional. `["Worksite addresses are listed.", "rri"]` only shows for
members who said they work at an outside lab; `"srcyes"` and `"srcno"` switch on whether the
project needs prior approval. The condition names are handled in `lineOn()`.

Write `{START}` anywhere in a checklist line, lede, or note and it is replaced with that member's
start date. The two dates live in `startDate()`, and `needsSRC()` decides which one applies.
The submission deadline lives in `DEADLINE`.

`UNIVERSAL` holds the ground rules shown before everything else, and `PREAPPROVAL` lists the
forms that trigger the red "approval before experimentation" banner.

## Accuracy

Sample pages are marked SAMPLE and use invented names, addresses, and medical details.
Blank pages are the official forms as distributed. Where this site and the current ISEF
*International Rules & Guidelines* disagree, the rules win — check with the club advisor.

PJAS meet dates and registration deadlines are deliberately not in the site, because they change
every year. The club dates above are set in `DEADLINE` and `startDate()`.
