# Ham Spotter Locator

A mobile-optimized single-page web app for SKYWARN storm spotters to quickly report their position to the National Weather Service.

## Features

- **Nearest intersection** — Resolves your GPS coordinates to a road name and cross street
- **Nearest city/community** — Finds the closest named place (city, town, village, or hamlet) with distance and compass bearing (e.g. "2.4 mi SW of Skyline")
- **County & state** — Displays your current county and state
- **Maidenhead grid square** — Computes your 8-character ham radio grid locator
- **GPS coordinates** — Shows latitude, longitude, and accuracy in meters
- **Full-screen map** — Tap "Show Map" to open an interactive OpenStreetMap view centered on your location with a marker and accuracy circle; tap × to close
- **Auto-refresh** — Configurable interval (default 5 min) to re-poll GPS and update all fields
- **Manual refresh** — Force an immediate location update at any time
- **What3Words** — Button to open your location in the What3Words map
- **Error details** — Tap the status pill in the header to see the full error message if something goes wrong

## Data Sources

| Data | Source |
|------|--------|
| Road / intersection / county / state | OpenStreetMap via [Nominatim](https://nominatim.openstreetmap.org) |
| Cross street lookup | OpenStreetMap via [Overpass API](https://overpass-api.de) |
| Nearest city / community | OpenStreetMap via [Overpass API](https://overpass-api.de) |
| Map tiles | [OpenStreetMap](https://www.openstreetmap.org) via [Leaflet](https://leafletjs.com) |
| GPS coordinates | Browser Geolocation API |

## Usage

Open `index.html` from a web server — **do not open directly from disk**. Browsers block cross-origin API requests from `file://` URLs.

For local testing:

```bash
python3 -m http.server 8080
```

Then navigate to `http://localhost:8080`.

## Configuration

At the top of the `<script>` block in `index.html`:

```js
let intervalMinutes = 5;                       // Auto-refresh interval in minutes
const NOMINATIM_EMAIL = 'your@email.com';      // Required by OSM usage policy
```

Set `NOMINATIM_EMAIL` to your email address as required by the [Nominatim usage policy](https://operations.osmfoundation.org/policies/nominatim/).

## Icon

Place a file named `icon.png` in the same directory as `index.html` to display a custom icon in the header. Any size works; 512×512 is recommended for sharp rendering on high-DPI screens.

## License

Personal use. Data © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright).
