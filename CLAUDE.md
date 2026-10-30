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
- `leaderboards.html` — bi-weekly (quincenal) Clash.GG wager race: hero with stats and affiliate buttons, metallic top-3 podium, race progress bar, and ranking list for #4+. Its look deliberately mirrors the DropsClub race page (drops-club.com/leaderboard/krush) — keep that styling when editing it.
- Assets: `clash.jpg` (sponsor banner), `favicon.jpg` (index favicon), `gem.webp` (Clash gem icon, also leaderboard favicon).

Each page is fully self-contained: its CSS lives in an inline `<style>` and its JS in an inline `<script>`. There is no shared stylesheet or script, so the header/nav and base styles are **duplicated** in both files — a change to either must be made in both pages. Only `index.html` has the falling-particle canvas; the leaderboard uses a CSS diagonal-stripe background instead. The two files use different formatting (`index.html` minified one-rule-per-line CSS; `leaderboards.html` expanded); match the style of the file being edited.

External dependencies (CDN only): Google Fonts Poppins; Font Awesome 6.5.0 (header nav icons on both pages, footer icons on index).

## Things to know

- All leaderboard content is rendered by JS from the `LEADERBOARD` object at the top of the `leaderboards.html` script (prize pool, period length, `endsAt`, `updatedAt`, affiliate `code`/`referral`, `rewards` per rank, `players`). There is no API; updating standings means editing that object. Players are sorted by `wagered`; podium is rendered in visual order 2nd, 1st, 3rd (`.podium-2/1/3`). Race start, day count and progress are derived from `endsAt` − `periodDays`, rolling forward when the date passes. Player names are still placeholders and `endsAt` is an example date.
- `rewards` should sum to `prizePool`; the index page's "Top N Premiados" card and prize-pool counter (`target=500`) are hardcoded and must be kept in sync by hand.
- The Discord footer icon is commented out until there's an invite link.
- Accent colors: purple `#9146FF` (primary), gold/silver/bronze for podium, orange `#ffb347` for table ranks, cyan `#00d4ff` for the sponsor card.
