# Partify PickPath Concept Demo

This is a mobile-first, offline-capable prototype for a warehouse pick-path workflow.

## Files
- `index.html` — UI, sample data, routing logic, and visual map
- `manifest.webmanifest` — lets the site behave like a home-screen web app
- `sw.js` — caches the app for offline use
- `icon-192.png` / `icon-512.png` — app icons

## Run locally on a laptop
Because service workers need HTTP/HTTPS (not a plain `file://` URL), use a local server:

```bash
cd partify_pickpath_demo
python3 -m http.server 8000
```

Then open:
`http://localhost:8000`

## Put it online with GitHub Pages
1. Create a new GitHub repository, for example `pickpath-demo`.
2. Upload every file from this folder to the repository root.
3. In the repository, open **Settings → Pages**.
4. Under deployment/source, choose the `main` branch and `/ (root)`.
5. Save and wait for GitHub Pages to publish the HTTPS link.
6. Open that link on the iPhone in Safari.

## Install on iPhone
1. Open the published HTTPS URL in Safari.
2. Let the page finish loading.
3. Reload it once so the service worker has definitely taken control.
4. Tap **Share**.
5. Tap **Add to Home Screen**.
6. Name it `PickPath`.
7. Open the new home-screen icon once while online.
8. Turn on Airplane Mode and open it again to verify offline use.

## What the demo does
- Choose among sample orders.
- Shows an intentionally simple "current / naïve" pick route.
- Uses Manhattan distance because a warehouse picker normally follows aisles rather than walking diagonally through shelves.
- Uses a nearest-neighbor routing heuristic: from the current location, pick the nearest remaining item.
- Optional physical constraint: small items first, bulky items last.
- Compares estimated route distance before and after optimization.
- Tap any recommended route step to highlight it on the map.

## Important
All layouts, SKUs, locations, distances, and savings are illustrative sample data. Do not present the numbers as Partify operational data.

## Future production direction
A real version could use:
- Python + FastAPI for backend APIs
- PostgreSQL / SQL Server for SKU, order, bin, and facility data
- Google OR-Tools for richer route and batching optimization
- Scanner/WMS integrations
- Real walking-path graph rather than Manhattan distance
- Cart capacity, one-way aisles, congestion, bulky-item handling, multiple pickers, and order priority
