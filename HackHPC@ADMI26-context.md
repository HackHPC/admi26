# Project overview

HackHPC@ADMI26 is a public GitHub Pages-hosted hackathon website for the ADMI26 event, built with Jekyll. The site is a live event hub that presents schedules, organizers, staff, resources, and event details through data-driven YAML configuration.

## Goals and scope

- Provide a dynamic, maintainable hackathon website for HackHPC@ADMI26.
- Surface event schedule, staff, organizers, resources, and team information through editable YAML files in `_data/`.
- Keep the site fully compatible with GitHub Pages build constraints.
- Prioritize a responsive mobile-first user experience across all core pages.
- Support eventual enhancements such as dark mode, multi-language content, Zoom meeting integration, `.ics` calendar download, and participant deliverable tracking.

## Technical environment

- Static site generated with Jekyll.
- Hosted on GitHub Pages.
- Uses Ruby/Bundler with a `Gemfile` pinned for GitHub Pages compatibility.
- Frontend styling is managed in `css/styles.css` with modern CSS conventions.
- No server-side runtime logic; all content is rendered at build time.

## Architecture and design decisions

- Content is data-driven: event content must be managed via `_data/*.yml` rather than hardcoded HTML.
- Core pages (`index.html`, `schedule.html`, `staff.html`, `organizers.html`, `resources.html`, `code-of-conduct.html`) are rendered from site templates plus YAML data.
- `_config.yml` stores reusable site-wide configuration values such as asset paths and registration URL.
- The site uses `site.baseurl` for URL handling and asset references to support GitHub Pages path requirements.
- Layouts are lightweight HTML pages rather than complex theme scaffolding, keeping build compatibility simple.

## Repository and file structure

- `_config.yml` — Jekyll configuration and site-level variables.
- `_data/` — structured source data driving pages.
  - `organizers.yml`
  - `schedule.yml`
  - `sponsors.yml`
  - `teams.yml`
  - `resources.yml`
  - `staff.yml`
- `assets/` — static images and other binary assets.
- `css/styles.css` — global site styles.
- `index.html` — homepage with summary, about content, and navigation.
- `schedule.html` — dedicated schedule page rendered from `_data/schedule.yml`.
- `organizers.html` — organizers page rendered from `_data/organizers.yml`.
- `staff.html` — staff page rendered from `_data/staff.yml`.
- `resources.html` — resources page with categorized YAML resources and session-specific links derived from `schedule.yml`.
- `code-of-conduct.html` — static policy page.
- `JEKYLL_BUILD_GUIDE.md` — local build instructions.
- `Gemfile` / `Gemfile.lock` — Ruby dependency management.
- `.gitignore` — excludes generated build output and local artifacts.

## Current status

- Core site pages are live and data-driven from `_data/*.yml`.
- Added a dedicated `_data/staff.yml` and updated `staff.html` to render staff profiles from it.
- Created `_data/resources.yml` and built `resources.html` to render categorized resource lists.
- `resources.html` now also includes session-specific links extracted from `schedule.yml`.
- Resource categories are collapsible and resource titles are direct links to their pages.
- Added `.gitignore` and untracked generated `_site/` content from the repository.
- Added `Gemfile`, `Gemfile.lock`, and `JEKYLL_BUILD_GUIDE.md` for GitHub Pages-compatible local development.
- The site uses centralized registration link configuration in `_config.yml` and consistent `site.baseurl` path handling.
- Brand palette styling is applied via `css/styles.css`.

## Open issues and TODOs

- Mobile-first refactoring across all pages and data loops.
- Implement native dark mode.
- Add multi-language support.
- Integrate Zoom meeting coordinates into schedule pages and/or session details.
- Generate and link downloadable `.ics` calendar files.
- Build participant deliverable/submission tracking functionality.
- Avoid hardcoded HTML content; ensure new content is added through `_data/*.yml`.
- Keep the site compatible with GitHub Pages and avoid unsupported plugins.

## Conventions and constraints

- Always update `_data/*.yml` files for event content changes.
- Keep HTML pages lean and use Liquid loops/conditionals for data rendering.
- Use `{{ site.baseurl }}` for paths and `{{ site.registration_url }}` for registration links.
- Maintain public-safe content: do not commit secrets, private keys, or sensitive personal data.
- Prefer modern clean CSS; SCSS is acceptable if it remains build-compatible with GitHub Pages.
- Do not include generated `_site/` artifacts in version control.

## How to resume work

Continue by focusing on mobile-first layout and responsive behavior for the existing pages. Verify that pages render from `_data/` instead of hardcoded content, then extend the site with dark mode, language support, Zoom links, and calendar export features. Maintain GitHub Pages compatibility and keep the repo public-safe.
