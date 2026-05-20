# Ham Spotter Locator — Claude Instructions

## Project Overview
A mobile-optimized single-page web app for SKYWARN storm spotters to report their GPS position. All code lives in a single `index.html` file.

## Deployment
- Hosted at `tracker.wx0mik.radio` on a DigitalOcean VPS (Ubuntu, Apache)
- Deploy path: `/mnt/volume_nyc3_01/www/tracker.wx0mik.radio/`
- GitHub Actions auto-deploys on every push to `main` via rsync as `root`
- Workflow: `.github/workflows/deploy.yml`

## Rules
- **Always update the footer version and date on every code change.** Format: `v1.x (YYYY-MM-DD)`. Increment the minor version with each change.
- Commit and push only when the user explicitly asks.
- Keep all code in `index.html` — do not split into separate files unless explicitly asked.

## Data Sources
- Road / intersection / county / state: Nominatim (`https://nominatim.openstreetmap.org`)
- Cross street & nearest city: Overpass API (`https://overpass-api.de`)
- Map tiles: OpenStreetMap via Leaflet

## Key Implementation Details
- **Cross street lookup** — adaptive radius: tries 100m → 200m → 400m until a result is found; results ranked by OSM highway classification (motorway=1 through service=9)
- **Nearest city** — excludes OSM `locality` type (used for subdivisions); weighted by place type so cities rank above closer hamlets (city 0.2×, town 0.4×, village 0.7×, hamlet 1.0×)
- **Timestamp display** — shows both last updated time and next scheduled update time
