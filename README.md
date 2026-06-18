# mouline-co-uk

Production site served at **https://mouline.co.uk** via GitHub Pages.

This repo holds **only the deployment mechanism** — it has no source content of
its own. The actual landing pages are authored in
[`mouline-io/nova-marketing`](https://github.com/mouline-io/nova-marketing).

## How to deploy

**Actions → "Deploy landing to production" → Run workflow.**

The workflow clones `nova-marketing`, copies the chosen landing file to
`index.html`, and publishes it to GitHub Pages. By default it ships
`docs/landing-mouline-v2.html`; override the `source_file` input to publish a
different version.

## How it works (no-key pull model)

The deploy job runs *here* and pulls *from* `nova-marketing`:

1. `git clone` the public `nova-marketing` repo (no auth needed — it's public).
2. Copy the selected landing → `index.html`, add `CNAME` + `.nojekyll`.
3. Deploy to this repo's own GitHub Pages using the built-in `GITHUB_TOKEN`.

No deploy keys or secrets are involved.

> [!IMPORTANT]
> This depends on `nova-marketing` being **public**. If it is ever made
> private, the unauthenticated clone in `.github/workflows/deploy.yml` will fail
> and the deploy mechanism must be reworked (e.g. a deploy key).
