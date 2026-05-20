# Colorado 14ers Tracker

An interactive summit tracker for all 58 of Colorado's 14,000+ foot peaks — built with Claude and the AllTrails MCP connector.

![Colorado 14ers Tracker](https://img.shields.io/badge/peaks-58-26c6da?style=flat-square) ![Built with Claude](https://img.shields.io/badge/built%20with-Claude-ab47bc?style=flat-square) ![AllTrails](https://img.shields.io/badge/data-AllTrails%20MCP-4ade80?style=flat-square)

---

## What it is

A single-file HTML app for tracking your progress on the Colorado 14ers. No account, no server, no build step — open it in a browser and go.

**Three views:**

- **Map** — Google Maps satellite view with all 58 peaks marked. Cyan = unclimbed, purple = summited. Click any marker to pull up trail details.
- **Panorama** — Isometric terrain canvas showing all peaks in a west-to-east landscape view. Filter by range and only that range's peaks stay bright.
- **List** — Sortable table of all 58 peaks. Sort by name, elevation, class, range, distance, or rating.

**Left sidebar:**
- Filter by difficulty class (1–4)
- Filter by mountain range (6 ranges)
- Toggle unclimbed-only or hide sub-peaks
- Scrollable peak list — click any peak to select it

**Right panel:**
- Trail details: elevation, gain, distance, difficulty stars
- Class-specific prep notes (what gear, what skills)
- Direct link to the trail on AllTrails

**Progress tracking:** Check peaks off as you summit them. Progress saves to `localStorage` — persists between sessions without any account.

---

## Data disclaimer

> This tool uses the official AllTrails MCP connector, published by AllTrails for integration with AI assistants like Claude. Trail data is sourced directly through AllTrails' supported integration — no scraping or unofficial APIs are involved. AllTrails' terms of service and privacy policy govern data use and are subject to change; anyone using or building on this tool should review the latest policies at [alltrails.com](https://www.alltrails.com).

---

## How it was built

This project was built entirely through conversation with Claude — no code written by hand.

**Phase 1 — Claude Code (data + initial build):**
The AllTrails MCP connector was used to probe real trail data before any UI was designed. Claude compiled all 58 peaks from USGS/14ers.com sources, enriched with AllTrails trail data, and built the initial three-view app (map, list, panorama) as a self-contained HTML file.

**Phase 2 — Claude Code (design iteration):**
Full color system redesign to a tactical/satellite mapping aesthetic — dark background, teal/cyan (#26c6da) accents, purple (#ab47bc) for summited peaks. The panorama view was redesigned from abstract SVG cards to an isometric canvas terrain with three parallax depth layers.

**Phase 3 — Claude Cowork (shipping):**
Google Maps integration, hero header with onboarding copy, range filtering wired into the terrain canvas, UI polish (green section headers, info icon tooltips, collapse buttons), and a series of bug fixes including a script-ordering issue that prevented the map from loading on first render.

The full build process is documented in `14ers-build-processv2.md` — including design decisions, AllTrails data policy research, technical architecture notes, and prompting observations.

---

## Setup

### Run locally

Just open `Colorado 14ers v4 - working.html` in any modern browser. No server needed.

### Google Maps

The app uses a Google Maps JavaScript API key for the satellite map view. The included key is development-only and rate-limited. To use your own:

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a project and enable the **Maps JavaScript API**
3. Create an API key under **APIs & Services → Credentials**
4. In the HTML file, find both instances of the key string and replace:
   ```
   AIzaSyBnQ34cb15BlEiQiFTc7yuIF_3X6_akMs4
   ```
5. After deploying, restrict the key to your domain (see [Restricting your API key](#restricting-your-api-key) below)

### Deploy

The file is fully self-contained — deploy anywhere that serves static HTML:

- **Netlify**: drag and drop the HTML file at [app.netlify.com](https://app.netlify.com)
- **GitHub Pages**: push to a repo, enable Pages under Settings → Pages → Deploy from branch
- **Vercel**: `npx vercel` in the folder

### Restricting your API key

After deploying, lock down your Google Maps key so it can only be used from your domain:

1. Go to [console.cloud.google.com](https://console.cloud.google.com) → **APIs & Services → Credentials**
2. Click your key → **Edit**
3. Under **Application restrictions** → select **Websites**
4. Add your deployed URL: `https://your-site.com/*`
5. Under **API restrictions** → select **Maps JavaScript API** only
6. Save — changes take up to 5 minutes to propagate

---

## Tech stack

- Vanilla HTML/CSS/JS — zero dependencies, zero build step
- Canvas 2D API for the terrain view
- Google Maps JavaScript API for satellite map
- `localStorage` for summit progress persistence
- AllTrails MCP connector for trail data

---

## The 58 peaks

Colorado's "14ers" are peaks above 14,000 feet. The traditional count of 58 includes 53 peaks with 300+ feet of topographic prominence plus 5 conventional sub-peaks that are climbed as part of classic routes:

- Mount Cameron (sub-peak of Mt. Lincoln)
- Conundrum Peak (sub-peak of Castle Peak)
- North Maroon Peak (sub-peak of South Maroon)
- Challenger Point (sub-peak of Kit Carson)
- North Eolus (sub-peak of Mt. Eolus)

Peaks span 6 ranges: Sawatch (15), San Juan (15), Sangre de Cristo (10), Elk Mountains (7), Front Range (6), Mosquito (5).

---

## Difficulty classes

This tracker uses the Yosemite Decimal System (YDS), the standard for Colorado mountaineering — not AllTrails' Easy/Moderate/Hard scale:

| Class | What it means |
|-------|--------------|
| 1 | Trail hiking — no technical skills required |
| 2 | Off-trail scrambling, basic route-finding |
| 3 | Hands-on scrambling with exposure — a fall could injure |
| 4 | Technical climbing — rope recommended, falls can be fatal |

---

## Acknowledgements

Trail data sourced through the [AllTrails MCP connector](https://www.alltrails.com/mcp) — an officially published integration by AllTrails for use with AI assistants. Built with [Claude](https://claude.ai) by Anthropic.

Peak data: USGS, [14ers.com](https://www.14ers.com), AllTrails.

---

*Built May 2026 · Open to PRs and issues*
