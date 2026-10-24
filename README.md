# hello-world-site

A small static "Hello World" site. This repository is kept private by request. The site lives in the `site/` folder and contains:

- `index.html` — the page
- `styles.css` — simple styling

Preview locally

- Open `site/index.html` in the browser (double-click or use a `file://` path).
- Or run a simple local server from the project root (requires Python):

  - Python 3: `python -m http.server --directory site 8000`
  - Then open http://localhost:8000

How to publish later

You can enable GitHub Pages or use an external host (Vercel / Netlify) when you're ready. Below are safe options and step-by-step guidance.

Option A — Publish from `docs/` on `main` (easy, no extra branch)

1. Move the `site/` contents into a `docs/` folder at the repository root:

   - `mkdir docs`
   - `cp -r site/* docs/`
   - `git add docs && git commit -m "Add docs for GitHub Pages"`
   - `git push`

2. Go to the repository Settings → Pages and select "Deploy from a branch" → `main` / `docs` folder, then Save.

Option B — Publish from a `gh-pages` branch (keeps `main` as source)

1. Create a deployment workflow that builds and publishes `site/` to the `gh-pages` branch. You can use an action such as `peaceiris/actions-gh-pages` or `JamesIves/github-pages-deploy-action`.

2. Example (create `.github/workflows/deploy-pages.yml`):

```yaml
name: Deploy site to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          branch: gh-pages # The branch the action should deploy to.
          folder: site     # The folder the action should deploy.
```

3. After this workflow runs on `main` it will push compiled site files to `gh-pages`. In Settings → Pages set "Branch: gh-pages" as the source.

Option C — Use Vercel or Netlify (deploy publicly, keep repo private)

- Vercel and Netlify can build from private GitHub repos if you link your GitHub account and give the platform access to the repository.
- On Vercel: "New Project" → Import from GitHub → select the private repo → set the build settings (no build step needed for plain static site; set output to root or `site/`). After deployment, Vercel gives a public URL.

Making the repo public (if you change your mind)

- Via GitHub website: Settings → Danger Zone → Change repository visibility → Make public.
- Via GitHub CLI: `gh repo edit OWNER/REPO --visibility public` (you must be authenticated with `gh`).

Notes & recommendations

- Because you asked to keep the repo private, I have not enabled Pages or added any deployment workflows.
- If you want, I can prepare one of the deployment workflows (example for `gh-pages` or Vercel configuration) and add it to the repo so you can enable/publish later without losing privacy.

What I can do next

- Add a `LICENSE` file.
- Add a sample GitHub Actions workflow for Pages (kept disabled or on a branch) so you can enable it later.
- Deploy the site to Vercel or Netlify and give you the public URL while keeping the repo private.
- Make the repo public and set up automatic Pages deployment (only if you say so).

Tell me which of these you want me to take next.
