# Physicist website starter

A Quarto academic website intended for deployment to Cloudflare Pages.

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

## 4. Create the Cloudflare Pages project

In Cloudflare:

1. Open **Workers & Pages**.
2. Create a **Pages** project using **Direct Upload**.
3. Name it, for example, `academic-site`.
4. Make an initial upload of the locally generated `_site` directory, or run Wrangler locally.

Render and deploy manually if desired:

```bash
quarto render
npx wrangler pages deploy _site --project-name=academic-site
```

## 5. Configure automatic deployment

In the GitHub repository, open **Settings → Secrets and variables → Actions**.

Create repository secrets:

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

The workflow deploys to the Cloudflare Pages project named `website`. If your
Pages project has a different name, update `--project-name=website` in
`.github/workflows/deploy.yml`.

For the API token, create a Cloudflare token with **Account → Cloudflare Pages →
Edit** permission. After the secrets exist, every push to `main` triggers
`.github/workflows/deploy.yml`.

## 6. Attach the `.dev` domain

In Cloudflare, open the Pages project, select **Custom domains**, choose **Set up a domain**, and enter either:

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
