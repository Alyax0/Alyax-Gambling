# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static two-page community site for the streamer "Alyax" (Clash.GG affiliate, Kick/YouTube). Plain HTML/CSS/JS — no build step, package manager, framework, linter, or tests. Site copy is in Spanish (`lang="es"`); keep new user-facing text in Spanish unless told otherwise. Changes are often uploaded directly through the GitHub web UI (`Alyax0/Alyax-Gambling`), so the repo history is mostly "Update index.html"-style commits.

## Running

Open `index.html` directly in a browser, or serve the folder to avoid file:// quirks with the Kick iframe:

```bash
python -m http.server 8000
```

## Structure

- `index.html` — landing page: hero, animated prize-pool counter, Clash.GG sponsor card (referral link `https://clash.gg/r/ALYAX`), YouTube Shorts cards (thumbnails pulled from `img.youtube.com/vi/<id>/hqdefault.jpg`), embedded Kick player (`player.kick.com/alyaxgg`), social footer.
- `leaderboards.html` — weekly wager leaderboard: prize box with countdown text, top-3 podium cards, and a table for ranks 4+.
- Assets: `clash.jpg` (sponsor banner), `favicon.jpg` (index favicon), `gem.webp` (Clash gem icon, also leaderboard favicon).

Each page is fully self-contained: its CSS lives in an inline `<style>` and its JS in an inline `<script>`. There is no shared stylesheet or script, so the header/nav, base styles, and the falling-particle canvas animation are **duplicated** in both files — a change to any of those must be made in both pages. The two files use different formatting (`index.html` minified one-rule-per-line CSS; `leaderboards.html` expanded); match the style of the file being edited.

External dependencies (CDN only): Google Fonts Poppins; Font Awesome 6.5.0 (index only, for footer icons).

## Things to know

- All leaderboard data is hardcoded placeholder HTML (names, wagers, rewards, `i.pravatar.cc` avatars, the "Termina en …" timer text). The index prize-pool counter just animates to a hardcoded `target=500`. There is no API integration; updating standings means editing the markup.
- Podium order in the markup is 2nd, 1st, 3rd (so 1st renders in the middle); rank classes are `.first`/`.second`/`.third`.
- The nav in `leaderboards.html` links to `leaderboard.html` (singular), which does not exist — the real file is `leaderboards.html`.
- Discord and X/Twitter footer links are `href="#"` placeholders.
- Accent colors: purple `#9146FF` (primary), gold/silver/bronze for podium, orange `#ffb347` for table ranks, cyan `#00d4ff` for the sponsor card.
