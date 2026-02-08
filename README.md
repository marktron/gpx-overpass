# GPX → Overpass Buffer

A browser-based tool that generates buffered polygon queries for [Overpass Turbo](https://overpass-turbo.eu) from GPX routes. Upload a cycling, hiking, or running route and find nearby amenities within a configurable corridor.

**[Try it live →](https://yourusername.github.io/your-repo-name/)**

## How it works

1. **Upload a GPX file** — drag-and-drop or file picker. Supports both tracks (`trkpt`) and routes (`rtept`).
2. **Adjust the buffer** — set how far from the route to search (100m–5km, default 800m).
3. **Pick filters** — select one or more amenity types (water, toilets, food, bike shops, shelters, etc.) or write a custom Overpass tag filter.
4. **Copy or run the query** — paste into Overpass Turbo, or open it directly with one click.

The tool simplifies the route using the Douglas-Peucker algorithm, then offsets each point perpendicular to the direction of travel to create a buffer polygon with semicircular end caps. Filters sharing the same OSM tag key are merged into a single regex alternation to minimize query size.

## Features

- **Adjustable buffer distance** with real-time SVG preview
- **Multi-select filters** that merge by tag key for efficient queries
- **Polygon detail control** to balance accuracy vs. query length
- **Copy to clipboard** and **Open in Overpass Turbo** buttons
- **View route on map** via geojson.io (route + buffer polygon with styled GeoJSON)
- Zero dependencies — runs entirely in the browser

## Usage

Open `index.html` in any modern browser. No build step, no server, no install.

To host on GitHub Pages: push this repo, go to Settings → Pages, select your branch, and your site will be live.

## Query example

Selecting "Drinking Water" and "Toilets" with an 800m buffer produces:

```
[out:json][timeout:90];
(
  nwr["amenity"~"drinking_water|toilets"](poly:"43.44767 -79.68249 43.44541 ...");
);
out body;
>;
out skel qt;
```

## License

MIT
