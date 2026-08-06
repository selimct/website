[![Deploy website](https://github.com/selimct/website/actions/workflows/deploy.yml/badge.svg)](https://github.com/selimct/website/actions/workflows/deploy.yml)


# Physicist website starter

A Quarto academic website deployed with Cloudflare Workers static assets.

## 1. Install Quarto and preview locally

Install Quarto from https://quarto.org/docs/get-started/ and then run:

```bash
quarto preview
```

The local preview normally opens automatically. Edit `.qmd` files and the browser will refresh.

## 2. Personalise the template

Replace all placeholders in:

- `_quarto.yml`
- `index.qmd`
- `about.qmd`
- `publications.bib`
- project and note examples

Replace `profile-placeholder.svg`, `projects/project-placeholder.svg`, and `files/cv.pdf` with real files. If filenames differ, update the links.

The included `nature.csl` is a small placeholder style file. For a particular journal style, obtain the appropriate CSL file and replace the `csl:` value in `_quarto.yml`.

## 3. Create a GitHub repository

```bash
git init
git add .
git commit -m "Initial academic website"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

## 4. Create the Cloudflare Worker

In Cloudflare:

1. Open **Workers & Pages**.
2. Create a **Worker** named `website`.

Render and deploy manually if desired:

```bash
quarto render
npx wrangler deploy
```

## 5. Configure automatic deployment

In the GitHub repository, open **Settings → Secrets and variables → Actions**.

Create repository secrets:

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

The workflow renders the Quarto site and deploys it to the Worker named
`website`, as configured in `wrangler.jsonc`.

For the API token, create a Cloudflare token with **Account → Workers Scripts →
Edit** permission. After the secrets exist, every push to `main` triggers
`.github/workflows/deploy.yml`.

## 6. Attach the `.dev` domain

In Cloudflare, open the Worker, select **Settings → Domains & Routes**, add a
custom domain, and enter either:

- `your-domain.dev`, or
- `www.your-domain.dev`

Update `site-url` in `_quarto.yml` to the final canonical address.

## Content workflow

Add a project by copying `projects/example-project.qmd`.

Add a note by copying `notes/example-derivation.qmd`.

Add publications to `publications.bib`.

Then:

```bash
git add .
git commit -m "Add new content"
git push
```
