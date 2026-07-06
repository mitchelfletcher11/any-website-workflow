---
name: any-website-workflow
description: >-
  Design and BUILD a distinctive, up-to-date best-practice marketing website for any business —
  either from scratch or transformed from the business's existing site — then deploy it live to
  Cloudflare Pages (free, HTTPS). Use this whenever the user wants a new website, a site
  rebuilt/redesigned/modernised, a landing or marketing page for a company/agency/product/portfolio,
  or says things like "build me a website for my business", "make a site for X", "I need a modern
  website", "redesign our site", "turn our old website into something better". This is for
  GENERAL businesses as a self-contained static single-page site. (For the restaurant
  WordPress+Astra managed pipeline use rest-website-workflow instead; for a restaurant's
  Instagram link-in-bio companion page — menu-first, reservation, chat concierge — use
  rest-minisite-workflow, which complements a full website rather than replacing it. This skill
  composes rest-website-extract, data-search-to-saturation and frontend-design rather than
  duplicating them.)
---

You design and ship a **distinctive, best-practice marketing website** for a business, end to end:
intake → (optional) extract an existing site → discover exemplars → **propose a design + system and
get sign-off** → build a self-contained `index.html` → verify on desktop & mobile → deploy to
Cloudflare Pages. The output should be good enough that the site itself is a portfolio piece.

**Two modes, same workflow:**
- **From scratch** — a brand-new business with only a brief (e.g. the KreatorKitchen build).
- **From an existing site** — transform/modernise a live site, reusing its real content + assets.

**The golden rule: PROPOSE before you BUILD.** Phase 4 is a hard sign-off gate. Never jump
straight to code — a wrong concept wastes the whole build. And never ship generic "AI-slop"
design; the whole point is a site that feels genuinely, specifically designed.

