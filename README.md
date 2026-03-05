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

**Environment:**
- Python 3.12
- Jupyter Notebook
- VS Code

**Library versions:**
- `osmnx` 2.1.0
- `rasterio` 1.5.0
- `geopandas` 1.1.2
- `matplotlib` 3.9.2
- `numpy` 1.26.4
- `glob` (built-in)

| Library | Purpose |
|---|---|
| `osmnx` | Fetching city boundary polygons from OpenStreetMap |
| `rasterio` | Reading and clipping GeoTIFF raster files |
| `geopandas` | Working with geographic dataframes |
| `matplotlib` | Building visualizations |
| `numpy` | Numerical operations and NaN handling |
| `glob` | Auto-detecting .tif files in the directory |

## 📦 Installation

```bash
pip install osmnx geopandas rasterio matplotlib numpy
```

> ⚠️ If you get a NumPy compatibility error, downgrade to NumPy 1.x:
> ```bash
> pip install "numpy<2" --force-reinstall
> ```

## 🌍 Data Source

Raster data: [WorldPop](https://hub.worldpop.org) — Unconstrained individual countries 2000–2020, 1km resolution.  
TIFF files were downloaded manually from WorldPop for Vietnam specifically — one file per year. The same dataset is available for 200+ countries.  
City boundaries: OpenStreetMap via `osmnx`.

## ⚙️ How It Works

1. **`load_city_data(city_name)`** — fetches the city boundary from OSM, then clips each `.tif` raster file to that boundary. Returns a dictionary `{year: array}`.

2. **`plot_city(years_data, city_title)`** — builds a 2×2 grid of maps with a shared color scale (YlOrRd colormap). The color range is set using the 95th percentile to avoid outliers skewing the palette.

## 🎨 Color Scale

`viridis` (Purple → Blue → Green → Yellow): darker purple = lower density, bright yellow = higher density.  
A single shared colorbar is used across all 4 subplots for easy comparison between years.