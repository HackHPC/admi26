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
show_teams: false        # true → shows Participating Teams section in index.html
show_deliverables: false # true → shows Deliverables cards section in index.html
                         #        and Submission Guidelines in resources.html
```

---

## Data Files (`_data/`)

| File | Purpose |
|------|---------|
| `schedule.yml` | Full 5-day schedule (10 sessions). Each block has date, session, theme, Zoom link, and event list |
| `organizers.yml` | 6 organizers with bios, avatars, social links |
| `staff.yml` | Staff members + past team data (members, awards, GitHub links) |
| `sponsors.yml` | 3-tier sponsors (Platinum: ADMI, SGX3, NSF; Gold: TACC, projectEUREKA!; Silver: HackHPC) |
| `resources.yml` | 60+ resources in 11 categories (AI Platforms, Computing, Web Dev, etc.) |
| `teams.yml` | Sample team data for feature testing (`show_teams`) |
| `hackathon.yml` | General event metadata |

To add/update schedule events, organizers, staff, resources — **only edit the YAML files**.

---

## Includes (`_includes/`)

| File | Used In | What It Does |
|------|---------|-------------|
| `innovation-tracks.html` | `index.html` via `{% include innovation-tracks.html %}` | Full descriptions of the 3 hackathon tracks with Marvel examples |
| `deliverables.html` | `index.html` via `{% include deliverables.html %}` | Collapsible `<details>` listing required team deliverables |

Both follows the same `<details class="*-dropdown">` collapsible pattern.

---

## Pages

| File | URL | Key Sections |
|------|-----|-------------|
| `index.html` | `/` | Hero, About, Innovation Tracks (include), Key Technologies, Logistics, Deliverables (include), conditional Teams section |
| `schedule.html` | `/schedule` | All sessions from `_data/schedule.yml` |
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
- `.card` / `.team-card` / `.profile-card` — card variants
- `.btn-primary` / `.btn-secondary` / `.btn-zoom` — button variants
- `.deliverables-dropdown` — collapsible details pattern (gold summary bar)
- `.schedule-block` / `.schedule-header` / `.event-item` — schedule components
- `.about-list` — green-tinted list items with bold labels
- `.badge` / `.award-badge` — gold badge chips

Mobile breakpoint: `@media (max-width: 768px)`

---

## Innovation Tracks (the hackathon theme)

Teams choose one of three tracks, all centered on Wikipedia as a knowledge graph:

1. **Where Did It Start? (Origin Tracking)** — trace a topic backward to its conceptual/historical origins
2. **What's Next? (Future Event Predictor)** — use past patterns to predict future developments
3. **What If? (Alternative Timeline Analyzer)** — explore how outcomes change if one key event differs

---

## Recent Work (last session)

- Added `_includes/innovation-tracks.html` with full track descriptions (Marvel examples, question prompts, quick summary)
- Replaced inline Innovation Tracks content in `index.html` with `{% include innovation-tracks.html %}` — same pattern as `{% include deliverables.html %}`
- The include sits inside the About section (`<section id="about" class="container">`) between the intro paragraphs and Key Technologies

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
