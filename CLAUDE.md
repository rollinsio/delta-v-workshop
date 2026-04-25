# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-page marketing/landing page for a paid live-build session ("Agents Building Agents" — 2 hours: 60m build + 60m Q&A). The entire site is `index.html`; there is no build system, no package manager, no tests.

## Stack

- Static HTML in `index.html`.
- Tailwind CSS via CDN (`https://cdn.tailwindcss.com`) with an inline `tailwind.config` extending a `brand` color palette (`brand-400/500/600`). Do not introduce a Tailwind build step or `tailwind.config.js` unless the page outgrows the CDN — keep edits to the inline config block.
- No JS framework, no bundler. Open `index.html` directly in a browser to preview.

## Editing notes

- The page has four sections that must stay in sync when content changes: Hero (`<header>`), Details (`#details`) including the "Event Logistics" card, Requirements (`#requirements`) with two cards (skills + system setup), and Pricing (`#pricing`) with three tiers (Supported $29 / Standard $99 / Supporter $199). The Standard tier is visually highlighted (`border-brand-500`, translated up) — preserve that emphasis if restyling.
- Duration appears in three places that must stay aligned: hero subhead (implicit), Details intro paragraph ("2-hour live implementation session", "first hour … full hour"), and the Logistics card `Format` line. The FAQ also references "60-minute Q&A".
- Known placeholders to fill before launch (all listed in the `<head>` config comment):
  - `WORKSHOP_DATE` — appears in the hero badge and Logistics card.
  - `WORKSHOP_EMAIL` — used in the "Express interest" `mailto:` link and the plain-text fallback. Should be a Google Workspace alias/group on the owner's domain (no inbound server needed — site stays static).
  - `STRIPE_LINK_SUPPORTED` / `STRIPE_LINK_STANDARD` / `STRIPE_LINK_SUPPORTER` — Stripe Payment Link URLs (one per tier, generated in the Stripe Dashboard). Payment Links keep the site truly static: no Stripe keys live in the repo. Only switch to Stripe.js if a tier needs custom amounts or embedded checkout — and even then only the publishable key would be added (which is safe to commit; the secret key must never appear in this repo).
- Times listed in the hero badge ("Saturday, 9:00 AM PT") and Logistics ("9:00 AM PT / 12:00 PM ET / 5:00 PM UK / 9:30 PM IST") must be kept consistent across both blocks.
