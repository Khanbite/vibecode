# 🚀 Deployment Guide for Vibecode

This document outlines the steps to deploy the **Vibecode** project using **GitHub Pages** and **GitHub Actions** for continuous deployment.

---

## 📁 Prerequisites

- A GitHub repository: [github.com/Khanbite/vibecode](https://github.com/Khanbite/vibecode)
- Node.js installed locally
- A production build command (e.g., `npm run build`) that outputs to a folder like `dist/` or `build/`

---

## 🛠️ Step 1: Set Up GitHub Pages

1. Go to your GitHub repository.
2. Navigate to **Settings** > **Pages**.
3. Under **Source**, select:
   - **Branch**: `gh-pages`
   - **Folder**: `/ (root)` or `/docs` depending on where your static files will live.
4. Click **Save**.

> ⚠️ If the `gh-pages` branch doesn't exist yet, it'll be created during the GitHub Actions deployment.

---

## ⚙️ Step 2: Add GitHub Actions Workflow

Create a file at `.github/workflows/deploy.yml` with the following content:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '16'

      - name: Install dependencies
        run: npm install

      - name: Build project
        run: npm run build

      - name: Deploy to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@4.1.7
        with:
          branch: gh-pages
          folder: dist
```

## ✅ Step 3: Verify Deployment

After pushing your changes to the `main` branch:

1. GitHub Actions will run the deployment workflow.
2. On success, your site will be live at:
   https://khanbite.github.io/vibecode/
