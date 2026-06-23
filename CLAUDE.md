# HackHPC@ADMI26 — Claude Session Handoff

## What This Project Is

Jekyll/GitHub Pages site for **HackHPC@ADMI26**, a 5-day virtual hackathon (June 22–26, 2026) organized by ADMI, SGX3, and NSF. Teams use Wikipedia as a knowledge graph and compete in one of three innovation tracks. Live at `https://hackhpc.github.io/admi26`.

Working directory: `/Users/jeaimehp/Desktop/admi26-hackhpc/admi26`
Git remote: `HackHPC/admi26` on GitHub — push to `main` triggers automatic GitHub Pages deploy.

---

## Architecture at a Glance

- **No custom layouts** — all pages are standalone HTML files using inline Liquid templating
- **All content lives in `_data/*.yml`** — never hardcode content in HTML
- **All paths use `{{ site.baseurl }}`** — required for GitHub Pages subpath `/admi26`
- **Feature flags in `_config.yml`** control section visibility (see below)
- **CSS variables** drive the entire design system (see Design System section)

---

## Feature Flags (`_config.yml`)

```yaml
show_teams: true         # true → shows Participating Teams section in index.html
show_deliverables: false # true → shows Deliverables cards section in index.html
                         #        and Submission Guidelines in resources.html
```

---

## Data Files (`_data/`)

| File | Purpose |
|------|---------|
| `schedule.yml` | Full 5-day schedule (10 sessions). Each block has date, session, theme, Zoom link, event list, and optional `summary`. Events support `name`, `type`, `description`, `award`, and `links` fields. |
| `organizers.yml` | 6 organizers with bios, avatars, social links |
| `staff.yml` | Staff members + past team data (members, awards, GitHub links) |
| `sponsors.yml` | 3-tier sponsors (Platinum: ADMI, SGX3, NSF; Gold: TACC, projectEUREKA!; Silver: HackHPC) |
| `resources.yml` | 60+ resources in 11 categories (AI Platforms, Computing, Web Dev, etc.) |
| `teams.yml` | Real team data for all 4 competing teams (names, affiliations, majors, emails, LinkedIn URLs, theme songs) |
| `hackathon.yml` | General event metadata |

To add/update schedule events, organizers, staff, resources — **only edit the YAML files**.

### `schedule.yml` session block fields

```yaml
- date: "2026-06-23T16:00:00-04:00"
  session: Afternoon
  zoomlink: "https://..."
  theme: "Afternoon Check-in"
  events: [...]
  summary: |                   # optional — renders as collapsible "Session Summary" dropdown
    Markdown content here...
```

### `schedule.yml` event fields

```yaml
- name: Event Name
  type: Presentations          # displayed in parentheses next to name
  description: >               # rendered as HTML (supports <br> and &nbsp;)
    Free text...
  award: "🏆 Award Name"       # rendered as a gold .award-badge chip below description
  links:
    - title: Link Label
      icon: fa-regular fa-file-pdf
      url: "assets/slide-decks/file.pdf"
      iconcolor: red
```

### `teams.yml` team fields

```yaml
- teamname: Team Name
  awards:
    - "🏆 Award Name"
  background: ""               # optional explicit path to background image; auto-detected from ZoomVirtualBackground.png if blank
  files: "teams/FolderName"    # must match the directory under /teams/
  goal: "..."                  # short project goal description (italic, muted text)
  research_question: "..."     # displayed as a green left-bordered block below goal
  milestones:                  # rendered as custom M# chip + text (not a numbered list)
    - "M1: Description"
    - "M2: Description"
  technologies:
    - name: Tool Name
      url: https://...
      icon: fa-brands fa-python
      description: One-line description shown on hover
  members:
    names: [...]
    affiliation: [...]
    affiliation_url: [...]
    major: [...]
    role: [...]
    socials: [...]             # LinkedIn URLs; empty string for members without one
    email: [...]
  theme_song: "Song Title"     # rendered as gold-background block in plan column, below links, above milestones
  theme_song_url: "https://..." # links the song title
  theme_song_artist: "handle"  # shown as "by handle" in italic
  links:                       # rendered in plan column above theme song and milestones dropdown
    - name: GitHub Repository
      url: https://github.com/...
      icon: fa-brands fa-github
      iconcolor: "#111111"
```

---

## Team Directories (`/teams/`)

Each team has a folder under `/teams/`. Files dropped in are **automatically rendered** on `teams.html`:

Files are rendered in this order: `ZoomVirtualBackground.png` first, then all other images, then audio/video/documents.

