# 🔥 LA Wildfire Predictive Intelligence — Implementation Plan

> Version 1.0 · Los Angeles County · Predictive & Tech-Forward Dashboard

---

## Project Overview

This dashboard takes a **prevention-first** approach to wildfire risk in LA County — predicting where fires are likely to start and spread, rather than mapping damage after the fact. The current version is a fully functional static prototype. This plan outlines how to evolve it into a live, data-connected production system.

> **Current state:** Working HTML/SVG prototype with simulated data — fully shareable, zero dependencies, runs in any browser.
> **Next milestone:** Connect live data APIs to replace simulated values with real-time feeds.

---

## Implementation Phases

### ✅ Phase 1 — Prototype & Publish (Weeks 1–2) — COMPLETE
- Build HTML/SVG dashboard with 5 predictive modules
- Animated SVG maps, metric cards, sidebar navigation
- Publish to GitHub Pages
- Write README and implementation documentation

### 🔵 Phase 2 — Live Data Integration (Weeks 3–6) — NEXT
- Register and connect NOAA weather API (wind speed, humidity)
- Connect AirNow AQI API (live air quality by zip code)
- Connect NASA FIRMS active fire hotspot feed
- Auto-refresh data every 15 minutes
- Replace all simulated values with real-time data

### 🟠 Phase 3 — Interactive Maps (Weeks 7–10) — PLANNED
- Migrate SVG maps to Leaflet.js with real OpenStreetMap geography
- Add real LA County neighborhood boundary polygons
- Clickable markers with data popups
- Layer toggles (risk zones, fuel load, AQI, utility assets)
- Full mobile-responsive layout

### 🟣 Phase 4 — Alerts & Scale (Weeks 11–16) — FUTURE
- Email / SMS alert system when risk thresholds are crossed
- User location detection for personalized risk scores
- Historical trend analysis and fire season comparisons
- Cal OES / LAFD data integration
- Embeddable widget for agency portals

---

## Delivery Timeline

| Week | Milestone | Status |
|------|-----------|--------|
| 1–2 | Prototype complete & published to GitHub Pages | ✅ Done |
| 3 | Register API keys (NOAA, AirNow, NASA FIRMS) | ⏳ Next |
| 4 | Connect NOAA wind + humidity to Ember Cast module | ⏳ Next |
| 5 | Connect AirNow AQI to Air Quality module | ⏳ Next |
| 6 | Connect NASA FIRMS fire hotspots + auto-refresh loop | ⏳ Next |
| 7–8 | Migrate SVG maps to Leaflet.js | 📋 Planned |
| 9–10 | Mobile responsive layout + UI polish | 📋 Planned |
| 11–13 | Email / SMS alert system | 🔮 Future |
| 14–16 | Agency integration + embeddable widget | 🔮 Future |

---

## Live Data Sources & APIs

All primary data sources are **free and publicly available**. No paid subscriptions required for Phases 1–3.

| Module | Data Source | API / Feed | Cost | Refresh Rate |
|--------|------------|------------|------|-------------|
| Ember Cast | NOAA National Weather Service | api.weather.gov | Free | Hourly |
| Ember Cast | NASA FIRMS | firms.modaps.eosdis.nasa.gov | Free | 3 hours |
| Ignition Risk | NASA Landsat-9 / MODIS | NASA EarthData API (NDVI) | Free | Daily |
| Ignition Risk | Cal Fire Incidents | incidents.fire.ca.gov | Free | 15 min |
| Fuel Load | NASA MODIS | NDVI + fuel moisture index | Free | Daily |
| Utility Risk | SCE Open Data | sce.com/developer (PSPS) | Free | Real-time |
| Utility Risk | LADWP | ladwp.com/open-data | Free | Real-time |
| Air Quality | SCAQMD / AirNow | airnowapi.org | Free | Hourly |
| Air Quality | NOAA HYSPLIT | ready.noaa.gov (plumes) | Free | 6 hours |
| All Maps | OpenStreetMap / Leaflet | tile.openstreetmap.org | Free | Static |
| Alerts | NWS Red Flag Warnings | api.weather.gov/alerts | Free | 15 min |

