# Flight Network Routing Optimisation

Finding the best path for data to travel between aircraft over the North Atlantic and three ground stations, using real flight position data and graph optimisation.

**Stack:** Python (pandas, NumPy, NetworkX) · Dijkstra's algorithm · Basemap / Plotly for route maps

---

## Problem
Aircraft over the North Atlantic can relay data packets to each other until a packet reaches a ground station. Each aircraft-to-aircraft link has a distance, a latency and a transmission rate. The task: choose routes that make this network perform best.

Ground stations: **London Heathrow (LHR)**, **Newark (EWR)**, **Narsarsuaq, Greenland (UAK)**

Two objectives were solved separately:
1. **Minimise end-to-end latency** from every aircraft to the ground stations
2. **Maximise end-to-end transmission rate**, subject to the given link conditions

## Approach
| Step | What was done |
|---|---|
| 1. Data | Loaded a snapshot of real North Atlantic flight positions (flight number, altitude, latitude, longitude; 29 June 2018) and added ground-station coordinates |
| 2. Distances | Calculated great-circle distances between every aircraft pair and every aircraft-ground station pair |
| 3. Link rates | Converted distance to transmission rate; removed links out of range (rate = 0), self-links and duplicates |
| 4. Network | Built a weighted graph with NetworkX, aircraft and ground stations as nodes |
| 5. Optimisation | Applied Dijkstra's shortest-path algorithm per objective |
| 6. Visualisation | Plotted aircraft, ground stations and chosen routes on a map |

## Why Dijkstra
Both problems are single-objective, the graph is small to medium in size, and all edge weights are non-negative, which is the case Dijkstra's algorithm solves optimally and efficiently.

## Results
- **Latency:** found the minimum-latency route from every aircraft to all **3** ground stations
- **Transmission rate:** found maximum-rate routes when using **2** ground stations; with all 3, the solver did not reach a valid solution under the given conditions

## Relevance to Planning and Operations
The same method underlies network and capacity decisions in logistics: choosing routes, assigning flows to nodes, and trading off speed against capacity under constraints.

## Files
| File | Purpose |
|---|---|
| `SEO.ipynb` | Full analysis: data prep, distance and rate calculations, graph build, Dijkstra routing, maps |

## Context
MSc Data Science & AI coursework, Bournemouth University (2023).
