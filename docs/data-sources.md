# Data sources, coverage, and reuse

This demo uses public services directly from the browser. Public availability does not guarantee uptime, current data, permission to bulk-download, or production capacity. Recheck each provider's live terms before a public/commercial launch.

| Data | Provider | What Trail Advisor uses | Coverage / freshness caveat |
| --- | --- | --- | --- |
| Trail geometry and attributes | [USGS National Digital Trails / USGSTrails](https://www.usgs.gov/national-digital-trails/qas-about-usgs-trail-data) | Name search, nearby mapped sections, section length, type, maintainer/source agency, activities, and designation when present. | USGS aggregates public official trail data and says incoming data is quality-reviewed. Its coverage includes federal agencies, 36 states, four trail organizations, and some local trails; it is not exhaustive. USGS reports non-federal data may refresh every 3–5 years. The ArcGIS layer allows at most 2,000 records in a query; nearby display is limited to the nearest eight among records returned by the service. |
| Trail service | [USGS ArcGIS layer metadata](https://partnerships.nationalmap.gov/arcgis/rest/services/USGSTrails/MapServer/0) | Query endpoint for the nationwide trail layer. Result metadata includes `sourceoriginator`, `primarytrailmaintainer`, and source dates where available. | Public USGS service with no availability guarantee from this app. Source agency is displayed when provided, but visitors should confirm closures, access, and season status with that maintainer. |
| Recreation-site amenities | [USDA Forest Service Recreation Sites](https://apps.fs.usda.gov/arcx/rest/services/EDW/EDW_InfraRecreationSites_01/MapServer/0) | Recorded Forest Service sites and available restroom, water, accessibility, seasonal, and current-condition fields. | Only participating/recorded Forest Service site data; missing records do not establish that a facility is absent. Information can be outdated. |
| Weather alerts and forecast | [National Weather Service API](https://www.weather.gov/documentation/services-web-api) | Active alerts, point forecast, and latest available nearby station observation. | U.S. NWS coverage; station observations can be delayed or geographically distant from a remote trail. Not an emergency alert channel. |
| Place search / reverse geocoding | [Photon](https://photon.komoot.io/) | City autocomplete and selected-pin place labels. Photon is based on OpenStreetMap data. | Public demo endpoint asks for reasonable use and offers no uptime guarantee. Search text and selected coordinates are sent when those lookups are requested. |
| Street basemap | [OpenFreeMap](https://openfreemap.org/quick_start/) and OpenStreetMap data | Default vector basemap and place labels. | OpenFreeMap states its public service is free for commercial use; check current terms and capacity. OSM data attribution is required and the data is under ODbL. |
| Topographic / aerial map tiles | USGS The National Map | U.S. topo and aerial imagery styles. | Public domain data generally; coverage, age, resolution, and credits vary by region. The imagery is not live. |
| Map renderer | [MapLibre GL JS](https://github.com/maplibre/maplibre-gl-js) | Interactive vector map. | BSD 3-Clause license. |

## Important interpretation

“Quality-reviewed” describes the USGS aggregation process. It does not mean a trail is currently open, safe, maintained, accessible, or verified in the field today. Trail line length is the length of a source segment, not necessarily the end-to-end distance for a named route. Source update intervals vary. Do not infer that a blank map means no trail exists.

The nearby trail radius is a maximum search distance (5–1,000 miles). Nearby results display up to eight closest mapped sections; this is a discovery aid, not an exhaustive trail inventory. The USGS ArcGIS query caps each response at 2,000 records, so a broad-radius result can omit records beyond that service limit. Search by trail name or open the USGS Trails Explorer for source inspection.

This table is a product disclosure, not legal advice or a substitute for reviewing the current provider license/terms for a particular deployment.
