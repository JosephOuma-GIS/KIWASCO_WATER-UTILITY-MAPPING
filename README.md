#  Kisumu County Water Utility — CIS Data Gap Analysis

> **Phase 1 Findings & Phase 2 Priority Zone Documentation**  
> Spatial analysis of uncollected Customer Information Survey (CIS) records across Kisumu County's water distribution network.

---

##  Project Overview

This repository hosts the spatial datasets and map outputs produced during the **Phase 1 Customer Information Survey (CIS)** for Kisumu County's water utility mapping project, covering both **Non-Revenue Water (NRW)** and **Revenue Water** service areas.

Using GIS-based gap analysis, the project team has identified and mapped every building within the pipeline service zone for which a CIS record was **not collected** during Phase 1 fieldwork. These uncollected locations form the basis of the **Phase 2 priority revisit zones**.

---

## Objective

To determine the spatial data gap between:

- **Buildings within the serviceable pipeline zone** — structures eligible for a water connection based on proximity to the distribution network
- **Phase 1 CIS collected points** — survey records actually gathered in the field

The difference between these two datasets reveals exactly **where, how many, and in which priority order** uncollected CIS records must be obtained in Phase 2 — without revisiting already-surveyed locations.

---

## Repository Contents

| File / Folder | Description |
|---|---|
| `CIS_Gap_Buildings.geojson` | All building footprints within the service zone with no Phase 1 CIS match — the primary gap dataset |
| `CIS_Collected_Phase1.geojson` | Phase 1 collected CIS points for reference overlay |
| `Pipeline_Service_Buffer.geojson` | 50-metre service influence zone derived from the pipeline network |
| `Ward_Priority_Zones.geojson` | Ward-level boundaries with gap count and priority ranking attributes |
| `maps/` | Exported PNG maps from ArcGIS Pro 3.4 |
| `README.md` | This document |

---

## 🔬 Methodology Summary

All analysis was conducted in **ArcGIS Pro 3.4** using the following workflow:

1. **Coordinate Reference System** — All layers projected to `Arc 1960 / UTM Zone 36S (EPSG: 21036)` to ensure metre-based accuracy
2. **Service Zone Definition** — A 50-metre buffer applied around the pipeline network to define the maximum serviceable reach
3. **Building Selection** — `Select by Location` used to extract all building footprints intersecting the service zone (`Buildings_In_Service_Zone`)
4. **Spatial Join** — One-to-one spatial join matching Phase 1 CIS points to building footprints (Intersect, 10m search radius)
5. **Gap Classification** — `CIS_Status` field calculated:
   - `Join_Count > 0` → **Collected**
   - `Join_Count = 0` → **GAP — Not Collected**
6. **Priority Ranking** — Gap buildings aggregated by ward using `Summarize Within`; zones ranked HIGH / MEDIUM by gap count

---

##  Key Findings

| Zone | Predicted GAP Count | Priority Rank |
|---|---|---|
| Manyatta | 11,300 | 🔴 HIGH |
| Riat | 4,746 | 🔴 HIGH |
| Central Business District | 3,931 | 🟡 MEDIUM |
| Kenya Re | 3,023 | 🟡 MEDIUM |
| Milimani | 2,690 | 🟡 MEDIUM |
| Middle East | 506 | 🟡 MEDIUM |
| **TOTAL** | **26,196** | **2 HIGH ZONES** |

> **Manyatta** and **Riat** account for **61% of all uncollected CIS records** and are designated as immediate Phase 2 priorities.

---

## Interactive Map Preview

> *(GeoJSON files in this repository render automatically as interactive maps on GitHub)*  
> Click `CIS_Gap_Buildings.geojson` above to explore the gap buildings spatially.

**Map Legend:**

- 🔴 **Red** — Gap buildings (CIS not collected in Phase 1)
- 🟢 **Green** — Collected buildings (Phase 1 CIS confirmed)
- 🔵 **Blue** — Pipeline network & 50m service buffer
- ⬛ **Black outline** — Ward administrative boundaries

---

## 🛠️ Tools & Data Sources

| Item | Detail |
|---|---|
| GIS Software | ArcGIS Pro 3.4 |
| Coordinate System | Arc 1960 / UTM Zone 36S (EPSG: 21036) |
| Pipeline Data | Kisumu County Water & Sewerage Company (KIWASCO) |
| Building Footprints | County GIS Department / Digitised from high-resolution imagery |
| Phase 1 CIS Data | Field collected via GPS — project fieldwork team |
| Administrative Boundaries | Kenya National Bureau of Statistics (KNBS) |

---

## 📋 Attribute Schema — CIS_Gap_Buildings.geojson

| Field Name | Type | Description |
|---|---|---|
| `OBJECTID` | Integer | Unique feature identifier |
| `CIS_Status` | String | `GAP - Not Collected` for all features in this layer |
| `Zone` | String | Administrative zone name |
| `Priority_Rank` | String | `HIGH` or `MEDIUM` |
| `Join_Count` | Integer | Always `0` — confirms no Phase 1 CIS match |
| `Area_m2` | Double | Building footprint area in square metres |
| `Shape_Length` | Double | Perimeter length in metres |

---

## 📍 Study Area

**County:** Kisumu County, Kenya  
**Region:** Lake Victoria Basin, Western Kenya  
**Coordinate System:** Arc 1960 / UTM Zone 36S  
**Coverage:** Full water utility service area including urban, peri-urban, and rural distribution zones

---

## 📞 Contact & Project Team

This repository is maintained by the project GIS team responsible for the Kisumu County Water Utility Mapping Project.

For technical enquiries regarding the dataset, methodology, or Phase 2 field operations, please contact the project team via the Kisumu County Water & Sewerage Company (KIWASCO) procurement office.

---

## ⚖️ Data Use & Disclaimer

This dataset is shared for **county government review and tender documentation purposes only**. All spatial data remains the property of Kisumu County Government and KIWASCO. Redistribution or use outside the scope of this project requires written authorisation from the county.

The gap counts presented are **predicted estimates** derived from spatial modelling. Final confirmed counts will be established upon completion of Phase 2 field verification.

---

*Last updated: February 2026 | ArcGIS Pro 3.4 | EPSG: 21036*
