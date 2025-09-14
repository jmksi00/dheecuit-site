# .github/workflows/deploy.yml - GitHub Actions for secure deployment
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Pages
        uses: actions/configure-pages@v4
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

---

# _config.yml - Jekyll configuration for GitHub Pages
title: "DheeCuit - Personalized Meal Planning"
description: "Get custom diet-specific recipes, one-tap grocery lists, and stress-free meal prep — all in one AI-powered app."
url: "https://yourusername.github.io"
baseurl: "/dheecuit-website"

# Security settings
safe: true
plugins:
  - jekyll-sitemap
  - jekyll-feed

# Exclude files from processing
exclude:
  - README.md
  - LICENSE
  - .gitignore

---
