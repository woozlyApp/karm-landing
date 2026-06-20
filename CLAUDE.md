# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Stack

Pure HTML/CSS. No build step, no framework, no JS, no package manager. GitHub Pages serves `main` branch root directly at `karm.woozly.app`.

## Previewing

Open any `.html` file directly in a browser — no server needed. For accurate `prefers-color-scheme` testing, use browser dev tools to force light/dark mode.

## Structure

```
index.html          ← Landing page (hero + App Store badge)
support/index.html  ← Support FAQ page
privacy-policy/index.html ← Privacy policy page
icon.png            ← App icon (96×96, from Karm iOS assets)
CNAME               ← karm.woozly.app
app-ads.txt         ← Google AdMob verification
```

## Design System

All styles are inline in each HTML file. The landing page (`index.html`) uses CSS custom properties and matches the Karm iOS app design:

- **Font:** DM Sans via Google Fonts CDN (only on landing page; support/privacy use system font stack)
- **Colors:** dark `#141F16` bg / `#F2F6F3` text; light `#F3F5F2` bg / `#1A2A1E` text — driven by `prefers-color-scheme`
- **Text opacity levels:** primary (full), secondary (0.6), footer (0.45)
- **App icon radius:** `border-radius: 22px` (iOS approximation)

Support and privacy-policy pages intentionally use a simpler style (system font, black text on white) — not the dark/green design system.

## Deployment

Push to `main` → GitHub Pages auto-deploys. No CI, no build artifacts.

## App Details

- App Store: `https://apps.apple.com/us/app/karm-tasks-that-follow/id6778794889`
- Support email: `dev.karm.app@gmail.com`
- "Karm" is the Sanskrit word for work
- Data is 100% local (no accounts, no sync); ads via Google AdMob
