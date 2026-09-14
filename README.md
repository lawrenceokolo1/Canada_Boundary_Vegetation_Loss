# Canada Boundary & Vegetation Loss Analysis
A geospatial pipeline that combines Statistics Canada administrative boundary data with Landsat satellite imagery to map vegetation loss across Canada's fire-prone provinces between 2022 and 2025.

# About
This project demonstrates how administrative boundary data (StatCan Census Subdivisions) can be used to scope, validate, and contextualize satellite-based change detection, turning a raw remote sensing index into something tied to real jurisdictions like provinces, census divisions, and municipalities.
The core analysis uses the Normalized Burn Ratio (NBR), calculated from Landsat 8 surface reflectance imagery, compared across two matching summer windows (July–August 2022 vs. July–August 2025) to produce a dNBR (delta NBR) change layer. Positive values indicate vegetation loss between the two periods.
Note: dNBR detects vegetation loss broadly, it is not a confirmed-fire detector on its own. Loss signals can also come from logging, insect infestation, or land conversion. Cross-referencing an independent fire perimeter dataset (e.g., CWFIS, NASA FIRMS) would be needed to confirm fire specifically.

# What's Included
Boundary construction: Loading and filtering StatCan Census Subdivision boundaries (province → division → subdivision), including custom multi-division AOIs (e.g., Lake Ontario shoreline).
Earth Engine bridge: Re-importing boundary data as a server-side FeatureCollection for use in Google Earth Engine.
NBR / dNBR analysis: Building seasonally-matched Landsat composites, calculating NBR for each period, and differencing them to produce a vegetation-loss change layer.
Interactive visualization: Side-by-side imagery comparison, a color-coded dNBR severity map, and administrative boundary overlays, exportable as a standalone HTML file.

# Data Sources
Boundaries: Statistics Canada, Census Subdivision boundary file (lcsd000a25a_e)
https://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/bound-limit-s-eng.cfm?year=25

Imagery: USGS Landsat 8, Collection 2, Level-2 Surface Reflectance (LANDSAT/LC08/C02/T1_L2), accessed via Google Earth Engine

# You'll also need:
A Google Earth Engine account with an initialized Cloud project
The StatCan Census Subdivision shapefile (download from StatCan's website)

# Running It
Update the Earth Engine project ID and local file paths at the top of the notebook to match your environment.
Run the cells in order, boundary loading/filtering first, then the Earth Engine and NBR/dNBR sections.
The final cell exports an interactive map as a standalone HTML file, viewable in any browser.

# Limitations
dNBR indicates vegetation loss, not confirmed fire, other disturbances (harvest, pests, land conversion) can produce a similar signal.
No topographic correction is applied, which can matter in mountainous regions.
The Lake Ontario shoreline AOI is manually curated by division name, not derived from a hydrological boundary, it includes each full division, not just the immediate shoreline.

# Author
Lawrence Okolo
