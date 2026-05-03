# Field Locator

A lightweight Progressive Web App (PWA) that displays your current GPS position with a set of field-useful data readouts. Works offline after the first load and can be installed directly to your phone's home screen.

**Live app:** `https://yourusername.github.io/locator_app/`

---

## Features

| Readout | Details |
|---|---|
| **Latitude / Longitude** | High-accuracy GPS, updated every 30 seconds |
| **Maidenhead Grid Square** | 6-character locator (e.g. `EN35ab`) |
| **Sunrise / Sunset** | Local time, calculated from your position using the NOAA solar algorithm |
| **Day Length** | Hours and minutes of daylight |
| **UTC Clock** | Live seconds display |
| **Local Clock** | Live seconds display with timezone abbreviation |
| **State / County** | Reverse geocoded via OpenStreetMap Nominatim (requires network) |
| **GPS Accuracy** | Meter-level accuracy badge, warns if fix is poor |

- Auto-refreshes location every **30 seconds** with a countdown timer
- Manual **Refresh** button resets the countdown
- **Offline banner** appears automatically when network is unavailable
- Adapts to **light and dark mode** automatically

---

## Installing on Your Phone

### iPhone / iPad (Safari)
1. Open the app URL in **Safari** (not Chrome or Firefox)
2. Tap the **Share** button (box with arrow) at the bottom of the screen
3. Scroll down and tap **Add to Home Screen**
4. Confirm the name and tap **Add**
5. On first launch, allow location access when prompted

### Android (Chrome)
1. Open the app URL in **Chrome**
2. Look for an **Install app** banner at the bottom — tap it
3. If no banner appears, tap the **⋮ menu** → **Add to Home Screen**
4. Tap **Add** to confirm
5. On first launch, allow location access when prompted

> The app caches itself on first load so it runs fully offline after that. State and county lookup requires a network connection.

---

## How It Works

Everything except the reverse geocoder runs locally with no external dependencies:

- **GPS** — Browser [Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API)
- **Maidenhead Grid** — Calculated from lat/lon using the standard amateur radio algorithm
- **Sunrise / Sunset** — [NOAA Solar Calculator](https://gml.noaa.gov/grad/solcalc/) algorithm implemented in JavaScript
- **State / County** — [Nominatim](https://nominatim.org/) reverse geocoding API (OpenStreetMap data, free, no API key required)
- **Offline support** — Service worker caches `index.html` and `manifest.json` on first visit

---

## Project Structure

```
locator_app/
├── index.html      # Entire app — HTML, CSS, and JavaScript
├── manifest.json   # PWA manifest (name, icon, display mode)
├── sw.js           # Service worker (offline caching)
└── README.md
```

The app is intentionally a single self-contained HTML file with no build tools, no frameworks, and no dependencies beyond two Google Fonts loaded at runtime.

---

## Deploying

The app is hosted via [GitHub Pages](https://pages.github.com/). To deploy your own copy:

1. Fork or clone this repo
2. Go to **Settings → Pages** in your GitHub repo
3. Set source to **Deploy from branch → main → / (root)**
4. Visit `https://yourusername.github.io/locator_app/`

---

## Privacy

- Location data never leaves your device except for the Nominatim reverse geocode request (lat/lon sent to OpenStreetMap servers to look up state/county)
- No analytics, no tracking, no cookies
- No API keys required

---

## License

MIT
