# any-website-workflow — setup

This skill **composes five other skills**. It now installs them for you: on first run its
**Preflight** section detects each, and on your yes clones the missing ones into `~/.claude/skills/`.
You normally don't need to touch anything here — just install this skill and answer the prompt.

## The composed skills (all public)

| Skill | Repo | Role |
|---|---|---|
| `frontend-design` | https://github.com/mitchelfletcher11/frontend-design | Phase 5 — build craft (quality core) |
| `cloudflare-pages-deploy` | https://github.com/mitchelfletcher11/cloudflare-pages-deploy | Phase 7 — deploy to a public HTTPS URL |
| `data-search-to-saturation` | https://github.com/mitchelfletcher11/data-search-to-saturation | Phase 3 — exemplar discovery |
| `rest-website-extract` | https://github.com/mitchelfletcher11/rest-website-extract | Phase 2 — extract a live site (from-existing mode) |
| `rest-website-intake` | https://github.com/mitchelfletcher11/rest-website-intake | Phase 1 — intake when there's no site (pairs with extract) |

## Manual install (if you skip the Preflight prompt)

```bash
for s in frontend-design cloudflare-pages-deploy data-search-to-saturation rest-website-extract rest-website-intake; do
  git clone --depth 1 https://github.com/mitchelfletcher11/$s.git ~/.claude/skills/$s
done
```

`frontend-design` + `cloudflare-pages-deploy` are needed for every build; `rest-website-extract`/
`-intake` only for transforming an existing site.

## Credentials

Only **`cloudflare-pages-deploy`** needs credentials (a Cloudflare API token + account ID) — see that
skill's own `SETUP.md`. The other four need none.
