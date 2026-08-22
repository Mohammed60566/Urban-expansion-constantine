# Urban Expansion Analysis — Constantine, Algeria (2015–2020)

**GIS change-detection project measuring built-up area growth in Wilaya de Constantine, Algeria, between 2015 and 2020, using free open satellite-derived data.**

![Final map](Urban_Expansion_Constantine_2015_2020.png)

---

## Overview

This project answers one question: **how did the built-up area of Constantine change between 2015 and 2020, and where was that growth concentrated?**

Rather than showing a static snapshot, the analysis compares two independently measured time points and derives a real change-detection layer — the standard approach in remote sensing and urban planning studies.

## Key Result

> Built-up surface in Wilaya de Constantine increased by approximately **2.98 km²** between 2015 and 2020, with **no measured decrease** recorded anywhere in the study area.

| Statistic | Value |
|---|---|
| Pixel count | 224,880 (100 m resolution) |
| Minimum change | 0 m² |
| Maximum change (single pixel) | 5,467 m² |
| Total increase | 2,975,661 m² (~2.98 km²) |

## Data & Methods

| Item | Detail |
|---|---|
| Boundary | Wilaya de Constantine, OpenStreetMap (administrative relation, level 4) |
| Built-up data | [GHS-BUILT-S R2023A](https://human-settlement.emergency.copernicus.eu/) — European Commission, Joint Research Centre (JRC), 100 m resolution |
| Epochs used | 2015 and 2020 — the two most recent **measured** epochs (2025/2030 are model projections and were excluded) |
| CRS | WGS84 (EPSG:4326) for the boundary; World Mollweide (ESRI:54009) for GHSL rasters |
| Method | Pixel-wise raster difference: `Built-up(2020) − Built-up(2015)`, both rasters clipped to the wilaya boundary before comparison |
| Software | QGIS (Desktop) |

Full step-by-step methodology, including every tool and menu path used, is documented in
[`Urban_Expansion_Constantine_Methodology.pdf`](Urban_Expansion_Constantine_Methodology.pdf).

## Workflow Summary

1. Downloaded the Constantine administrative boundary from OpenStreetMap and exported it as GeoJSON.
2. Identified and downloaded the correct GHS-BUILT-S tile covering Constantine, for epochs 2015 and 2020.
3. Loaded boundary and raster data into QGIS; verified spatial alignment visually.
4. Clipped both raster layers to the exact boundary of Constantine (same extent for both).
5. Computed the pixel-wise difference (2020 − 2015) using the Raster Calculator.
6. Extracted summary statistics (min, max, sum) with the Raster Layer Statistics tool.
7. Designed a three-panel map layout (Built-up 2015 / Urban Change / Built-up 2020) with a shared scale bar, north arrow, and cleaned legend.
8. Exported the final map as a high-resolution PDF.

## Repository Contents

| File | Description |
|---|---|
| `urban_expansion_constantine.qgz` | QGIS project file (all layers, styling, and the final layout) |
| `Urban_Expansion_Constantine_2015_2020.pdf` | Final cartographic output (3-panel map, print-ready) |
| `Urban_Expansion_Constantine_Methodology.pdf` | Full step-by-step methodology and tool documentation |
| `data/` | Boundary GeoJSON and clipped GHSL raster layers used in the analysis |

## Limitations

- GHS-BUILT-S measures built-up **surface** per grid cell, not the administrative city boundary or every urbanized land use (e.g. roads, informal settlements below detection resolution).
- 100 m spatial resolution means small or scattered individual buildings may not be resolved as distinct features.
- The color scale on the "Urban Change" map was adjusted for visual clarity only (display stretch); the statistics above were computed from the unmodified raster values.

## Data Sources & Attribution

- Built-up data: © European Union, Joint Research Centre, [GHS-BUILT-S R2023A](https://human-settlement.emergency.copernicus.eu/)
- Boundary data: © OpenStreetMap contributors

---

*Project 1 of a GIS portfolio series (Urban Growth Analysis → Spatial Data Analysis with Python → Territorial Planning Suitability Analysis → Environmental Risk Mapping).*