### API Registration Links
- **AirNow API** — https://docs.airnowapi.org/
- **NASA EarthData** — https://urs.earthdata.nasa.gov/
- **NOAA Weather** — No registration required: https://api.weather.gov
- **NASA FIRMS** — https://firms.modaps.eosdis.nasa.gov/api/
- **Cal Fire Incidents** — No registration: https://incidents.fire.ca.gov

---

## Module-by-Module API Plan

### 💨 Ember Cast Simulator
- **APIs:** NOAA wind speed & direction, relative humidity · NASA FIRMS fire hotspots
- **Logic:** Compute ember travel radius = function of (wind_speed, humidity). Render dispersion ellipse on map centered on the nearest active FIRMS fire hotspot.

### 🗺️ Ignition Risk Map
- **APIs:** NOAA weather per lat/lng · NASA NDVI · Cal Fire historical incidents
- **Logic:** Weighted risk score — Wind 30% + Humidity 25% + NDVI dryness 25% + Historical fire density 20%

### 🌿 Fuel Load Monitor
- **APIs:** NASA EarthData MODIS NDVI · USFS fuel moisture data
- **Logic:** Invert NDVI value to get dryness index. Normalize 0–100 as fuel load %. Trigger alert when corridor exceeds user-set threshold.

### ⚡ Utility Infrastructure Risk
- **APIs:** SCE PSPS status feed · LADWP outage API · NOAA wind speed at asset location
- **Logic:** Cross-reference each asset's lat/lng with live wind speed. Elevate risk level when wind exceeds 35 mph at that location.

### 🌫️ Air Quality Corridors
- **APIs:** AirNow AQI by zip code · NOAA HYSPLIT smoke trajectory model
- **Logic:** Pull current AQI per zip. Overlay HYSPLIT 6h and 24h smoke plume polygons as translucent map layers.

### 🚨 Alert System (Phase 4)
- **APIs:** NWS alerts feed · Twilio SMS · SendGrid email
- **Logic:** Monitor risk scores every 15 minutes. Trigger notification when any watched zip code crosses the configured threshold.

---

## Recommended Technology Stack

| Layer | Technology | Reason |
|-------|-----------|--------|
| Frontend | HTML + CSS + JavaScript | No build step, runs anywhere, easy to edit |
| Maps (Phase 3) | Leaflet.js + OpenStreetMap | Free, open-source, excellent LA coverage |
| Data fetching | `fetch()` with `setInterval` | No backend needed for read-only public APIs |
| Hosting (current) | GitHub Pages | Free, automatic on every git push |
| Hosting (Phase 4) | Netlify or Vercel | Free tier, serverless functions for API proxying |
| API key security | Netlify/Vercel env variables | Keys never exposed in client-side code |
| Alerts (Phase 4) | Twilio + SendGrid | Both have free developer tiers |
| Analytics | Plausible or Umami | Privacy-friendly, free self-hosted |

---

## Priority Matrix

### 🟢 Quick Wins — High impact, low effort (do first)
- Connect AirNow AQI API to Air Quality module
- Connect NOAA wind and humidity to Ember Cast module
- Pull NWS Red Flag Warning alerts live
- Show Cal Fire active incident count
- Display data freshness timestamps

### 🔵 Strategic Investments — High impact, higher effort (plan carefully)
- Leaflet.js map migration with real neighborhood boundaries
- NDVI fuel load data pipeline
- Ember cast physics model (wind × humidity × terrain)
- Composite risk score algorithm with weighting
- SMS / email threshold alert system

### 🟡 Watch & Evaluate — Lower impact, lower effort (do if time permits)
- Dark / light mode toggle
- Print-friendly PDF export
- Language localization (Spanish priority for LA)
- Keyboard navigation / accessibility pass

