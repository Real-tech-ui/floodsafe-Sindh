# FloodSafe Sindh

**Flood Risk and Evacuation Planner** | OpenHack'26 | Category: Climate & Disaster Resilience

**Live demo:** https://floodsafe-sindh.babbsbs126.workers.dev
**Source code:** https://github.com/Real-tech-ui/floodsafe-Sindh

> **Prototype notice:** This project uses simulated sample data. Risk scores and routes are model estimates, not official warnings or emergency instructions.

## Problem Statement

**CL-01: Flood Risk and Evacuation Planner.** Communities near rivers and flood-prone settlements may lack accessible information about local hazards, nearby shelters and possible evacuation routes. Sindh was among the worst-hit regions in the 2022 floods.

## Our Solution

A map-based decision-support tool that shows flood risk by neighbourhood, lists nearby shelters, and recommends the safest evacuation route. When a road is blocked, the route recalculates automatically. Safety messages are available in English, Urdu and Sindhi.

## Key Features

- Interactive map of the demo area (Sukkur) with colour-coded risk zones
- Transparent risk scoring with a per-zone breakdown shown on click
- Rainfall slider to simulate conditions, pre-filled from a live forecast when available
- Shelter locations and the safest route to the nearest reachable shelter
- Click any road to block or unblock it; the route updates instantly
- Safety messages in English, Urdu and Sindhi that change with the risk level

## How the Risk Score Works

```
risk = 0.40 x proximity + 0.25 x low_elevation + 0.35 x rainfall

proximity     = 1 - min(distance_to_river_km / 3, 1)
low_elevation = 1 - min(max(elevation_m - 55, 0) / 15, 1)
rainfall      = min(rain_mm_24h / 150, 1)

High: risk >= 0.65   Medium: risk >= 0.35   Low: otherwise
```

Weights and thresholds are documented assumptions for demonstration, not calibrated hydrological values.

**Routing:** roads are a small graph; blocked roads are removed and Dijkstra's shortest-path algorithm finds the nearest reachable shelter by road distance. If every path is blocked, the app says so.

## Technologies

HTML, CSS and JavaScript (single file, no build step), Leaflet for the map, OpenStreetMap tiles, Open-Meteo forecast API for optional live rainfall, deployed on Cloudflare Workers, source on GitHub.

## Challenges

- **Data availability:** verified shelter and flood-zone data was not available in machine-readable form within 24 hours, so we used clearly labelled sample data.
- **Routing around blocked roads:** we modelled a simplified road graph so rerouting could be demonstrated and explained reliably.
- **Multilingual safety messages:** Urdu and Sindhi text needs review by native speakers before real-world use.

## AI & Open-Source Disclosure

```
AI Tools / Models:
- Claude (Anthropic): used to generate and refine the application code and documentation.
  The team tested, deployed and can explain the implementation.

Open-Source Technologies and External Services:
- Leaflet (map library)
- OpenStreetMap (map tiles and data)
- Open-Meteo (weather forecast API)
- Cloudflare Workers (hosting), GitHub (source hosting)
```

## Data, Limits and Safety

- Zones, shelters, elevations and road links are **sample data** with approximate coordinates.
- Risk scoring is a transparent rule-based model, not a flood forecast.
- Not a substitute for official warnings from PDMA, NDMA or local authorities.

## Roadmap

Verified PDMA/NDMA shelter data, official flood-warning feeds, shelter capacity, community reporting of blocked roads, native-speaker review of translations.

   **Team name:** TEAM ZEROX

   | Member | Contribution |
   | ------ | ------------ |
   | Ali Huzaifa | Chose the problem, directed the project, tested and deployed it |