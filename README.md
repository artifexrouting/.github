# artifexrouting/.github

Org-level defaults and reusable workflows.

## plugin-release-docs.yml

Reusable workflow (`workflow_call`) that runs when a plugin repo pushes a
release tag: it parses the tagged version's `== Changelog ==` section out of
`readme.txt` and publishes it to the artifex site as a **Release Notes** doc,
then regenerates the plugin's **Hooks Reference** from its docblocks
(`wp-hooks/generator`) — both via the `artifexrouting/user-docs` pipeline
over the WP REST API.

See the header comment in
`.github/workflows/plugin-release-docs.yml` for the caller snippet and
required org secrets:

| Secret | Purpose |
|---|---|
| `DOCS_SITE_URL` | Production site URL (e.g. `https://example.com`) |
| `DOCS_API_USER` | WP service user (`docs-bot`) |
| `DOCS_APP_PASSWORD` | Application password for that user |
| `DOCS_REPO_TOKEN` | Fine-grained PAT with read access to `artifexrouting/user-docs` |

The coupon-creator family (free/pro/add-ons) shares `product: coupon-creator`
and each repo passes its own `component:` display name, so all three publish
into one Release Notes category with per-component posts.
