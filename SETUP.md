# Setup

`any-website-workflow` is a **composing** skill — it invokes these skills at specific phases rather
than duplicating them. Install the ones you want active (each is optional; the workflow degrades
gracefully, but you get the full experience with all four):

| Composed skill | Used at | Purpose |
|---|---|---|
| `rest-website-extract` | Phase 2 | harvest a real existing site's content/assets/brand (content-agnostic) |
| `data-search-to-saturation` | Phase 3 | discover ranked exemplar sites + current best practice |
| `frontend-design` | Phase 5 | the build-craft principles (owns design taste; this skill's defaults defer to it) |
| `cloudflare-pages-deploy` | Phase 7 | publish the static build to a public HTTPS URL (credentials, wrangler/Node caveat) |

## Tooling
- **Node + Playwright** for Phase 2 extraction and Phase 6 verification (a project with `playwright` installed).
- **Cloudflare account + API token** for deploy — handled by `cloudflare-pages-deploy` (see its SETUP).

## Notes
- **Fonts self-host by default** (GDPR/Abmahnung); a CDN `<link>` is used only for an explicitly non-EU audience.
- For a **restaurant**, use `rest-website-workflow` (managed WordPress) or `rest-minisite-workflow`
  (Instagram bio-link mini-site) instead — this skill is for general-business static sites.