### ⬜ Defer — Lower impact, higher effort (not now)
- Native iOS / Android mobile app
- Custom ML fire prediction model
- Real-time multi-user collaboration features
- Full user accounts and saved preferences

---

## Cost Estimate

| Item | Phase | Est. Monthly Cost | Notes |
|------|-------|------------------|-------|
| GitHub Pages hosting | 1–2 | $0 | Free for public repos |
| All data APIs (NOAA, NASA, AirNow, Cal Fire) | 2 | $0 | All free public APIs |
| Netlify / Vercel hosting | 3–4 | $0–$19/mo | Free tier covers most usage |
| Twilio SMS alerts | 4 | ~$8/mo | At ~1,000 alerts/day @ $0.0079/SMS |
| SendGrid email | 4 | $0 | Free up to 100 emails/day |
| Domain name (optional) | 3 | ~$1/mo | e.g. lawildfiredash.org (~$12/year) |

> **Phases 1–3 can be completed for under $50 total in infrastructure costs.** The primary investment is developer time: approximately 20–30 hours for Phase 2, 30–40 hours for Phase 3.

---

## Risks & Mitigations

| Risk | Likelihood | Mitigation |
|------|-----------|-----------|
| API rate limits exceeded during active fire events | Medium | Cache responses locally; use staggered polling; fallback to last known good data |
| NOAA / AirNow API downtime during emergencies | Low | Show last-known data with timestamp; display "data unavailable" banner gracefully |
| Simulated data mistaken for real data | Medium | Add prominent "SIMULATED DATA" banner on prototype; remove only when all feeds are live |
| CORS restrictions on direct API calls from browser | High | Proxy API calls through a Netlify serverless function to bypass browser CORS |
| SCE / LADWP data feeds change format or URL | Low | Build a data adapter layer; monitor feed schemas quarterly |
| Mobile layout breaks on small screens | Medium | Phase 3 includes full responsive redesign; test on iPhone SE (375px) as minimum |

---

## Success Metrics

| Metric | Phase 1 Target | Phase 3 Target |
|--------|---------------|----------------|
| Dashboard loads without errors | ✅ Any browser | ✅ Any browser + mobile |
| Data freshness | Static (simulated) | ≤ 15 minutes old |
| Page load time | < 1 second | < 3 seconds (with Leaflet) |
| Modules with live data | 0 of 5 | 5 of 5 |
| Mobile usability | Partial | Fully responsive |
| Alert accuracy (Phase 4) | N/A | ≥ 90% vs NWS ground truth |

---

## Immediate Next Steps

1. **Publish to GitHub Pages** — Upload `index.html` + `README.md` + `IMPLEMENTATION.md` → enable Pages → share the live link
2. **Register for free API keys** — AirNow (airnowapi.org) · NASA EarthData (urs.earthdata.nasa.gov) · NOAA (no key needed)
3. **Connect AirNow AQI first** — Replace static AQI numbers with live zip-code data (~2 hours of work, biggest visible impact)
4. **Connect NOAA wind + humidity** — Replace Ember Cast metric cards with live NWS point forecast data for LA County
5. **Plan Leaflet.js decision** — Decide whether to keep SVG maps for simplicity or migrate to real geography based on target audience needs

---

## File Structure

```
la-wildfire-dashboard/
├── index.html            ← The complete dashboard (single file)
├── README.md             ← Project overview & navigation guide
└── IMPLEMENTATION.md     ← This file — full implementation plan
```

---

## How to Run Locally

No install needed:

1. Download or clone this repository
2. Open `index.html` in any browser
3. The full dashboard loads instantly — no server required

```bash
git clone https://github.com/YOUR-USERNAME/la-wildfire-dashboard.git
cd la-wildfire-dashboard
open index.html
```

---

*LA Wildfire Predictive Intelligence · Implementation Plan v1.0 · Made with IBM Bob*
