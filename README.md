# Trail Advisor

A small outdoor-planning demo: start at a simple home page, explore a labeled world map, and check current U.S. weather and fire-weather advisories for a place. It is a static site with no build step or API key.

## Run locally

Serve the folder from localhost so browser location permission works:

```powershell
py -m http.server 8000
```

Then open <http://localhost:8000>. Stop the server with `Ctrl+C`.

## Tester walkthrough

1. Start at the home page and choose **Explore the map** or **View current advisories**.
2. On the explorer page, zoom around the map to see city/locality labels and country/state/provincial boundaries at increasing detail. Click a point to check active NWS alerts at that pin. A compact alert preview appears beside the pin; use **Full alert details** or scroll below the map for the complete list and affected-area mapping.
3. On the advisories page, review the plain-language NWS alert signal and active alerts. The signal runs from 0 to 5 based on the highest alert severity returned near the selected point; it is a caution summary, not a trail-specific forecast or a safety guarantee.
4. Alternatively, enter a city, address, or ZIP code and select a suggestion, or choose **Use my location**. Review the status message, alert details, and any affected alert areas mapped by NWS.
5. Try Light, Dark, and Red display modes. The selected mode is shared between pages. In Red mode, opening NASA FIRMS or an official alert shows a brightness warning. **Continue and adjust my eyes** fades Trail Advisor to Light mode over 2.5 seconds, then opens the destination in a new tab.

## Data and known limits

- Weather and fire-weather alerts come from the National Weather Service and cover the United States and territories. Alert boundaries appear only when NWS provides geometry; this is not a fire-perimeter or evacuation map.
- The alert signal uses only the severity of returned NWS alerts (Extreme, Severe, Moderate, Minor, or unspecified). It is not a probability, route assessment, or guarantee of safety. A zero means no active NWS alerts were returned for the point when checked.
- The explorer uses OpenFreeMap's Liberty vector style through MapLibre GL JS. Map labels and administrative boundaries appear according to the selected style's zoom levels. Clicking the map asks Photon, a public OpenStreetMap-based geocoder, for the nearest named place; exact labeling depends on available map data.
- Location autocomplete and map selection use Photon. Search text is sent to Photon while typing on the advisories page. Its demo server asks for reasonable use and has no availability guarantee.
- Public map and geocoder services are suitable for a low-traffic prototype, not a production availability guarantee. OpenStreetMap attribution is included.
- The site needs an internet connection for MapLibre, map tiles, geocoding, fonts, and NWS data. Public services can be unavailable or change their terms.
- A diagnostics panel on the advisories page can copy service response codes and error details from the current session. It does not record location coordinates or search text.

## Commercial use

OpenFreeMap states that its public map service is free for commercial use and has no request or view limits, but provides no SLA. Check the [OpenFreeMap quick start](https://openfreemap.org/quick_start/) and current service terms before launch. OpenStreetMap data is licensed under the ODbL and requires attribution. Photon is a public demo geocoder with usage limits; choose a geocoder with terms and service commitments that fit a commercial product before launch.

MapLibre GL JS is distributed under the BSD 3-Clause license. NWS API data is publicly available, but this prototype is not an official emergency alert channel. Follow local emergency officials and land-manager guidance.
