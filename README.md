# 🗺️ Vietnam Population Density Visualization

Visualization of population density changes in major Vietnamese cities using WorldPop raster data and OpenStreetMap boundaries.
Vietnam was chosen as an example — the same approach works for any country or city in the world. WorldPop provides raster data for 200+ countries, and OpenStreetMap covers boundaries globally.

## 📊 Cities

- Hanoi
- Ho Chi Minh City (Saigon)
- Da Nang
- Phu Quoc

## 📁 Project Structure

```
12_POPULATION/
├── test.ipynb              # Main notebook
├── vnm_pd_2000_1km.tif     # Population density raster 2000
├── vnm_pd_2010_1km.tif     # Population density raster 2010
├── vnm_pd_2015_1km.tif     # Population density raster 2015
├── vnm_pd_2020_1km.tif     # Population density raster 2020
└── README.md
```

## 🛠️ Stack

| Library | Purpose |
|---|---|
| `osmnx` | Fetching city boundary polygons from OpenStreetMap |
| `rasterio` | Reading and clipping GeoTIFF raster files |
| `geopandas` | Working with geographic dataframes |
| `matplotlib` | Building visualizations |
| `numpy` | Numerical operations and NaN handling |
| `glob` | Auto-detecting .tif files in the directory |


## 🌍 Data Source

Raster data: [WorldPop](https://hub.worldpop.org) — Unconstrained individual countries 2000–2020, 1km resolution.  
City boundaries: OpenStreetMap via `osmnx`.

## ⚙️ How It Works

1. **`load_city_data(city_name)`** — fetches the city boundary from OSM, then clips each `.tif` raster file to that boundary. Returns a dictionary `{year: array}`.

2. **`plot_city(years_data, city_title)`** — builds a 2×2 grid of maps with a shared color scale (Viridis colormap). The color range is set using the 95th percentile to avoid outliers skewing the palette.

## 🎨 Color Scale

viridis (Purple → Blue → Green → Yellow): darker purple = lower density, bright yellow = higher density.
A single shared colorbar is used across all 4 subplots for easy comparison between years.# Population-Density
