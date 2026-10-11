# Trail Advisor

A small outdoor-planning demo: search for a city or public trail, explore a labeled map, review quality-reviewed agency trail records, and check current U.S. weather, forecasts, and advisories. It is a static site with no build step or API key.

## Why Trail Advisor exists

Trail Advisor is an independent portfolio project exploring a simple question: can trail, map, and official weather information be brought together in a useful, approachable planning tool? It is a learning/demo product, not an official emergency service, a replacement for land-manager guidance, or a claim that any route is safe. It focuses on U.S. public data and uses the USGS National Digital Trails aggregation, which draws from public federal, state, and some local agency sources. The longer-term direction is clearer route context, more reliable and current trail conditions, and broader coverage where ethical, legal, and practical data sources exist.

The original branding uses a deep blue field palette, glacier-teal highlights, and a small waypoint mark to distinguish the project from commercial trail products. Light, dark, and red display modes are supported.

Built by Tylar as a personal portfolio project.

## Technology

- Plain HTML, CSS, and JavaScript; no framework, build pipeline, API key, or server-side application.
- [MapLibre GL JS](https://maplibre.org/) for the interactive map, with OpenFreeMap street tiles and USGS National Map topographic and aerial layers.
- USGS National Digital Trails ArcGIS service for quality-reviewed public federal, state, and some local trail records; USDA Forest Service ArcGIS for recorded recreation-site amenities.
- National Weather Service API for alerts, point forecasts, and observations; USGS EPQS for optional endpoint elevation samples.
- Photon geocoding and OpenStreetMap-derived map data, with attribution and responsible-use notes in the interface.
- GitHub Pages can host the static site. Public provider availability, licensing, coverage, and rate limits should be rechecked before commercial use.

## Roadmap

### TODO

- Improve trail identity and continuity: join adjacent source trail sections and make whole-route distance less ambiguous.
- Add richer elevation profiles and cumulative ascent, with clear source and accuracy notes.
- Explore reliable, licensed trail-condition and closure data from land managers before estimating muddy, icy, dusty, or slippery conditions.
- Expand coverage responsibly where official public sources are available, and publish source-level coverage notes.
- Add resilient data loading, caching, and clear stale-data timestamps before considering production use.
- Continue keyboard, screen-reader, mobile, and low-light accessibility reviews as features grow.

## Feedback

Use the [Trail Advisor suggestion form](https://github.com/tylartylartylar/trail-advisor/issues/new?template=suggestion.yml) to share an idea, usability issue, or accessibility observation. Feedback is submitted as a GitHub issue, so it is public, requires a GitHub sign-in, and may include your GitHub username. Please do not include private location history or sensitive personal information.

## GitHub Pages

The workflow in `.github/workflows/pages.yml` publishes the static site on pushes to `main`. In the repository, set **Settings → Pages → Build and deployment → Source** to **GitHub Actions**. The expected site address is <https://tylartylartylar.github.io/trail-advisor/> once Pages is enabled and the first deployment succeeds.

## Run locally

Serve the folder from localhost so browser location permission works:

```powershell
py -m http.server 8000
```

Then open <http://localhost:8000>. Stop the server with `Ctrl+C`.

## Tester walkthrough

1. Start at the home page and choose **Explore the map** or **View current advisories**.
2. On the explorer page, use the map toolbar to switch between Streets, topographic, and aerial imagery. Search for a city or trail name. Suggestions identify **City** and **Trail** matches; choosing a city centers the map and opens the nearby-trails results, while a trail search returns matching mapped sections. For a selected pin, **Nearby trail radius** controls how far (5 to 1,000 miles) to look for the nearest trail records. The list shows up to eight nearby segments. Trail searches are sent to the USGS service and city suggestions to Photon only after typing a few characters. Select **Locate me** to request browser permission and show a blue location marker; this action alone does not send coordinates to an API. The expandable rows below the map contain trail, facility, forecast, and alert details. Select **Show on map** to highlight a trail section, mark the geometry endpoints, and show a midpoint forecast. The Google Maps link opens the selected coordinates without embedding a paid Maps API.
3. Review the nearby weather section for the latest available NWS station observation and hourly forecast periods. The trail popup forecast is for one point near the mapped segment midpoint; neither display represents conditions along the whole trail.
4. On the advisories page, review the plain-language NWS alert signal and active alerts. The signal runs from 0 to 5 based on the highest alert severity returned near the selected point; it is a caution summary, not a trail-specific forecast or a safety guarantee.
5. Alternatively, enter a city, address, or ZIP code and select a suggestion, or choose **Use my location**. Review the status message, alert details, and any affected alert areas mapped by NWS.
6. Try Light, Dark, and Red display modes. The selected mode is shared between pages. In Red mode, opening NASA FIRMS or an official alert shows a brightness warning. **Continue and adjust my eyes** fades Trail Advisor to Light mode over 2.5 seconds, then opens the destination in a new tab.

## Data and known limits

- Weather and fire-weather alerts come from the National Weather Service and cover the United States and territories. Alert boundaries appear only when NWS provides geometry; this is not a fire-perimeter or evacuation map.
- Hourly point forecasts and latest nearby station observations are retrieved from the NWS API. Observations may be delayed, missing, or from a station far from a remote trail.
- Nearby and name-searched trail geometry and attributes come from the USGS National Digital Trails ArcGIS layer. USGS says its aggregation is sourced from official public data, reviewed for data quality, and includes federal, state, and some local sources. It does not include every trail; non-federal sources may be refreshed every 3–5 years, so records can be incomplete or stale. The service allows up to 2,000 records per query and the app displays up to the eight nearest segments for nearby searches. Lengths describe individual mapped sections, not necessarily a complete named route. Where present, each result identifies the source agency/maintainer. Confirm access, seasonal status, and current conditions with that maintainer.
- Nearby facility information comes from the Forest Service Recreation Sites layer. It can include activity type, restrooms, water availability, accessibility notes, and current-conditions notes. Forest Service records cover only participating/recorded sites; null data does not mean a facility is absent, and listed amenities can be outdated. Verify details with the official site or local land manager.
- Optional endpoint elevations are queried from the USGS Elevation Point Query Service using the selected segment's first and last geometry points. The net endpoint difference does not represent total ascent or a full elevation profile.
- Selecting a map point sends its coordinates to the USGS trail and Forest Service recreation-site services, the National Weather Service, and Photon for place naming. Coordinates are sent to USGS EPQS only when an elevation estimate is requested. Choosing **Locate me** displays your location in the browser and does not trigger those lookups until you select a map point. No location history is stored by this static demo.
- The alert signal uses only the severity of returned NWS alerts (Extreme, Severe, Moderate, Minor, or unspecified). It is not a probability, route assessment, or guarantee of safety. A zero means no active NWS alerts were returned for the point when checked.
- The explorer uses OpenFreeMap's Liberty vector style through MapLibre GL JS by default and offers USGS The National Map topographic and imagery tile services. USGS basemap data is generally public domain and attribution is included. Aerial imagery is not live, its age and resolution vary by region, and source imagery has regional licensing exceptions; confirm the specific imagery credits before commercial redistribution. The USGS topographic and imagery layers cover U.S. areas. Map labels and administrative boundaries vary by style and zoom. Clicking the map asks Photon, a public OpenStreetMap-based geocoder, for the nearest named place; exact labeling depends on available map data.
- Location autocomplete and map selection use Photon. Search text is sent to Photon while typing on the advisories page. Its demo server asks for reasonable use and has no availability guarantee.
- Public map and geocoder services are suitable for a low-traffic prototype, not a production availability guarantee. OpenStreetMap attribution is included.
- The site needs an internet connection for MapLibre, map tiles, geocoding, fonts, and NWS data. Public services can be unavailable or change their terms.
- A diagnostics panel on the advisories page can copy service response codes and error details from the current session. It does not record location coordinates or search text.

## Commercial use

The NWS API states its open data is free to use for any purpose. USGS identifies the National Digital Trails data as public domain, including data it aggregates from official public sources; source metadata is retained in results when available. USGS trail coverage and update intervals vary, and USGS services do not provide this app an uptime guarantee. The Forest Service recreation-site layer remains limited to recorded agency facilities, with incomplete coverage and metadata in some areas.

OpenFreeMap states that its public map service is free for commercial use and has no request or view limits, but provides no SLA. Check the [OpenFreeMap quick start](https://openfreemap.org/quick_start/) and current service terms before launch. OpenStreetMap data is licensed under the ODbL and requires attribution. Photon is a public demo geocoder with usage limits. A commercial product would need to review each provider's current service terms, capacity, and any redistribution conditions before launch. Open-Meteo is not used because its free API tier is non-commercial only.

MapLibre GL JS is distributed under the BSD 3-Clause license. Trail Advisor is not an official emergency alert channel or land-manager source. Follow local emergency officials and land-manager guidance.

## Engineering docs

- [Architecture and data flow](docs/architecture.md)
- [Data sources, coverage, and licensing notes](docs/data-sources.md)
- [Contribution and review process](CONTRIBUTING.md)
- [Security reporting](SECURITY.md)
- [Release history](CHANGELOG.md)

The project currently uses `main` for the published portfolio demo and `alpha` for active pre-release changes. Alpha milestones are marked with pre-release tags (for example, `v0.1.0-alpha.1`). See [CONTRIBUTING.md](CONTRIBUTING.md) for the branch, change, and release conventions.
