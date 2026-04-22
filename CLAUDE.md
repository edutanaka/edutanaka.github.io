# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static HTML site for edutanaka.me (personal portfolio/landing page), deployed via GitHub Pages. No build system — files are served as-is.

## Deployment

`git push` to `main` deploys automatically via GitHub Pages. The `.nojekyll` file disables Jekyll processing so raw HTML is served directly. The custom domain is configured in `CNAME` (`edutanaka.me`).

## Architecture

Each directory is an independent mini-app or page:

- **`index.html`** — Main landing page: dark space-themed with CSS animations (stars, nebula, typing effect) and Google Tag Manager (GTM-P9646W2Z) via first-party server-side endpoint `st.edutanaka.me`.
- **`test.html`** — Staging/testing page used to try analytics integrations before promoting to `index.html`.
- **`whatsapp/`** — WhatsApp Business API embedded signup flow; communicates with Facebook SDK and handles `FINISH`/`CANCEL`/`ERROR` postMessage events.
- **`chatwoot/`** — Chatwoot dashboard app; uses postMessage API for iframe communication.
- **`politica-privacidade.html` / `termo-uso.html`** — Legal pages in Portuguese.

## Analytics & Integrations

The site integrates multiple analytics and marketing tools. Changes here are sensitive:

- **Google Tag Manager** (`GTM-P9646W2Z`) — loaded on `index.html` via first-party server-side container at `st.edutanaka.me`.
- **RudderStack** — currently on `test.html` only; key `38nVyRQkSUXQU7qeADacsNDy6G2`, dataplane `edutanakaifrbb.dataplane.rudderstack.com`.
- **Meta / Facebook SDK** — used in `whatsapp/index.html` for embedded signup.

When moving an integration from `test.html` to `index.html` (or vice versa), verify the SDK snippet, write key/endpoint, and any event calls are all transferred consistently.
