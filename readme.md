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

# robots.txt - SEO and security
User-agent: *
Allow: /

# Block sensitive paths (if any)
Disallow: /admin/
Disallow: /.git/

Sitemap: https://yourusername.github.io/dheecuit-website/sitemap.xml

---

# .htaccess - Security headers (for Apache servers)
# Note: GitHub Pages uses its own security headers, but good to have

# Security Headers
Header always set X-Frame-Options "SAMEORIGIN"
Header always set X-Content-Type-Options "nosniff"
Header always set X-XSS-Protection "1; mode=block"
Header always set Referrer-Policy "strict-origin-when-cross-origin"
Header always set Permissions-Policy "geolocation=(), microphone=(), camera=()"

# HTTPS Redirect (GitHub Pages handles this automatically)
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

---

# README.md - Documentation for your repository
# DheeCuit Landing Page

A modern, responsive landing page for DheeCuit - the AI-powered meal planning app.

## 🚀 Features

- Responsive design that works on all devices
- Modern gradient design with smooth animations
- Working email signup form
- SEO optimized
- Security best practices implemented

## 🔒 Security Features

- Input sanitization
- XSS protection
- Secure form handling
- HTTPS enforcement
- Security headers configured

## 📱 Live Demo

Visit: [https://yourusername.github.io/dheecuit-website](https://yourusername.github.io/dheecuit-website)

## 🛠️ Local Development

1. Clone the repository
2. Open `index.html` in your browser
3. Make changes and commit to deploy

## 📧 Form Integration

Currently stores emails in localStorage. For production, integrate with:
- [Formspree](https://formspree.io/) - Easy form backend
- [Netlify Forms](https://www.netlify.com/products/forms/) - If hosting on Netlify
- [EmailJS](https://www.emailjs.com/) - Send emails directly from frontend

## 📊 Analytics

Ready for integration with privacy-friendly analytics:
- [Plausible](https://plausible.io/)
- [Simple Analytics](https://simpleanalytics.com/)
- [Fathom](https://usefathom.com/)

## 📄 License

MIT License - Feel free to use for your projects!

---

# LICENSE - MIT License for your project
MIT License

Copyright (c) 2025 DheeCuit

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
