# la-wildfire

# 🔥 LA Wildfire Predictive Intelligence Dashboard

A fully interactive, self-contained web dashboard that takes a **predictive and tech-forward approach** to wildfire risk in Los Angeles County. Instead of showing damage after the fact, this dashboard focuses on **what could happen next** — where embers will travel, which neighborhoods face the highest ignition risk, which power lines are most likely to start a fire, and where air quality is heading.

Built with plain HTML, CSS, and SVG — no frameworks, no installs, no API keys required. Open the file in any browser and it works instantly.

**[▶ View Live Dashboard](https://radhikamehra-portfolio.github.io/la-wildfire/)**

---

## 📋 What This Dashboard Shows

This dashboard is **not** about fire damage or evacuation maps. It is about **predicting and preventing** the next fire before it starts. It pulls together five predictive data perspectives:

| Module | What it answers |
|---|---|
| 💨 Ember Cast Simulator | Where will airborne embers land and start new fires? |
| 🗺️ Ignition Risk Map | Which neighborhoods are most likely to ignite right now? |
| 🌿 Fuel Load Monitor | Where has dry brush built up to dangerous levels? |
| ⚡ Utility Infrastructure Risk | Which power lines are most likely to cause ignition? |
| 🌫️ Air Quality Corridors | Where is smoke spreading and who needs to stay indoors? |

---

## 🗺️ How to Navigate the Dashboard

### The Sidebar (Left Panel)
The left sidebar has three sections:

1. **Predictive Tools** — Click any of the 5 module names to switch between pages
2. **Current Risk Levels** — Always-visible bar chart showing live risk scores for 7 LA neighborhoods
3. **Active Alerts** — Current Red Flag Warnings and watches from the National Weather Service

### The Alert Bar (Top)
The colored bar just below the header shows the most urgent active alerts — Red Flag Warnings, Ember Transport Watches, and PSPS (power shutoff) decisions.

### Each Module Page
Every page follows the same layout:
- **Title + subtitle** — what this module tracks
- **4 metric cards** — the key numbers at a glance (color-coded: red = danger, amber = warning, blue = informational, green = ok)
- **Main visualization** — an animated SVG map or data chart
- **Supporting panel** — a timeline, table, or detail card on the right

---

## 💨 Module 1: Ember Cast Simulator

**What it shows:** During a wildfire, burning embers (called *firebrands*) get lofted into the air and carried by wind — sometimes over a mile — before landing and starting entirely new fires called *spot fires*. This is how wildfires jump highways and leap from canyon to canyon.

**The map:** The animated map shows Topanga Canyon as the fire origin point (orange pulsing dot). The red and orange ellipses spreading downwind show where embers are most likely to land. The floating orange dots are animated ember particles showing the direction of travel.

**What the numbers mean:**
- **Wind Speed (58 mph)** — The current sustained Santa Ana wind speed. Above 35 mph, spot fire risk becomes very high
- **Ember Travel Distance (1.8 mi)** — The maximum distance an ember can travel under current conditions before landing
- **Relative Humidity (6%)** — How dry the air is. Below 15% RH, vegetation ignites almost instantly when an ember lands
- **Spot Fire Probability (84%)** — The likelihood that a landed ember actually starts a new fire given current fuel and humidity conditions

**The timeline:** Shows projected times for ember-started fires to appear at specific locations if conditions hold.

---

## 🗺️ Module 2: Ignition Risk Map

**What it shows:** A neighborhood-by-neighborhood risk score (0–100) combining five real-time inputs: wind speed, relative humidity, air temperature, satellite vegetation dryness (NDVI), and historical fire density.

**The map:** Each colored ellipse represents a neighborhood. The size of the ellipse reflects the geographic area; the color reflects the risk score. Pulsing dots mark neighborhoods where risk is actively increasing.

**Color coding:**
- 🔴 **Red (75–100)** — Critical. Conditions similar to those before the Woolsey and Thomas fires
- 🟡 **Amber (50–74)** — High. Active monitoring required
- 🔵 **Blue (25–49)** — Moderate. Elevated but not immediately dangerous
- 🟢 **Green (0–24)** — Low. Near-normal conditions

**The table:** Shows the top ignition sources by type (power lines, lightning, vehicle sparks, etc.) with count and probability data from the last 30 days.

**Key term — NDVI:** The Normalized Difference Vegetation Index is a satellite measurement of how green or dry vegetation is. A low NDVI means dry, brown plants — which are far more flammable.

---

## 🌿 Module 3: Fuel Load Monitor

**What it shows:** How much dry, burnable vegetation has accumulated in each LA corridor, measured via NASA Landsat-9 and MODIS satellite imagery updated every 1–2 days. Think of fuel load as how much kindling is stacked up waiting for a spark.

**The gauges:** Each horizontal bar shows what percentage of that corridor's vegetation is critically dry and burnable. 90%+ is the danger threshold — at that point, a single spark from a power line, a vehicle, or lightning can ignite a fire that moves faster than people can evacuate.

**Why are burns blocked?** The prescribed burn schedule shows that most planned burns — which would safely remove this fuel — are blocked by the same dangerous weather conditions that make fires so risky. This is a known paradox in fire management.

**Key terms:**
- **Chaparral** — Dense native shrubland unique to Southern California. It is highly adapted to fire and extremely flammable when dry
- **Prescribed Burn** — A controlled fire intentionally set by Cal Fire or the US Forest Service to safely remove excess fuel before wildfire season
- **MODIS** — A NASA satellite instrument that passes over Los Angeles twice daily, measuring vegetation health and surface temperature

---

## ⚡ Module 4: Utility Infrastructure Risk

**What it shows:** Power lines and electrical equipment are the number one cause of California wildfires — responsible for the 2018 Camp Fire (85 deaths, the deadliest in state history) and many others. This module tracks SCE (Southern California Edison) and LADWP assets near high-risk terrain.

**The asset list:** Each row is a specific piece of infrastructure ranked by ignition risk. The colored pill on the right (CRITICAL / HIGH / MEDIUM / LOW) reflects a combination of proximity to dry vegetation, current wind speed, and recent inspection status.

**PSPS tracker:** PSPS stands for *Public Safety Power Shutoff* — when a utility company proactively cuts electricity to prevent its lines from starting fires during extreme wind events. This is a major decision because it leaves thousands of customers without power, including people who depend on medical equipment.

**Key terms:**
- **Conductor Galloping** — When high winds cause power lines to swing violently. If two lines touch, the resulting electrical arc can ignite fires directly below
- **Vegetation Contact** — When tree branches or shrubs grow into live power lines. The primary cause of ignition in California
- **kV (kilovolt)** — The voltage of a transmission line. Higher voltage lines carry more energy and create larger arcs if they fail

---

## 🌫️ Module 5: Air Quality Corridors

**What it shows:** Wildfire smoke is not just unpleasant — it is a serious health emergency. This module tracks the Air Quality Index (AQI) by zip code and models where smoke plumes are moving using NOAA's HYSPLIT atmospheric transport model.

**The AQI grid:** Each colored card shows the current AQI for that zip code. The color reflects the health risk level.

**AQI scale:**
| AQI | Category | What it means |
|---|---|---|
| 0–50 | Good | Air quality is satisfactory |
| 51–100 | Moderate | Unusually sensitive people should limit outdoor exertion |
| 101–150 | Unhealthy for Sensitive Groups | Children, elderly, asthma patients should stay indoors |
| 151–200 | Unhealthy | Everyone should avoid prolonged outdoor activity |
| 201–300 | Very Unhealthy | Everyone should avoid all outdoor activity |
| 301–500 | Hazardous | Emergency conditions — remain indoors, seal windows |

**Key terms:**
- **PM2.5** — Fine particulate matter smaller than 2.5 micrometers — about 1/30th the width of a human hair. These particles penetrate deep into the lungs and can enter the bloodstream, causing heart and lung damage
- **HYSPLIT** — NOAA's Hybrid Single-Particle Lagrangian Integrated Trajectory model, which predicts where smoke travels based on atmospheric wind patterns
- **SCAQMD** — South Coast Air Quality Management District, the agency that operates the network of air quality sensors across Los Angeles County

---

## 🛠️ Technical Stack

| Component | Technology |
|---|---|
| Framework | None — pure HTML/CSS/SVG |
| Maps | Hand-crafted animated SVG |
| Animations | CSS keyframe animations |
| Navigation | Vanilla JavaScript (< 20 lines) |
| Dependencies | Zero — fully self-contained |
| File size | ~60KB single file |

---

## 📡 Data Sources (Simulated)

This dashboard uses representative/simulated data based on real LA County conditions. In a production version, these would connect to live APIs:

| Data | Real Source |
|---|---|
| Fire risk scores | NASA FIRMS + NOAA Weather API |
| Vegetation / fuel load | NASA Landsat-9, MODIS NDVI |
| Wind speed & humidity | NOAA National Weather Service |
| Air quality (AQI) | SCAQMD sensor network + AirNow API |
| Power infrastructure | SCE and LADWP open data portals |
| Fire perimeters | Cal Fire incident data |
| Smoke plume modeling | NOAA HYSPLIT model |

---

## 📁 File Structure

```
la-wildfire-dashboard/
└── index.html      ← The entire dashboard (single file)
```

---

## 🚀 How to Run Locally

No install needed. Just:

1. Download `index.html`
2. Double-click it
3. It opens in your browser

---

## 📄 License

Open source — free to use, adapt, and share.

---


