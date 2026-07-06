# Technical Documentation - Sol Spy Telegram Mini App

This document outlines the technical details and architecture of the **Sol Spy** Telegram Mini App (TMA).

## Tech Stack
- **Framework**: Astro.js (v7.x)
- **Styling**: Tailwind CSS (v4.x) using `@tailwindcss/vite`
- **Logic**: Vanilla JavaScript running client-side

## Core Integrations

### 1. Telegram Web App SDK
- Script included in `src/layouts/Layout.astro` via `<script src="https://telegram.org/js/telegram-web-app.js" is:inline></script>`.
- Initialized in the browser:
  - `window.Telegram.WebApp.ready()` tells the Telegram client the app is loaded and ready.
  - `window.Telegram.WebApp.expand()` expands the mini app to full viewport height for optimal mobile styling.
  - Custom header and background color styling applied dynamically to match the cyber-dark slate theme.

### 2. DexScreener API
- Endpoint: `https://api.dexscreener.com/latest/dex/search?q=solana`
- Purpose: Retrieve real-time metrics of active pairs.
- Filtering Rules:
  - Keep only pairs where `chainId === 'solana'`.
  - Filter out duplicates of base tokens to show 5 unique assets.
  - Sort descending by 24h volume (`volume.h24`).
- Refreshed automatically every 30 seconds to keep track of active pumps.

### 3. Viral Loop & Unlock
- Target: 4th and 5th cards are locked behind a blur layer.
- Action: Share button triggers Telegram's native share deep link.
- Unlock: Uses standard CSS transition classes (removing opacity, blur, and pointer events restrictions) triggered after a 2-second timeout to simulate validation.

## Performance Optimization
- **Zero Client-Side Framework Overhead**: Fully written in vanilla JS inside Astro to keep initial JS bundle size under ~50KB.
- **Progressive Image/Text Load**: Immediate page rendering with skeleton loaders to minimize Largest Contentful Paint (LCP) and Cumulative Layout Shift (CLS).
- **Polling Throttling**: The 30s auto-refresh polling is paused when the tab goes background (`document.hidden === true`) to conserve battery and API limits on mobile.
