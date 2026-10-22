# Keng Seng Choo Artist

A static artist portfolio and bilingual archive, built with Astro. Articles are Markdown files and can be added by prompting the assistant in this project. See [the content workflow](docs/content-workflow.md).

## Local preview

Use Node.js 24 or newer supported by Astro and install dependencies with `npm ci`. Run `npm run dev`, then open the local URL it prints. Run `npm run build` and `npm run validate` before publication.

The website contains the 31 published WordPress articles, seven unrestricted pages and 14 paintings: the original 12 from the 2016 collection plus two oil paintings already published in earlier WordPress articles. The recovered private archive is kept outside this repository until a selection is made. The two near-duplicate articles retain their original records and routes.

## Hosting

The public artist source repository is [Keng Seng Choo Artist](https://github.com/kengcc/Keng-Seng-Choo-Artist). The existing [live website](https://kengsengchoo.com/) is deployed from `kengcc/kengsengchoo.com`; keep both repositories in sync when publishing. The workflow builds and validates both copies, and deploys only from the hosting repository at the custom domain.

The GitHub Actions workflow builds and publishes the `main` branch through GitHub Pages. Set the repository's Pages source to GitHub Actions. The production address is `https://kengsengchoo.com/`.

The workflow defaults to `SITE_URL=https://kengsengchoo.com` and `SITE_BASE=/`, matching the custom domain configured in GitHub Pages and `public/CNAME`. Optional repository variables override them; remove any old project-path overrides when publishing at the domain root. Local preview builds still default to `/` without a production origin.

To test the production deployment locally:

```sh
SITE_URL=https://kengsengchoo.com SITE_BASE=/ npm run build
SITE_BASE=/ npm run validate
SITE_URL=https://kengsengchoo.com npm run validate:seo
```

To test an alternative project-path deployment locally:

```sh
SITE_URL=https://kengcc.github.io SITE_BASE=/kengsengchoo.com/ npm run build
SITE_BASE=/kengsengchoo.com/ npm run validate
```

`dist/` is portable static output and can also be hosted on Cloudflare Pages. The build supplies exact legacy-path HTML redirects; `_redirects` adds server redirects on hosts that support it. GitHub Pages uses the HTML redirect pages. Old `?p=ID` links need the homepage's query-redirect behavior.

The build emits a sitemap, RSS feed and production robots rules when `SITE_URL` is configured. The unmatched VIP page and private collection are excluded. A local preview build without that variable disables indexing.

## Content and privacy

The unmatched VIP gallery and the 211 recovered personal collection candidates are excluded. Only artwork referenced in WordPress content belongs in this site. The public contact details are limited to email and Facebook.

Original WordPress backups, SQL exports, migration reports and excluded family photographs belong outside this source repository. Original artwork and press material retain their source attribution. Do not rerun the original import over subsequent editorial changes.

Deployment follows [Astro's official GitHub Pages guide](https://docs.astro.build/en/guides/deploy/github/).