| Extension | Rendered As |
|-----------|------------|
| `ZoomVirtualBackground.png` | Always rendered first; card header image on index page team preview |
| `.pdf` | Red PDF icon link |
| `.doc` / `.docx` | Blue Word icon link |
| `.ppt` / `.pptx` | Orange PowerPoint icon link |
| `.xls` / `.xlsx` | Green Excel icon link |
| `.csv` | Green table icon link |
| `.txt` | Gray file-lines icon link |
| `.md` | Markdown icon link |
| `.py` | Python icon link |
| `.ipynb` | Book icon link |
| `.png` / `.jpg` / `.jpeg` / `.gif` / `.svg` / `.webp` | Displayed as inline image |
| `.mp3` / `.wav` / `.ogg` | Embedded audio player |
| `.mp4` / `.mov` / `.webm` | Embedded video player |
| anything else | Generic file icon link |

`.gitkeep` is silently ignored. Current teams and their folder names:

| Team | Folder |
|------|--------|
| The Hacking Tribunal | `teams/TheHackingTribunal/` |
| Origin Zero | `teams/OriginZero/` |
| WinMaxxers | `teams/WinMaxxers/` |
| Capsule Corp CoderZ | `teams/CapsuleCorpCoderZ/` |

---

## Includes (`_includes/`)

| File | Used In | What It Does |
|------|---------|-------------|
| `innovation-tracks.html` | `index.html` | Full descriptions of the 3 hackathon tracks with Marvel examples |
| `deliverables.html` | `index.html` | Collapsible `<details>` listing required team deliverables |
| `teams-section.html` | `index.html` | Preview grid of all teams — clickable cards linking to `teams.html#slug` |
| `navbar.html` | All pages | Site navigation; Teams link is permanent (not behind a feature flag) |
| `sponsors.html` | `index.html` | Sponsors banner |
| `sponsors-sidebar.html` | All inner pages | Sidebar sponsors column |
| `seo.html` | All pages (via `<head>`) | Open Graph + Twitter Card meta tags using `HackHPC_at_ADMI26.jpg` as the share preview image |

---

## Pages

| File | URL | Key Sections |
|------|-----|-------------|
| `index.html` | `/` | Hero → Sponsors → About (Past Events, Teams preview, Innovation Tracks, Key Technologies, Logistics, Deliverables) |
| `schedule.html` | `/schedule` | All sessions from `_data/schedule.yml`; supports `award` per event and `summary` per session block (collapsible dropdown); each block has an `id` set to the slugified theme name for deep linking (e.g. `#final-presentations-awards`); "Add All Sessions to Calendar" button links to the combined ICS file |
| `teams.html` | `/teams` | Full team rows (4-column: identity / members / files / plan); each card has `id` anchor for deep linking |
| `staff.html` | `/staff` | Profile cards from `_data/staff.yml` |
| `organizers.html` | `/organizers` | Profile cards from `_data/organizers.yml` |
| `resources.html` | `/resources` | Collapsible categories from `_data/resources.yml` + session resources from schedule |
| `code-of-conduct.html` | `/code-of-conduct` | Community standards, enforcement, reporting |

---

## Design System (`css/styles.css`)

### CSS Variables
```css
--primary-color: #18A558      /* Green — buttons, headings, accents */
--primary-hover: #0D7A40      /* Dark green — hover states */
--accent-gold: #F4C414        /* Gold — schedule headers, badges */
--accent-gold-dark: #C99800
--danger-color: #D7262B       /* Red — alerts */
--structural-black: #111111   /* Navbar, headings */
--bg-color: #F2F2F2           /* Page background */
--card-bg: #FFFFFF            /* Cards */
--muted-text: #333333         /* Body text */
--light-green: #D9F5E3        /* Section background alternate */
--light-gold: #FFF5CC         /* Dropdown summary backgrounds */
```

### Key CSS Classes
- `.container` — max-width 1200px, centered, `4rem 5%` padding
- `.bg-light` — light green section background
- `.grid` — auto-fit CSS Grid (min 300px columns)
- `.card` / `.profile-card` — card variants
- `.btn-primary` / `.btn-secondary` / `.btn-zoom` — button variants
- `.deliverables-dropdown` — collapsible details pattern (gold summary bar)
- `.schedule-block` / `.schedule-header` / `.event-item` — schedule components
- `.session-summary-dropdown` / `.session-summary-body` — collapsible session summary on schedule page
- `.about-list` — green-tinted list items with bold labels
- `.badge` / `.award-badge` — gold badge chips
- `.past-event-card` / `.past-event-year` / `.past-event-name` / `.past-event-link` — past events grid on index page
- `.teams-preview-grid` / `.team-preview-card` — index page team preview cards
- `.teams-list` / `.team-card-row` — full-width team rows on `teams.html`
- `.team-col-identity` / `.team-col-members` / `.team-col-files` / `.team-col-plan` — columns within a team row
- `.member-list-row` / `.member-chip` — flex-wrap member grid
- `.team-image` / `.team-image-link` — inline image display in team file listings
- `.research-question` — green left-bordered block for team research question
- `.team-theme-song` / `.theme-song-label` / `.theme-song-link` / `.theme-song-artist` — gold-background theme song block in plan column
- `.milestone-item` / `.milestone-label` / `.milestone-text` — M# chip + text milestone rows
- `.team-plan-dropdown` / `.team-milestones` / `.team-tech-list` — plan column components