**Skills this composes (don't duplicate them — invoke/apply them):**
- **`rest-website-extract`** — Phase 2, to harvest a real existing site's content/assets/brand.
- **`data-pipeline-workflow`** → its discovery phase **`data-search-to-saturation`** — Phase 3, to
  find ranked exemplar sites + current best-practice for the business type (discovery only — do NOT
  scaffold the full collect/classify pipeline).
- **`frontend-design`** — Phase 5, the build-craft principles (distinctive type/colour/motion, no AI-slop).
- **`cloudflare-pages-deploy`** — Phase 7, to publish the static build to a public HTTPS URL.

(This is the general-business counterpart to the restaurant-specific `rest-website-workflow`.)

---

## Phase 1 — Intake (ask these; don't assume)

Ask conversationally, grouped — not as a wall. Capture every answer; these are the inputs the
whole build depends on. (These reproduce the inputs that produced KreatorKitchen.)

1. **Business name** (and any tagline).
2. **From scratch, or from an existing website?** If existing → get the **URL** (you'll extract it in Phase 2).
3. **What does the business actually do — and why does it matter?** The real-world purpose/stakes, not a slogan.
4. **Who are ALL the audiences?** ⚠️ *The single most important question.* Many businesses are
   **two-sided / multi-audience** and you must design for every side. KreatorKitchen looked like a
   restaurant agency but actually serves **restaurants AND creators** — a kitchen-only concept would
   have alienated half the market. **Never assume one audience.** Explicitly ask "is there more than
   one type of person this needs to speak to?" and, if so, what each side wants and fears. The brand
   must intrigue every side from the name down.
5. **The services/offerings to present** (usually 3–5). For each: is it **two-sided** (delivers value
   to more than one audience)? Note which.
   - **Creator / influencer briefs — ask this EARLY:** is the site the creator's **portfolio**
     (the site is *about the creator* — their work, their brand) or a **user-utility with the creator
     as curator** (the site helps the *visitor* do something — e.g. find where to eat — with the creator
     credited as a quiet "powered by" voice)? These produce **opposite** designs, and guessing wrong
     wastes whole builds (one creator brief ran to eleven iterations before this fork was pinned down).
6. **Desired tone/feel.** Push for a concrete adjective set (e.g. "compact, clean, sharp, contemporary
   — not minimalist-empty, not over-the-top"). Vague answers → offer 2–3 distinct directions to react to.
7. **Must the site itself prove design quality?** (Agencies/studios/designers: yes — it's their
   portfolio, so the bar is higher and the site must *perform* the craft, not just claim it.)
8. **Brand constraints or free rein?** Existing logo / colours / fonts to honour, or a clean slate?
9. **Language & locale + legal needs.** e.g. German/DACH → **Impressum + Datenschutz are mandatory**
   (§5 DDG — the Digitale-Dienste-Gesetz that replaced the TMG in 2024 — / DSGVO); other locales have their own. Always ask the primary language.
10. **Single-page or multi-page?** (Default to a single long-scroll for a focused business; add a thin
    secondary layer only for case-study detail + legal pages.)
11. **Primary conversion goal + CTA(s).** What's the one action you want a visitor to take? (If
    two-sided, you likely need a dual CTA — one per audience.)
12. **Hosting/deploy** — confirm Cloudflare Pages is fine (default), and the desired project slug.

If the user already gave some of this in conversation, fill it in and only ask the gaps. Confirm a
short summary before moving on.

---

## Phase 2 — Existing site? Extract the real material

Only if Mode = from existing site. **Reuse `rest-website-extract`** (it's content-agnostic) to
harvest: real copy (verbatim — never paraphrase headlines), photos/logo/favicon, brand colours,
fonts (incl. any distinctive display/logo font + its text effects), reviews/testimonials with the
correct source + aggregate rating, social embeds, and the full page/section inventory.
**Path seam:** `rest-website-extract` writes to `clients/CLIENT_SLUG/` (its own convention) —
set CLIENT_SLUG to this project's slug, treat `clients/<slug>/` as the extraction workspace, then
copy the chosen assets/content into `<project>/website/` for the build; don't build inside the
extraction folder. Build the same "extract EVERY element" content inventory so nothing the
business already has goes missing. The goal: same content/assets, upgraded design.

**Go past the homepage — crawl the per-item detail pages** (events, products, team, menu items).
The homepage usually under-explains; the detail pages (and their slugs) carry the *concrete* "what
it actually is" — formats, prices, dates — and the **per-entity social links** (e.g. an Instagram
handle per venue) so social can be woven through every card, not linked once. Surfacing this concrete
detail is often the single biggest upgrade over the original.

**Bot-protected sites (Cloudflare "Just a moment…" / 403):** a plain headless crawl can't solve a
JavaScript challenge. Fall back to a **stealth headful** browser (xvfb + `navigator.webdriver`
patched + a real user-agent) and crawl **one page per fresh browser context** — the challenge
typically clears on the *first* navigation of a session, then re-triggers, so a fresh context per
page beats it. Pull images from the asset CDN (Webflow `*.website-files.com`, Jetpack `i0.wp.com`),
which usually isn't behind the same bot rules.

For a from-scratch build, skip this — the brief + Phase 3 are your inputs.

---

## Phase 3 — Discovery (exemplars + current best practice)

Find what excellent looks like for **this specific business type**, so the design is grounded in
current craft, not your defaults. Run the **discovery phase only** of `data-pipeline-workflow`
(i.e. `data-search-to-saturation`) — do NOT scaffold the full DB/scrape/classify pipeline for a
one-off design research task; that's overkill. The fast path: spawn ~3 parallel research subagents
on distinct angles (e.g. direct-category sites · adjacent/aspirational sites · design best-practice &
2026 trend sources, mining Awwwards / Godly / Land-book / SiteInspire). Each returns specific URLs
with concrete, stealable design traits (structure, type, colour, motion, density). Then **synthesise
a ranked exemplar list** and pull the recurring "premium formula" for the category. Flag any
direct competitors (what to beat / what-not-to-do) and any same-locale references.

---

## Phase 4 — Propose the design + system, get sign-off (HARD GATE)

Present the proposal in chat **before any code**, using THIS structure and order — it mirrors the
format that worked for KreatorKitchen, and the fixed order lets the user react fast:

**1. Exemplar list** — the ranked sites from Phase 3, grouped: **Study first** (closest fits) ·
category groups (e.g. direct / aspirational / meta-credibility) · local & competitor benchmarks.
One line each: name + URL + the single trait worth stealing.

**2. The design suggestion**
- **Concept** — a *named*, ownable creative direction + 1–2 sentences on **why** it fits the
  audiences and brief (e.g. *"Kreator × Kitchen — zwei Welten, ein Tisch"*: a two-sided duality,
  not a one-audience metaphor).
- **Section structure** — the page as a numbered scroll (hero → … → footer + legal).

**3. The design system, WITH reasoning** — a short block per item, every choice justified:
- **Typography** (display + body faces; why they fit / why non-default)
- **Colour** (base + accent(s); if two-sided, the dual-accent encoding; the "why")
- **Layout / density** (8px, bento, compact-not-empty; the "why")
- **Motion** (what + why; performance note)
- **Imagery / media** (what supplies the warmth/energy; placeholder plan if assets are missing)

**4. A one-line recommendation** — your default pick across the open choices.

**5. Sign-off gate** — then use **AskUserQuestion** for the genuinely pivotal forks, e.g.:
*Direction* (build as proposed / tweak / rethink) · *Theme* (light / dark-stage / mixed) ·
*Concept lean* (light seasoning / full / minimal) · *Type direction* · and **if two-sided, how the
audiences are structured** (unified paired scroll / dual-path / primary + on-ramp). Offer concrete
previews where they help the user choose.

**Do not build until the user confirms.** If the user reframes the brief (as on KreatorKitchen's
two-sided pivot), **re-propose** — a cheap conversation beats an expensive rebuild.

---

## Phase 5 — Build (apply `frontend-design`)

Invoke/apply the **frontend-design** skill's principles and build a **self-contained `index.html`**
(embedded CSS + minimal JS; one file is portable and showcases a fast site). Build in a clean folder
(e.g. `<project>/website/`). `frontend-design` owns the craft principles; the defaults below are
this skill's field-tested extensions of it, not a replacement — on conflict, taste questions defer
to `frontend-design`.

**Mechanic:** write ONE `index.html` — HTML + an embedded `<style>` block + vanilla `<script>`.
**Fonts: SELF-HOST by default** — download the woff2 files into `<project>/website/fonts/` and
declare them via `@font-face`; do **not** hot-link Google Fonts/CDN `<link>` tags for any site
with EU/German visitors (a remote Google Fonts request transmits the visitor's IP to Google —
the classic German Abmahnung risk, LG München 2022; self-hosting also loads faster and lets the
Datenschutzerklärung truthfully say "no data to Google"). Pull the files once at build time from
Fontshare/Google (a `css2?family=…&text=` request even gives pre-subsetted woff2s for CJK or
display-only glyph sets). A CDN `<link>` is acceptable ONLY when the client explicitly serves a
non-EU audience — and say so in the proposal. **No framework, no build step, no bundler** — a
single static file. This keeps it instantly deployable to Cloudflare Pages and is itself the
performance proof for the business. Use CSS custom properties for the whole design system
(tokens for colours, fonts, spacing, radius). Then serve it locally
(`cd <project>/website && python3 -m http.server <port>`) for Phase 6 verification.

Defaults that produced good results — adapt, don't blindly copy:

- **Typography:** a distinctive DISPLAY face + a clean body sans. **Never** the AI-default fonts
  (Inter, Roboto, raw Space Grotesk, the Outfit+DM-Sans "agency default") as the brand voice — the
  font is the first proof of taste. Good free sources: Fontshare (Clash Display, General Sans,
  Satoshi) and editorial serifs (Fraunces); paid upgrades (Canela, PP Editorial New). Pair for
  tension (serif × sans or distinctive-display × neutral-body). 2 families, ~3–4 weights.
- **Colour:** commit to a dominant neutral base + **one owned accent** — or, when the business is
  **two-sided, a meaningful DUAL accent that encodes the sides** (KreatorKitchen: ember = restaurants,
  lime = creators, used to colour-code each track). Avoid generic palettes (esp. purple-on-white).
  Use a warm near-black instead of pure #000 where warmth helps. Consider one dark "stage" band
  (e.g. for a video/work section) rather than a globally dark site.
- **Layout:** 8px spacing system; a **bento grid** backbone; **compact, editorial density — not
  minimalist-empty** (rank secondary content by size/weight, don't float one word per screen); one
  surgical anti-grid/asymmetric moment.
- **Motion:** tasteful CSS scroll-reveal (fade/translate-up), one kinetic hero moment, a sticky-scroll
  process section, hover micro-interactions. Animate **transform/opacity only**; respect
  `prefers-reduced-motion`. Motion should *demonstrate* craft, not decorate.
- **Media / imagery — real photography is the single biggest lever.** Imagery quality dominates whether
  a build reads as "designed" or "unfinished": emoji-on-gradient (and even tasteful duotone) placeholders
  read as a wireframe, and **no layout can rescue a page whose images are placeholders** — this was the
  root cause behind five rejected iterations on one build. So **pin down the imagery source EARLY** (in
  Phase 1/4, not at build time) and default to REAL photos, downloaded and bundled locally so the build is
  self-contained. Sourcing recipe when the business has no photos of its own:
  1. **WebSearch** with `allowed_domains=pexels.com` for the subject (e.g. "ramen bowl photo") to get
     Pexels photo-page URLs → the numeric **photo ID**.
  2. Construct the CDN URL: `https://images.pexels.com/photos/{id}/pexels-photo-{id}.jpeg?auto=compress&w=1400`
     (for Unsplash, `https://images.unsplash.com/photo-{id}?...`).
  3. **curl-test each URL** for a 200 + image content-type, then **download it into `website/img/`** — do
     NOT hotlink at runtime. Keyword-proxy services (`loremflickr`, `source.unsplash.com` (503/deprecated),
     `foodish`) are unreliable; only direct CDN-by-ID works.
  Use muted autoplay loops for video (lazy-loaded, captioned, with a real **poster** frame so the tile is
  never blank even if the codec can't decode in headless verify). Only fall back to intentional
  gradient/duotone placeholders when real imagery is genuinely unobtainable — and then tell the user they
  are placeholders to swap.
- **Section structure (single-page default):** sticky nav + CTA → hero (one value prop + visual,
  dual CTA if two-sided) → trust strip → services (numbered, **benefit-named** not category nouns,
  one highlighted; if two-sided show **both** sides per service) → proof/work (bento; dark band
  optional) → process (sticky, 3–4 steps) → offer/pricing (transparent) → CTA + **short contact
  form ≤5 fields** → footer (+ legal links). One primary CTA repeated (or dual, per audience).
- **Lists of many items** (events, products, menu, pairings): render the cards from a **JS data array
  + client-side filter** (by day/type/category) — not hand-coded duplicate markup. It keeps every card
  concrete and consistent, gives free filtering, and is trivial to extend. Each card should lead with
  the **concrete what** (format, price, date) — not vague description.
- **Brand fidelity (existing-site mode):** when honoring an existing brand, **self-host the original's
  actual font files** (grab the `woff2/otf/ttf` from its CDN) for exact typographic fidelity, and keep
  the **exact palette** — a recurring user preference is "keep the same colours/branding," so default
  to faithful and elevate the execution, not the identity, unless told otherwise.
- **Completeness (existing-site mode):** place EVERY element from the Phase-2 inventory — nothing the
  business already has should silently disappear.

---

## Phase 6 — Verify (screenshot, and check the bugs that actually bite)

Serve the folder locally and drive it with Playwright (chromium) at **1440px (desktop)** and
**390px (mobile)**. Look at the result — and run these concrete checks, because each is a real bug
that shipped on the first KreatorKitchen pass:

- **Scroll section-by-section** (scrollIntoView + wait), capturing per-section viewport shots. Do
  NOT trust a single `fullPage` screenshot — it doesn't reliably trigger scroll-reveal, so it
  falsely shows revealed content as blank.
- **"Stuck invisible" check:** a second `animation` on an element silently overrides an entrance
  `animation`, leaving it at `opacity:0`. Assert key visual elements have **computed opacity 1**
  after load/scroll. (Fix: don't put the entrance class on elements that also have their own
  keyframe animation — give them their own visible state.)
- **Reveal must never GATE visibility:** content must be readable even if the reveal JS never fires
  or is skipped. Use the IntersectionObserver for the animation, a scroll-listener failsafe, AND a
  **hard catch-all** — `setTimeout(()=>document.querySelectorAll('[data-reveal]').forEach(e=>e.classList.add('in')), ~2000)`
  — so nothing can ever stay `opacity:0`. (IO + scroll-failsafe alone still left whole below-fold
  sections invisible on Third World Medical and Tasteover until the hard timeout was added.) Assert
  **0** `[data-reveal]` elements have computed opacity < 0.05 after load + a full scroll.
- **Mobile overflow:** assert `document.documentElement.scrollWidth === innerWidth` (no horizontal
  scroll). If not, find offenders (`getBoundingClientRect().right > innerWidth`) — the usual cause
  is a **non-wrapping flex row** (add `flex-wrap:wrap`).
- **Zero-width container check:** a flex/grid item whose children are **all absolutely-positioned**
  has no in-flow content, so with `margin:auto` (which makes a grid/flex item size to its content,
  not stretch) it collapses to **width 0** — silently shrinking its absolute children to ~0px. This
  hit the KreatorKitchen mobile hero (the paired "reel" visuals vanished). Give such containers an
  **explicit width** (e.g. `width:min(360px,100%)`) instead of relying on stretch, and assert key
  layout containers have non-zero width at 390px.
- **Fonts loaded:** confirm the computed `font-family` on a heading/body matches the chosen faces
  (CDN font failures silently fall back to system fonts).
- **Lint the `<script>` block BEFORE the browser check:** extract the inline script and run
  `node --check` on it. A single stray straight quote inside a non-English string (e.g. a `"` inside a
  German `„…"`) silently terminates both the JS string literal AND the enclosing HTML attribute — a
  browser check may just show a blank/half-broken page with no obvious cause; `node --check` catches it
  in a second.
- **Homoglyph / unicode scan of non-English copy:** stray Cyrillic or Greek look-alikes (a Cyrillic
  `т`/`о`/`с` pasted into a German or French word) render fine but corrupt search, copy, and fonts. Scan
  the text for characters outside the expected Latin + locale range and flag any homoglyphs before ship.

---

## Phase 7 — Deploy to Cloudflare Pages

Deploy the built `<project>/website/` folder using the **`cloudflare-pages-deploy`** skill — it is
the single source of truth for the deploy mechanics (credential storage, the wrangler/Node caveat,
project-create, deploy, verify, ECONNRESET-retry, and the public-URL warnings). Give it the static
folder + a project slug; it returns the live `https://<slug>.pages.dev` and handles the
public/placeholder warnings. Re-deploy after edits by re-running its deploy command.

---

## Cross-cutting principles (why this works)

- **Propose before build.** The concept is the highest-leverage decision; a wrong one wastes the
  whole build. Always gate on sign-off (Phase 4).
- **Design for every audience.** Two-sided businesses are common and easy to under-serve. The brand,
  name, and visuals must make *each* side feel seen — ask, then encode it (e.g. dual accents/CTAs).
- **Distinctive over generic.** No AI-slop: no default fonts, no purple-on-white, no cookie-cutter
  hero→3-cards→footer with no point of view. Commit to one ownable idea and execute it precisely.
- **Compose, don't duplicate.** Lean on `rest-website-extract` (existing-site content),
  `data-search-to-saturation` (exemplar discovery), and `frontend-design` (the build craft).
- **Verify like a user, then ship.** Screenshot desktop + mobile, run the named bug checks, deploy
  to a real HTTPS link.

---

## Final Step — Write observation

Append a timestamped entry to `~/.claude/skills/any-website-workflow/observations.md`:

```markdown
## [ISO 8601 timestamp]
[One sentence: business + mode (scratch/existing), the concept chosen, what worked, any new
build/verify/deploy gotcha worth encoding next time.]
```

If `observations.md` does not exist, create it with this frontmatter first:

```markdown
---
last-reviewed: 1970-01-01T00:00:00Z
---
```
