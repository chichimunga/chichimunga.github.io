---
{"type":null,"dg-publish":true,"dg-hide":true,"created":"2026-04-04 18:23","modified":"2026-04-05 11:45","topic":null,"subtopic":null,"tags":[1,2,3,4,5,6,7],"dg-path":"/setup","permalink":"//setup/","hide":true,"dgPassFrontmatter":true,"dg-note-properties":{"type":null,"created":"2026-04-04 18:23","modified":"2026-04-05 11:45","topic":null,"subtopic":null,"tags":[1,2,3,4,5,6,7]}}
---


## Setting Up Obsidian Digital Garden on GitHub Pages

A complete guide to publishing your Obsidian notes at `username.github.io` using the [obsidian-digital-garden](https://github.com/oleeskild/obsidian-digital-garden) plugin.

---

### Prerequisites

- Obsidian installed with your vault on Google Drive (or local)
- A GitHub account (username: `chichimunga`)
- The note you want as your homepage must have these properties:
  - `dg-publish: true`
  - `dg-home: true`

---

### Step 1 — Create the GitHub Repo from the Template

> **Gotcha:** Do NOT create a blank repo. The plugin requires the repo to be set up from the digital garden template or it will silently fail with "Failed to update settings."

1. Go to **github.com/oleeskild/digitalgarden**
2. Click **"Use this template"** → **"Create a new repository"**
3. Name the repo exactly **`chichimunga.github.io`** (must match `username.github.io`)
4. Set it to **Public**
5. Click **Create repository**

---

### Step 2 — Create a GitHub Fine-Grained Token

> **Gotcha:** If you ever delete and recreate the repo (even with the same name), the old token becomes invalid for the new repo. You must create a new token — the token is scoped to a specific repo ID, not just the name.

1. Go to GitHub → **Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens**
2. Click **Generate new token**
3. Set **Resource owner** to your account
4. Set **Expiration** (No expiration is fine for personal use)
5. Under **Repository access** → select **Only select repositories** → choose `chichimunga.github.io`
6. Under **Permissions** → **Repositories** → add:
   - **Contents** → Read and write
   - **Metadata** is auto-added as Read-only (required)
7. Click **Generate token** and **copy it immediately** — you only see it once

> **Gotcha:** If you need to push workflow files (`.github/workflows/`), you also need the **Workflows: Read and write** permission. Contents alone won't allow writing workflow files.

---

### Step 3 — Install the Plugin

The plugin files need to be placed in your vault's plugins folder. Install manually:

1. Download `main.js`, `manifest.json`, and `styles.css` from the latest release at **github.com/oleeskild/obsidian-digital-garden/releases**
2. Create the folder: `[your vault]/.obsidian/plugins/digitalgarden/`
3. Place the three files inside it
4. In Obsidian → **Settings** → **Community Plugins** → toggle **Digital Garden** on

---

### Step 4 — Configure the Plugin

In Obsidian → **Settings** → **Digital Garden**:

| Field | Value |
|---|---|
| Publish Platform | GitHub/Self Hosted |
| GitHub repo name | `chichimunga.github.io` |
| GitHub Username | `chichimunga` |
| GitHub token | *(paste your token)* |
| Base URL | `https://chichimunga.github.io` |
| Slugify Note URL | Off |

> **Gotcha:** The Base URL defaults to a Vercel URL. Change it to your actual GitHub Pages URL or sitemap/RSS generation will point to the wrong place.

When configured correctly, you should see **"Connected with full access"** under GitHub Authentication.

---

### Step 5 — Add the Deploy Workflow

> **Gotcha:** The template repo only includes a `build.yml` that checks for errors — it does NOT deploy to GitHub Pages. You must add a deploy workflow manually.

Create the file `.github/workflows/deploy.yml` in your repo with this content:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: ["main"]

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: dist

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
```

> **Gotcha:** The build output directory is `dist/` (not `_site/` as some 11ty projects use). Confirm by checking `.eleventy.js` → `dir.output`.

The easiest way to add this file: go to your repo on GitHub → **Add file** → **Create new file** → name it `.github/workflows/deploy.yml` → paste the content → commit to `main`.

---

### Step 6 — Configure GitHub Pages Source

1. Go to your repo → **Settings** → **Pages**
2. Under **Source**, select **GitHub Actions**
3. Save

> **Gotcha:** If Pages source is set to "Deploy from a branch" (the default), it serves your raw README — not your built garden.

---

### Step 7 — Publish Your Notes

1. In Obsidian, open the note you want to publish (e.g. `Home.md`)
2. Make sure it has `dg-publish: true` in its properties
3. Press **Cmd+P** → run **"Digital Garden: Open Publication Center"**
4. Expand the folder, check the note, click **Publish Selected**

After publishing, a commit is pushed to your repo, GitHub Actions builds the site, and it deploys to `https://chichimunga.github.io` within a minute or two.

---

### Ongoing Use

- To publish a single note: **Cmd+P** → **"Digital Garden: Publish Single Note"**
- To publish multiple notes at once: **Cmd+P** → **"Digital Garden: Open Publication Center"**
- Add `dg-publish: true` to any note's properties to make it publishable
- The homepage note must also have `dg-home: true`

---

### Summary of Gotchas

1. Create the repo from the **template**, not as a blank repo
2. Deleting and recreating the repo **invalidates your token** — create a new one
3. Writing workflow files requires the **Workflows** permission (separate from Contents)
4. Change the **Base URL** from the Vercel default to your GitHub Pages URL
5. The template's `build.yml` does **not deploy** — you must add `deploy.yml` yourself
6. Build output is **`dist/`**, not `_site/`
7. Set GitHub Pages source to **GitHub Actions**, not "Deploy from a branch"
