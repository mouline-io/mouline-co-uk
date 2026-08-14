# mouline-co-uk

Production site served at **https://mouline.co.uk** via GitHub Pages.

This repo holds the deployment mechanism plus the published site under `public/`.
It has no source of its own — the pages are authored in
[`mouline-io/nova-marketing`](https://github.com/mouline-io/nova-marketing) and
mirrored here automatically.

## How it works (push model)

The source repo pushes to this one; nothing here reads from the source repo.

1. A publishing workflow in the source repo mirrors its publish folder into
   `public/` here and pushes.
2. That push triggers `.github/workflows/deploy.yml`, which uploads `public/` and
   deploys it to this repo's GitHub Pages using the built-in `GITHUB_TOKEN`.

To redeploy the current content without a source change: **Actions → "Deploy landing
to production" → Run workflow.**

## Don't hand-edit `public/`

It is deleted and rebuilt from scratch on every publish, so local edits are silently
overwritten. Change the page in `nova-marketing` instead.

> [!IMPORTANT]
> The source repo is private and stays private. Deploys do **not** require it to be
> public — the mirroring push is authenticated. If the site stops updating, fix the
> publishing workflow in `nova-marketing`; never make that repo public to restore
> deploys.
