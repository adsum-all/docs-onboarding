# Cloudflare Pages deployment - adsum-design

Procedure for the ADSUM design deliverable (static site, edge Basic Auth).

## URLs

- Production site: https://adsum-design.pages.dev
- GitLab repository: https://gitlab.com/sr-media-ai/adsum/docs/adsum-design
- Cloudflare dashboard: Pages > adsum-design

## Build settings (Cloudflare Pages)

- Build command: none (static site).
- Output directory: repository root.
- Production branch: main.

## Access protection (Basic Auth at the edge)

Protection is enforced by `functions/_middleware.js`, published with the site.
It reads two variables defined on the Cloudflare Pages project
(Settings > Environment variables), on both production and preview:

- `SITE_USER` = `adsum`
- `SITE_PASS` = a strong password.

Without these variables the site stays open (no accidental lockout). With them,
Basic Auth is active everywhere. The password is stored only in the control tower
secret `.secret/adsum-design-basic-auth.json`, never committed, never in clear in
the repository.

## CI deploy (GitLab to Cloudflare)

The repository `.gitlab-ci.yml` deploys on every push to `main`:

```
npx --yes wrangler@3 pages deploy . --project-name=adsum-design --branch=main --commit-dirty=true
```

Required GitLab CI/CD variables (repo Settings > CI/CD > Variables, masked + protected),
read by wrangler from the environment, never in clear:

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

Workflow: `feature/*` -> merge request -> `main` (reviewed). Merging to `main`
triggers the deploy pipeline.

## Rollback

- Fast path: Cloudflare dashboard > Pages > adsum-design > Deployments, pick a
  previous successful deployment and choose "Rollback to this deployment".
- Git path: revert the offending commit on `main` through a new merge request;
  the merge triggers a fresh deploy of the previous good state.

## Rotate SITE_PASS

1. Update `SITE_PASS` on the Cloudflare Pages project (production and preview).
2. Redeploy (push to `main` or trigger a deployment).
3. Update `.secret/adsum-design-basic-auth.json`. Never commit the value.
