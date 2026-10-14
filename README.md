# FloodSafe Sindh

**Flood Risk and Evacuation Planner** | OpenHack'26 | Category: Climate & Disaster Resilience (CL-01)

**Live demo:** https://floodsafe-sindh.babbsbs126.workers.dev
**Source:** https://github.com/Real-tech-ui/floodsafe-Sindh

> **Prototype notice:** This project uses simulated sample data. Risk scores and routes are model estimates, not official warnings or emergency instructions.

## Problem

Communities along the Indus in Sindh were hit hard by the 2022 floods. Residents often lack simple, local information about which areas are at risk, where the nearest shelter is, and which route to take when a road is cut off.

## Solution

FloodSafe is a map-based decision-support tool that shows flood risk by neighbourhood, lists nearby shelters, and recommends the safest evacuation route, rerouting automatically when roads are blocked. Safety messages are available in English, Urdu and Sindhi.

## Features (CL-01 MVP)

- Interactive map of the demo area (Sukkur) with colour-coded risk zones
- Transparent, documented risk scoring (see below), with a per-zone breakdown on click
- Rainfall slider to simulate different conditions; pre-filled from a live forecast when available
- Shelter locations and the safest route to the nearest shelter
- Click any road to block or unblock it; the route recalculates instantly
- Safety messages in English, Urdu and Sindhi that change with the risk level

## How the risk score works

```
risk = 0.40 × proximity + 0.25 × low_elevation + 0.35 × rainfall

proximity     = 1 − min(distance_to_river_km / 3, 1)
low_elevation = 1 − min(max(elevation_m − 55, 0) / 15, 1)
rainfall      = min(rain_mm_24h / 150, 1)

High: risk ≥ 0.65   Medium: risk ≥ 0.35   Low: otherwise
```

The weights and thresholds are documented assumptions for demonstration. They are not calibrated hydrological values.

## Evacuation routing

Roads are modelled as a small graph. Blocked roads are removed, and Dijkstra's shortest-path algorithm finds the nearest reachable shelter by road distance. If every path is blocked, the app says so instead of guessing.

## Tech

HTML, CSS and JavaScript in a single file, [Leaflet](https://leafletjs.com) with OpenStreetMap tiles, and the Open-Meteo forecast API for optional live rainfall. No build step and no API keys. Deployed on Cloudflare Workers.

## Run locally

Open `index.html` in a browser (or use the VS Code Live Server extension). An internet connection is needed for map tiles and the optional forecast.

## Data, limits and safety

- Zones, shelters, elevations and road links are **sample data** with approximate coordinates.
- Risk scoring is a transparent rule-based model, not a flood forecast.
- Urdu and Sindhi messages need review by native speakers before real use.
- Not a substitute for official warnings from PDMA, NDMA or local authorities.

## Roadmap

- Replace sample data with verified PDMA/NDMA shelter and flood-zone data
- Integrate official flood-warning feeds and river-discharge data
- Add shelter capacity and live occupancy
- Let residents report blocked roads
- Native-speaker review of all translations

## Team

Ali Huzaifa, BS IT student. Built with AI assistance (Claude, by Anthropic) for code and documentation.
