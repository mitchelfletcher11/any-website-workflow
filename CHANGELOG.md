# Changelog

## v1.0.0 — 2026-07-06
Initial public release. Design + build a distinctive static marketing website for any business
(from scratch or transformed from an existing site), then deploy to Cloudflare Pages. Includes the
PROPOSE-before-BUILD gate, two-sided-audience intake, exemplar discovery, and:
- self-host-fonts-by-default policy (GDPR; CDN only for non-EU audiences)
- §5 DDG (ex-TMG) legal reference
- disambiguation vs rest-website-workflow and rest-minisite-workflow
- documented extract→build path seam; frontend-design owns design authority

## v1.1.0
- Add a **Preflight (first-run setup)** section that detects and installs the five composed skills
  (`frontend-design`, `cloudflare-pages-deploy`, `data-search-to-saturation`, `rest-website-extract`,
  `rest-website-intake`), each now published as its own public repo.
- SETUP.md rewritten to point at the live dependency repos + a one-shot manual install loop.
- Fixes the gap where installing this skill alone left the composed phases unusable.
