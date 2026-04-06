# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

HyKr Build Challenge 2026 — a registration form for India's startup challenge (₹50 Lakhs prize pool). This is a **static single-page application** built with vanilla HTML5, CSS3, and ES6+ JavaScript. There is no framework, no package.json, no build system.

## Development

**Local dev:** Open `build-challenge-form/index.html` directly in a browser. No dev server needed.

**Deployment:** Copy `build-challenge-form/` to any static hosting (GitHub Pages, Netlify, S3, etc.). No build step required.

## Architecture

The entire app lives in `build-challenge-form/index.html` (~1900 lines) with inline CSS and JavaScript:

- **Multi-step form** (4 steps + success screen) controlled by `currentStep` state variable
- **Key functions:** `validateStep()`, `nextStep()`, `prevStep()`, `collectFormData()`, `submitForm()`
- **Form submission:** POST to Zapier webhook (`hooks.zapier.com`) with JSON payload + ISO timestamp
- **Validation:** Client-side only — regex for email/phone, HTTPS check for URLs, 300-word limit on text fields with real-time word counters

### Form Steps

1. Lead Founder & Team Details (name, email, phone, city, linkedin, team info)
2. Challenge Theme Selection (10 themes across Deep Tech, Health & Bio, Construction)
3. Idea & Background (problem/solution, customer focus, business model, background)
4. Review & Submit (dynamic summary of all entered data)

### Analytics

Google Tag Manager (GTM-PJXGLHGV), Facebook Pixel, and Microsoft Clarity are embedded for tracking.

## Conventions

- All styles and scripts are inline in the single HTML file — no external CSS/JS files
- Custom fonts (Stack Sans) loaded from CDN
- Phone validation assumes Indian format (`+91 XXXXXXXXXX`)
- `request.js` is a reference/example file for the fetch call, not imported by the app
