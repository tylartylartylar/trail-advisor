# Trail Advisor

A small outdoor-planning demo: explore a labeled map, find nearby published National Forest System trail sections, review available trail details and an optional elevation estimate, and check current U.S. weather, hourly forecasts, and advisories. It is a static site with no build step or API key.

## Why Trail Advisor exists

Trail Advisor is an independent portfolio project exploring a simple question: can trail, map, and official weather information be brought together in a useful, approachable planning tool? It is a learning/demo product, not an official emergency service, a replacement for land-manager guidance, or a claim that any route is safe. It currently focuses on U.S. public data and Forest Service trail coverage; the longer-term direction is clearer route context, more reliable and current trail conditions, and broader coverage where ethical, legal, and practical data sources exist.

The original branding uses a deep blue field palette, glacier-teal highlights, and a small waypoint mark to distinguish the project from commercial trail products. Light, dark, and red display modes are supported.

Built by Tylar as a personal portfolio project.

## Technology

- Plain HTML, CSS, and JavaScript; no framework, build pipeline, API key, or server-side application.
- [MapLibre GL JS](https://maplibre.org/) for the interactive map, with OpenFreeMap street tiles and USGS National Map topographic and aerial layers.
- USDA Forest Service ArcGIS services for published trail sections and recorded recreation-site amenities.
- National Weather Service API for alerts, point forecasts, and observations; USGS EPQS for optional endpoint elevation samples.
- Photon geocoding and OpenStreetMap-derived map data, with attribution and responsible-use notes in the interface.
- GitHub Pages can host the static site. Public provider availability, licensing, coverage, and rate limits should be rechecked before commercial use.

## Roadmap

### TODO

- Improve trail identity and continuity: join adjacent Forest Service trail sections and make whole-route distance less ambiguous.
- Add richer elevation profiles and cumulative ascent, with clear source and accuracy notes.
- Explore reliable, licensed trail-condition and closure data from land managers before estimating muddy, icy, dusty, or slippery conditions.
- Improve search coverage and handling for trails outside Forest Service lands.
- Add resilient data loading, caching, and clear stale-data timestamps before considering production use.
- Continue keyboard, screen-reader, mobile, and low-light accessibility reviews as features grow.

## Feedback

Use the [Trail Advisor suggestion form](https://github.com/tylartylartylar/trail-advisor/issues/new?template=suggestion.yml) to share an idea, usability issue, or accessibility observation. Feedback is submitted as a GitHub issue, so it is public and may include your GitHub username. Please do not include private location history or sensitive personal information.

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
2. On the explorer page, use the map toolbar to switch between Streets, topographic, and aerial imagery. Type at least three letters in the trail search to see Forest Service name suggestions, then choose one and select **Search**. Search terms are sent to the Forest Service only after typing a few characters; nearby trail data loads after selecting a map point. Select **Locate me** to request browser permission and show a blue location marker; this action alone does not send coordinates to an API. The expandable rows below the map contain trail, facility, forecast, and alert details. Select **Show on map** to highlight a trail section, mark the published geometry endpoints, and show a midpoint forecast. The Google Maps link opens the selected coordinates without embedding a paid Maps API.
3. Review the nearby weather section for the latest available NWS station observation and hourly forecast periods. The trail popup forecast is for one point near the mapped segment midpoint; neither display represents conditions along the whole trail.
4. On the advisories page, review the plain-language NWS alert signal and active alerts. The signal runs from 0 to 5 based on the highest alert severity returned near the selected point; it is a caution summary, not a trail-specific forecast or a safety guarantee.
5. Alternatively, enter a city, address, or ZIP code and select a suggestion, or choose **Use my location**. Review the status message, alert details, and any affected alert areas mapped by NWS.
6. Try Light, Dark, and Red display modes. The selected mode is shared between pages. In Red mode, opening NASA FIRMS or an official alert shows a brightness warning. **Continue and adjust my eyes** fades Trail Advisor to Light mode over 2.5 seconds, then opens the destination in a new tab.

## Data and known limits

- Weather and fire-weather alerts come from the National Weather Service and cover the United States and territories. Alert boundaries appear only when NWS provides geometry; this is not a fire-perimeter or evacuation map.
- Hourly point forecasts and latest nearby station observations are retrieved from the NWS API. Observations may be delayed, missing, or from a station far from a remote trail.
- Nearby trail geometry and attributes come from the USDA Forest Service National Forest System Trails publication layer. The dataset covers Forest Service trails, not all trails, and information availability varies by forest. Lengths describe individual mapped sections; they may not represent the full named route. Access and status must be confirmed with the land manager.
- Nearby facility information comes from the Forest Service Recreation Sites layer. It can include activity type, restrooms, water availability, accessibility notes, and current-conditions notes. Forest Service records cover only participating/recorded sites; null data does not mean a facility is absent, and listed amenities can be outdated. Verify details with the official site or local land manager.
- Optional endpoint elevations are queried from the USGS Elevation Point Query Service using the selected segment's first and last geometry points. The net endpoint difference does not represent total ascent or a full elevation profile.
- Selecting a map point sends its coordinates to the Forest Service trail and recreation-site services, the National Weather Service, and Photon for place naming. Coordinates are sent to USGS only when an elevation estimate is requested. Choosing **Locate me** displays your location in the browser and does not trigger those lookups until you select a map point. No location history is stored by this static demo.
- The alert signal uses only the severity of returned NWS alerts (Extreme, Severe, Moderate, Minor, or unspecified). It is not a probability, route assessment, or guarantee of safety. A zero means no active NWS alerts were returned for the point when checked.
- The explorer uses OpenFreeMap's Liberty vector style through MapLibre GL JS by default and offers USGS The National Map topographic and imagery tile services. USGS basemap data is generally public domain and attribution is included. Aerial imagery is not live, its age and resolution vary by region, and source imagery has regional licensing exceptions; confirm the specific imagery credits before commercial redistribution. The USGS topographic and imagery layers cover U.S. areas. Map labels and administrative boundaries vary by style and zoom. Clicking the map asks Photon, a public OpenStreetMap-based geocoder, for the nearest named place; exact labeling depends on available map data.
- Location autocomplete and map selection use Photon. Search text is sent to Photon while typing on the advisories page. Its demo server asks for reasonable use and has no availability guarantee.
- Public map and geocoder services are suitable for a low-traffic prototype, not a production availability guarantee. OpenStreetMap attribution is included.
- The site needs an internet connection for MapLibre, map tiles, geocoding, fonts, and NWS data. Public services can be unavailable or change their terms.
- A diagnostics panel on the advisories page can copy service response codes and error details from the current session. It does not record location coordinates or search text.

## Commercial use

The NWS API states its open data is free to use for any purpose, and USGS 3DEP and National Map data/services are generally public domain. The Forest Service trail and recreation-site layers are public agency data with attribution included; trail/amenity coverage and metadata are incomplete in some areas. The prototype consumes public agency services directly and those services do not offer this app an uptime guarantee.

OpenFreeMap states that its public map service is free for commercial use and has no request or view limits, but provides no SLA. Check the [OpenFreeMap quick start](https://openfreemap.org/quick_start/) and current service terms before launch. OpenStreetMap data is licensed under the ODbL and requires attribution. Photon is a public demo geocoder with usage limits. A commercial product would need to review each provider's current service terms, capacity, and any redistribution conditions before launch. Open-Meteo is not used because its free API tier is non-commercial only.

MapLibre GL JS is distributed under the BSD 3-Clause license. Trail Advisor is not an official emergency alert channel or land-manager source. Follow local emergency officials and land-manager guidance.
