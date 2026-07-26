# Subodh Deshmukh — Personal Portfolio Website
### Full Project Documentation

**File:** `index.html`
**Type:** Single self-contained HTML file — no build step, no external dependencies except Google Fonts
**Theme:** "Dark Luxury Editorial" — near-black + gold palette, with a full light-mode counterpart
**Current size:** ~985 KB (large because the profile photo, resume PDF, and several brand logos are embedded directly in the file as base64 data — see [Embedded Assets](#embedded-assets) below)

---

## 1. What This Is

A single-page personal portfolio site for Subodh Deshmukh, positioned as an **Enterprise Product Leader** rather than around one specific job title (see [Positioning Decisions](#8-positioning--content-decisions) for why). It's built to be:

- **Portable** — one `.html` file. Copy it anywhere, open it in any browser, no server or build tooling required.
- **Self-contained** — the profile photo, downloadable resume PDF, and company/certification logos are all embedded as base64 data URIs directly in the file. Nothing external to load except two Google Fonts.
- **Themeable** — a working dark/light toggle, persisted across visits.
- **Fact-checked against real sources** — every number and claim on the site was cross-referenced against the user's actual resume (PDF + DOCX), LinkedIn export, and a real 2025 performance review document. Nothing was invented.

---

## 2. Tech Stack

| Layer | Technology |
|---|---|
| Structure | Semantic HTML5 |
| Styling | Vanilla CSS3 — CSS custom properties (variables) for theming, CSS Grid for layout, no framework |
| Interactivity | Vanilla JavaScript (IIFE, no libraries, no build step) |
| Fonts | Google Fonts: **Playfair Display** (serif, headings) + **DM Sans** (sans, body) |
| Icons | Hand-authored inline SVG (no icon font/library) |
| Images | Embedded as base64 `data:` URIs (photo, resume PDF, brand logos) |
| Hosting target | Static file — works on GitHub Pages, Netlify, or literally opened from disk |

No npm, no React/Vue/Next.js, no CSS preprocessor. Everything lives in one `<style>` block and one `<script>` block inside `index.html`.

---

## 3. Design System

### 3.1 Color Palette

The site ships with **two full themes**, toggled via a sun/moon button in the navbar (top right), persisted in `localStorage`, and defaulting to the visitor's OS-level light/dark preference on first visit.

**Dark theme (default):**
| Token | Value | Use |
|---|---|---|
| `--bg` | `#0A0A0B` | Page background — near-black |
| `--surface` | `#141416` | Card backgrounds |
| `--surface-2` | `#1B1B1E` | Card hover state |
| `--gold` | `#C9A961` | Accent — labels, links, dividers, highlights |
| `--gold-dim` | `#8f7d4d` | Secondary gold (muted accents) |
| `--text` | `#F4F1EA` | Primary text — warm off-white |
| `--muted` | `#8A8A8E` | Secondary/body text |

**Light theme** (`[data-theme="light"]`):
| Token | Value | Use |
|---|---|---|
| `--bg` | `#F6F2E9` | Warm cream background |
| `--surface` | `#FFFFFF` | Card backgrounds |
| `--surface-2` | `#EFE8D8` | Card hover state |
| `--gold` | `#A9772E` | Darker gold — tuned for contrast on light backgrounds |
| `--text` | `#231F18` | Near-black warm text |
| `--muted` | `#6B6255` | Secondary text |

All gradients, overlays, and translucent backgrounds reference `--bg-rgb` / `--text-rgb` / `--surface-rgb` (companion RGB-triplet variables) so `rgba()` effects adapt automatically when the theme switches — nothing is hardcoded to one theme.

### 3.2 Typography

- **Headings:** Playfair Display (serif) — large, confident, used for all `h1`–`h4`, pull quotes, and the hero name.
- **Body/UI:** DM Sans (sans-serif) — body copy, nav, buttons, labels.
- **Section labels** (e.g. "01 — About") are small, uppercase, letter-spaced gold text with a short gold rule before them — a recurring motif through the whole site.

### 3.3 Motion & Interaction Principles

- **Scroll reveal:** every major element fades in + translates up slightly as it enters the viewport (`IntersectionObserver`-driven), with staggered delays (`.reveal-delay-1` through `-6`) for sequential reveal within a section.
- **Restraint over gimmick:** animations are subtle (opacity/transform only), respect `prefers-reduced-motion` (marquee and constellation twinkle are disabled for users who request it).
- **Hero parallax:** the hero photo shifts a few pixels opposite the cursor on desktop pointer devices (`hover:hover` + `pointer:fine` media query guarded — doesn't fire on touch).
- **Card tilt + glow:** Platform Portfolio cards tilt slightly in 3D (`perspective` + `rotateX/rotateY`) following the cursor, with a soft gold radial glow that tracks pointer position via CSS custom properties (`--mx`, `--my`) set from JS.
- **Marquee:** a continuously scrolling strip of platform names beneath the hero, built with duplicated content + `translateX(-50%)` for a seamless loop.
- **Animated counters:** the Impact section's numbers count up from 0 when scrolled into view, using `requestAnimationFrame` and an ease-out curve.

---

## 4. Page Structure (Section by Section)

The site is a single scrolling page with 12 sections, each independently anchorable via the nav:

### 01 — Hero
Split-screen layout: name + positioning statement on the left, a large duotone (grayscale/sepia-treated) portrait photo on the right with a faint animated "constellation" of gold dots and connecting lines (a subtle nod to the "Interstellar" and "DAX Constellation" awards). Includes:
- Eyebrow: "Enterprise Product Leadership"
- Positioning line: *"Platform Strategy · Product Leadership · AI-First Delivery"* (deliberately role-neutral — see §8)
- Three stat chips: **9+ Years Experience**, **$1M+ Business Impact at Data Axle**, **$3M Client Savings at Genpact**
- CTAs: LinkedIn, Email, **Download Resume** (links directly to the embedded resume PDF)
- A horizontal marquee strip of all 8 platform names scrolls continuously beneath the hero

### Pull Quote
A standalone full-width banner: *"I'm not the loudest in the room — but the platforms I build don't go unnoticed."* — pulled verbatim from the user's own LinkedIn summary, used as a signature personal-brand line.

### 01 — About
Narrative bio (path: consulting → product management → platform ownership), plus a side panel with:
- A **contact detail list** (Location, Email, Phone, Languages, Availability)
- Three highlight cards: *Consulting → Product → Platform*, *AI-Native Workflow*, *Recognized Impact*

### 02 — What I Do
A 6-card icon grid of core competency areas (not literal "services," since this isn't a freelancer site): Platform Strategy, Zero-to-One Launches, Cross-Functional Leadership, AI-First Delivery, Enterprise Integration, Stakeholder Management. Each has a custom hand-drawn line-icon.

### 03 — Career Journey
A vertical timeline, **most recent role first** (descending order):
- A **"Companies" logo strip** (Data Axle, Genpact, and a MUVI text wordmark) sits above the timeline
- **Data Axle, Pune** (Jul 2023–Present): Lead Product Manager ← Senior Product Manager ← Product Manager, with a reversed promotion sub-timeline
- **Muvi.com** (Oct 2022–May 2023): Product Manager
- **Genpact, Hyderabad** (Apr 2018–Oct 2022): Lead Product Consultant ← Product Consultant

### 04 — Platform Portfolio
An asymmetric **bento-grid** layout (not a uniform grid) with a subtle isometric-style decorative gold line pattern behind it:
- **Custom Approval System** — large featured tile (2×2)
- **Salesforce CRM** — wide tile (2×1), with the real Salesforce logo
- Oracle ERP (real Oracle logo), AI-Powered Sales Retention Platform, Genesys Telecom/SMS Channel (real Genesys logo), Order Management & Billing, Shared Services Platform, Payment Gateway Platform
- Cards have cursor-tracking 3D tilt + gold glow on hover

### 05 — Impact & Awards
Left: four animated counters (icons + numbers) — **$3M** Genpact savings, **$1M+** Data Axle impact, **8+** platforms owned, **50–55** stakeholders managed.
Right: a full awards list with star icons — including the **2025 performance rating (4/4, "Sets a New Standard")**, Interstellar of the Year, Leading by Example, Special Gold Contributor, Badge of Honour, and three Genpact excellence awards.

### 06 — Recognition
- A **featured quote** from Prasad Udupi (People Manager, Data Axle), pulled from the user's real 2025 performance review
- A **4-card grid** of genuine LinkedIn recommendations from Jason Doss, Suresh Simson, Alberto Betti, and Anshuman Das

### 07 — Speaking & Community
Two cards: Product Leaders Forum (Apr 2026) and Institute for Product Leadership.

### 08 — Beyond Work
A bento grid (wide/narrow zigzag) covering Cricket (wide), Karate, Writing (poetry, merged with language fluency), and **QueueFinder** (wide) — a real 2020 COVID-19 relief initiative pulled from the LinkedIn export, not previously on the site.

### 09 — Education & Certifications
Education history, a certifying-body logo row (Scrum Alliance, Anthropic), and a certification pill cloud (10 certifications), plus a three-column Skills grid (Product / AI Tooling / Technical) each with its own icon.

### 10 — Contact
Large serif close-out line ("Let's build something that scales"), with email/phone/LinkedIn/location and a footer.

---

## 5. Interactive Features Checklist

- [x] Sticky navbar with active-section highlighting on scroll
- [x] Mobile hamburger menu (slide-in panel)
- [x] Dark/light theme toggle, persisted via `localStorage`, respects OS preference on first load, no flash-of-wrong-theme (early inline script sets the attribute before first paint)
- [x] Scroll-triggered fade/translate reveals throughout
- [x] Animated count-up statistics
- [x] Hero photo parallax on mouse move (desktop only)
- [x] Twinkling constellation dots/lines over the hero photo
- [x] Continuously scrolling platform-name marquee
- [x] 3D tilt + cursor-tracking glow on Platform Portfolio cards
- [x] Smooth-scroll navigation
- [x] Fully responsive: tested at 375px (mobile), 768px (tablet), 1440px (desktop)

---

## 6. Embedded Assets

Because this is a *single-file* site, all binary assets are embedded as base64 `data:` URIs rather than linked as separate files. This keeps the "no external dependencies" promise intact but makes the file large. Inventory:

| Asset | Format | Approx. size (encoded) | Where used |
|---|---|---|---|
| Profile photo | JPEG | ~49 KB | Hero section (duotone-treated via CSS `filter`) |
| Resume PDF | PDF | ~811 KB | "Download Resume" button in hero |
| Data Axle logo | PNG | ~17 KB | Career Journey companies strip |
| Genpact logo | SVG | ~8 KB | Career Journey companies strip |
| Genesys logo | SVG | ~12 KB | Genesys platform card |
| Salesforce logo | SVG | <1 KB | Salesforce platform card |
| Oracle logo | SVG | <1 KB | Oracle platform card |
| Scrum Alliance logo | SVG | ~10 KB | Certifications section |
| Anthropic logo | SVG | <1 KB | Certifications section |

**Logo sources:** Genpact, Data Axle, and Genesys logos were sourced from Wikimedia Commons (official company logos hosted there). Salesforce, Oracle, Scrum Alliance, and Anthropic logos came from the open-source **Simple Icons** project. All are used in a small "logo chip" format (white rounded background) purely to identify past employers, platforms worked with, and certifying bodies — standard nominative use, the same way LinkedIn itself displays them. Muvi does not have a reliably sourceable official logo file, so it's represented as a clean text wordmark instead of risking an incorrect/outdated image.

**All logo chips render on a white background** regardless of site theme — this guarantees legibility no matter what colors are baked into the source logo (several, like Genesys, use near-black text that would vanish on the dark theme without this).

---

## 7. Content Sources & Fact-Checking

Every claim on the site was cross-referenced against real source documents rather than invented:

1. **Resume** (`Subodh_Deshmukh_Resume copy.pdf` / `.docx`) — primary source for role titles, dates, and platform-level metrics.
2. **LinkedIn export** (`SUBODH DESHMUKH-Linkedin.pdf`) — source for the "not the loudest in the room" quote, the QueueFinder story, and the Certified AI Generalist / Claude 101 credentials.
3. **2025 Performance Review** (`Subodh Deshmukh - Review Form (Annual Performance Review CY 2025).pdf`) — source for the Prasad Udupi recognition quote, the 4/4 "Sets a New Standard" rating, and the generalized 2025 achievement bullets (150+ requirements delivered, 48-step→8-step process simplification, the 8-squad SMS launch).
4. **LinkedIn recommendations** (screenshots provided directly) — source for the 4-card Recognition grid quotes.

### Handling internal/confidential details
The performance review contained internal Data Axle system codenames (e.g. specific internal platform/squad names) and infrastructure specifics (disaster recovery, PCI compliance details). Per an explicit decision, these were **generalized** on the public site (e.g. "led a two-way SMS launch across 8 cross-functional squads" instead of naming the actual squads or internal system codenames) to avoid publishing internal-only information, while still capturing the scale and impact of the work.

---

## 8. Positioning & Content Decisions

A few notable judgment calls were made during development, worth documenting so future edits stay consistent:

- **Title framing:** The user's title differs across sources — LinkedIn says "Lead Product Owner," the resume says "Lead Product Manager," and the performance review says "Senior Product Owner." Rather than pick one (or worse, silently paper over the conflict), the site **does not lead with a specific title at all**. The hero uses a role-neutral positioning line ("Platform Strategy · Product Leadership · AI-First Delivery") instead of "Job Title · Company." Specific historical titles are still shown accurately inside the Career Journey timeline (sourced from the resume), where a factual record is expected.
- **Numbers were revised on request:** Business impact at Data Axle was updated from $500K+ → **$1M+**; Genpact client savings was updated from $4M → **$3M**. These were direct user corrections, applied consistently across the hero chips, Impact counters, and Career Journey bullet.
- **Career Journey is in descending (most-recent-first) order** — a deliberate change from the original ascending/chronological order, matching standard resume convention.
- **Not a title-driven, single-employer portfolio:** the whole site was restructured at one point specifically so it would be "usable everywhere" — i.e., not so tightly bound to the current job/title that it goes stale the moment the user changes roles.

---

## 9. How to Make Future Edits

Since everything lives in one HTML file, editing is straightforward but requires care around the embedded assets:

- **Text/copy changes:** Find the relevant section by its `<!-- SECTION NAME -->` HTML comment and edit directly. All section content is plain, readable HTML.
- **Colors/theme:** Edit the CSS custom properties in the `:root` block (dark) and `:root[data-theme="light"]` block (light) near the top of the `<style>` section. Everything else references these variables, so a single change cascades everywhere.
- **Adding a new section:** Copy an existing `<section>` block as a template, give it a unique `id`, and remember to renumber the `class="label"` values in every section that follows (e.g. "05 —" becomes "06 —") to keep the numbering sequential.
- **Swapping the photo or resume PDF:** These are base64-encoded inline. To replace them, the image/PDF needs to be re-encoded to base64 and the `data:` URI swapped — this is not a simple drag-and-drop replacement since there's no separate image file to overwrite. (Ask Claude to do this — it's a scripted process, not manual editing.)
- **Do not read the raw file top-to-bottom in an editor that struggles with extremely long lines** — the embedded base64 assets each sit on a single very long line, which can make plain text editors slow or unresponsive. Editing via search/replace on surrounding text (not the base64 itself) avoids this.

---

## 10. Deployment / Hosting

The site is **not yet deployed**. Two paths were discussed:

### Option A — Netlify Drop (fastest, zero setup)
Drag `index.html` onto [app.netlify.com/drop](https://app.netlify.com/drop) for an instant live URL.

### Option B — GitHub Pages (in progress)
- Target repo: `git@github.com:subodhpersonal/subodh-portfolio.git` (already exists on GitHub under the `subodhpersonal` account)
- This machine's default SSH key is tied to a **different** GitHub account (`subbbd`), so a second SSH key was generated specifically for `subodhpersonal` (`~/.ssh/id_ed25519_subodhpersonal`, aliased via `~/.ssh/config` as `github-subodhpersonal`)
- **Status: blocked.** The public key was generated and provided to the user to add under the `subodhpersonal` account's GitHub settings (Settings → SSH and GPG keys → New SSH key), but the connection test (`ssh -T git@github-subodhpersonal`) still returns "Permission denied (publickey)" — meaning the key has not yet been successfully added/saved on the GitHub side. This needs to be resolved before the first push can succeed.
- Once resolved, the remaining steps are: `git init`, commit `index.html`, `git remote add origin git@github-subodhpersonal:subodhpersonal/subodh-portfolio.git`, push to `main`, then enable Pages in the repo's Settings → Pages (source: `main` branch, root folder).

---

## 11. Open Items / TODO

- [ ] Resolve the SSH key setup for the `subodhpersonal` GitHub account and complete the first push
- [ ] Enable GitHub Pages once pushed, confirm the live URL
- [ ] Optional: source an authentic Muvi logo file to replace the current text wordmark
- [ ] Optional: add a scroll-drawn animation to the Career Journey timeline's connecting line
- [ ] Optional: add a custom cursor dot for extra desktop polish (discussed, not implemented)
- [ ] Reconcile the title discrepancy across LinkedIn / resume / performance review at the source (outside this site's scope, but worth doing for consistency)

---

## 12. File Manifest

| File | Purpose |
|---|---|
| `index.html` | The entire website — single file, self-contained |
| `PORTFOLIO-DOCUMENTATION.md` | This document |

No other files are required for the site to run. Any `.claude/` config files in this directory are local tooling artifacts (dev-server launch config used during development for local preview) and are not part of the deployed site.
