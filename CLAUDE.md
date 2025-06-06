# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
This is a Jekyll-based static website (onlyx.tech) using the Just the Docs theme. It's a personal blog/portfolio site for Stephen English with posts about technical projects and thoughts.

## Development Commands

### Local Development
```bash
bundle install          # Install dependencies
bundle exec jekyll serve # Build and serve locally at localhost:4000
```

### Site Structure
- Built site is generated in `_site/` directory
- Content pages are markdown files in the root directory
- Static assets are in `assets/` directory
- Site configuration is in `_config.yml`

## Content Management
- Each markdown file uses Jekyll front matter with `title`, `layout`, and `nav_order`
- The site uses the Just the Docs theme which provides navigation and styling
- Pages are automatically added to navigation based on their `nav_order` value

## Deployment
The site is deployed to GitHub Pages using GitHub Actions. Changes to the main branch automatically trigger a new build and deployment.