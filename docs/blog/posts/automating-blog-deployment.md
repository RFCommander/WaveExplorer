---
date: 2025-06-24
categories:
  - Development
tags:
  - GitHub Actions
  - CI/CD
---

![Banner Image](../../assets/images/banners/polygonal19.jpg){ .banner-image }

# Automating Blog Deployment with GitHub Actions

In this post, I'll show you how I automated the deployment of this blog using GitHub Actions. We'll cover setting up continuous integration to check markdown files and automatically deploy to GitHub Pages.

<!-- more -->

## Why Automation?

Automation helps ensure:

1. Consistent quality through linting
2. Automatic deployment on merges
3. No manual deployment steps
4. Version control and review process

## Setting Up GitHub Actions

Here's how we set up our GitHub Actions workflow:

```yaml
name: CI
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Lint Markdown files
        uses: DavidAnson/markdownlint-cli2-action@v15

  deploy:
    needs: lint
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
      - run: pip install mkdocs-material
      - run: mkdocs gh-deploy --force
```

## Results

Now, every time we push to main:

1. Markdown files are checked for consistency
2. The site is automatically built and deployed
3. Changes are live within minutes

This automation has made maintaining the blog much easier!