Mobile breakpoint: `@media (max-width: 768px)`

---

## Innovation Tracks (the hackathon theme)

Teams choose one of three tracks, all centered on Wikipedia as a knowledge graph:

1. **Where Did It Start? (Origin Tracking)** — trace a topic backward to its conceptual/historical origins
2. **What's Next? (Future Event Predictor)** — use past patterns to predict future developments
3. **What If? (Alternative Timeline Analyzer)** — explore how outcomes change if one key event differs

---

## Recent Work (June 22, 2026)

- **Schedule**: Added Session Slide Deck link for Team Introductions (6/22 afternoon); added `award` field support to `schedule.html` and awarded "🏆 Team Introductions Award" to The Hacking Tribunal
- **Teams**: Populated `_data/teams.yml` with all 4 real teams and full member data from registration CSV; renamed WinMaxers → **WinMaxxers**
- **teams.html**: New page with 3-column horizontal layout per team, LinkedIn links per member, and comprehensive auto-file rendering with icons; each card has `id="{{ team.teamname | slugify }}"` for deep linking
- **teams-section.html**: New include for `index.html` — 4-up preview cards using `ZoomVirtualBackground.png` as the card header image, linking to `teams.html#slug`
- **index.html**: Teams preview positioned inside About section, above Innovation Tracks; old inline teams block removed
- **Navbar**: Teams link is now permanent (removed `show_teams` flag guard); active-state highlighting added

## Recent Work (June 23, 2026)

- **Teams — research questions**: Added `research_question` field to all 4 teams in `_data/teams.yml`; rendered as a green left-bordered block below the goal on `teams.html`
- **Teams — GitHub links**: Added `links` entry for The Hacking Tribunal pointing to their GitHub repo; team links moved to the plan column (above Milestones dropdown) rather than the identity column
- **Teams — file ordering**: `teams.html` now renders files in 3 passes — `ZoomVirtualBackground.png` first, then all other images, then audio/video/documents
- **Teams — milestone chips**: Milestones changed from `<ol>` to a `<ul>` with the `M#` prefix extracted and rendered as a small green chip; new CSS classes `.milestone-item`, `.milestone-label`, `.milestone-text`
- **Teams — theme songs**: Added `theme_song`, `theme_song_url`, `theme_song_artist` to all 4 teams in `_data/teams.yml`; rendered in plan column (below GitHub link, above Milestones) as a gold-background block with black music note icon and "Team Theme Song:" label
- **Schedule — Day 2 Afternoon**: Added Session Slide Deck PDF link (`Day2-AfternoonCheckin-HackHPCatADMI26.pdf`) and session `summary` (collapsible dropdown) to the June 23 4:00 PM block
- **Schedule — deep links**: All session blocks now have `id="{{ block.theme | slugify }}"` anchors; Final Presentations event has "Add to Calendar" and "Share Session" links
- **Calendar ICS**: Generated `assets/hackhpc-admi26-schedule.ics` (all 10 sessions) and `assets/hackhpc-admi26-final-presentations.ics` (Final Presentations only); "Add All Sessions to Calendar" button on schedule page
- **SEO**: Created `_includes/seo.html` with Open Graph + Twitter Card meta tags; included in all 7 pages; `HackHPC_at_ADMI26.jpg` is the share preview image
- **Past Events**: Added Past HackHPC@ADMI Events grid (2022–2025) to `index.html` inside the About section, above the Participating Teams preview

---

## Local Dev

```bash
bundle install
bundle exec jekyll serve    # http://localhost:4000/admi26
```

Push to `main` → GitHub Pages auto-deploys. No manual deploy step needed.

---

## Conventions to Follow

1. Edit content in `_data/*.yml`, not in HTML
2. All href/src paths must use `{{ site.baseurl }}/...`
3. New collapsible sections use the `<details>/<summary>` pattern (see `deliverables.html`)
4. New sections added to `index.html` go inside an existing `<section>` or follow the `<section class="container">` pattern
5. New CSS goes in `css/styles.css` using the existing CSS variables — no inline styles except layout one-offs
6. Never commit `_site/`, `.env`, or credentials (`.gitignore` covers this)
7. Test locally with `bundle exec jekyll serve` before pushing
8. To add a team file: drop it in `teams/<FolderName>/` — it auto-renders on `teams.html` with no YAML changes needed
9. To set a team's index card background: name the file `ZoomVirtualBackground.png` and drop it in the team folder
