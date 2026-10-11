# Architecture

Trail Advisor is a static, browser-only website. The three HTML pages contain their own markup, CSS, and JavaScript. There is no application server, database, build step, API key, or telemetry pipeline.

## Runtime flow

1. `index.html` is the product landing page.
2. `explorer.html` loads MapLibre GL JS and an OpenFreeMap basemap. Its map toolbar handles basemap selection, combined city/trail search, nearby trail radius, browser geolocation display, and Google Maps deep links.
3. City suggestions and reverse labels use Photon. Trail suggestions and geometry use the USGS National Digital Trails ArcGIS service. Selecting a map point queries that point/radius for trails, the Forest Service recreation-site service for recorded facilities, NWS for point alerts and forecasts, and Photon for a nearby place label.
4. `advisories.html` accepts a place or coordinates and queries NWS active alerts. Alert scoring is a plain-language summary of returned alert severity, not a route safety rating.
5. Optional segment endpoint elevation uses USGS EPQS only after the user asks for it.

## Data and privacy boundaries

- Browser geolocation is displayed locally first. Coordinates are sent to the listed public providers only after the user selects a map point or searches for a place.
- A selected point is sent to USGS trails, Forest Service facilities, NWS, and Photon. The static app stores no location history.
- Provider requests happen in the visitor's browser. Provider availability, CORS policy, rate limits, and service behavior are outside this repository's control.
- Client-side validation and DOM rendering are used for user-supplied search text; do not construct HTML from provider or user text.

## Deployment

GitHub Actions publishes the repository root to GitHub Pages when changes land on `main`. The workflow is `.github/workflows/pages.yml`. Pages should be configured to use **GitHub Actions** as its deployment source. Alpha work is maintained on `alpha`, reviewed there, then fast-forwarded/merged into `main` for portfolio deployment.

## Key extension points

- Data endpoint URLs and trail querying/rendering are in the script of `explorer.html`.
- Theme tokens and responsive map layout are in the page-level styles in `explorer.html` and `advisories.html`.
- Public source terms, freshness, and coverage constraints are summarized in [data-sources.md](data-sources.md).
- There is currently no automated test or accessibility-audit job in CI; the Pages workflow deploys static files and does not gate publication on a test suite. For each change, record the checks actually performed in the PR description. At minimum, review affected pages in a browser, exercise keyboard focus and responsive layouts, and check empty/error states. Do not describe a manual check as an automated test.
