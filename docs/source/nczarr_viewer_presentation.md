---
marp: true
paginate: true
theme: edito-marp
backgroundImage: url('static/styles/background.jpg')
backgroundSize: cover
backgroundPosition: center
footer: '![Funded by the European Union](static/styles/footer-banner.png)'
# backgroundImage: url('source/static/branding/background.jpg')
# backgroundSize: cover
# backgroundPosition: center

# footer: '<img src="source/static/branding/footer-banner.png" width="280" alt="Funded by the European Union" />'

# # style: branding.
# # SIMPLER SELECTORS (let Marp add the scoping)
# style: |
#   /* Pin footer bottom-right, leave room for page number */
#   section > footer {
#     position: absolute;
#     right: 56px;
#     bottom: 12px;
#     margin: 0;
#     padding: 0;
#     z-index: 2;
#     text-align: right;
#   }
#   section > footer img { height: 32px; }

#   /* Move the pagination chip to the very edge */
#   section::after {
#     right: 10px;
#     bottom: 10px;
#     background: rgba(0,0,0,.35);
#     color: #fff;
#     padding: 2px 8px;
#     border-radius: 12px;
#     font-size: 12px;
#   }
# theme: edito
title: NCZarr Viewer
subtitle: Exploring and Subsetting Zarr & NetCDF Data
author: Samuel Fooks
---

# 🌊 NetCDF Zarr Viewer

## A Tool to Explore cloud data
**Samuel Fooks** - VLIZ  
**Making public NetCDF/Zarr Data Accessible to Everyone**

---

# NCZarr Viewer

- 📊 **Load and explore** NetCDF and Zarr datasets
- 🔍 **Browse variables** and dimensions through a simple interface
- ✂️ **Subset data** by time, space, and other dimensions visually
- 📈 **Visualize results** with interactive plots
- 🌍 **Access cloud data** directly from S3 buckets
- 🚀 **Work with large datasets** efficiently
- 🐳 **Containerized** for easy deployment and sharing

---

# 🏗️ Architecture Overview


👤 User Interface  →  🚀 Dash App  →  🗄️ Data Engine
         ↓                   ↓                ↓
    🖥️ Web Browser    🐍 Python Core    📊 Xarray
         ↓                   ↓                ↓
    🎨 Interactive UI   🔧 Data Manager   📁 NetCDF/Zarr

---

# 🛠️ Technology Stack

- **Frontend**: Dash + Bootstrap Components
- **Data Processing**: Xarray + NumPy
- **File Formats**: NetCDF4, Zarr
- **Visualization**: Plotly, Matplotlib, Cartopy 
- **Cloud Access**: S3FS, FSSpec (cloud storage access)
- **Marine Data**: Copernicus Marine Toolbox integration

---

# 🚀 Quick Start


```bash
# Option 1: Use Docker
docker run -p 8050:8050 samfooks/nczarr-viewer:latest

# Option 2: Local development (if you have Python)
git clone [https://github.com/EDITO-Infra/nczarr-viewer)](https://github.com/EDITO-Infra/nczarr-viewer)
cd nczarr-viewer
pip install -r requirements.txt
python run.py
```

**Access at**: http://localhost:8050

**💡 Tip**: Think of this as "R Shiny for NetCDF data" - but already built for you!

---

# 📁 Supported Data Sources

- **ARCO data on EDITO**: ARCO datasets from the EDITO STAC
- **Personal Cloud Storage**: [Minio storage](https://datalab.dive.edito.eu/file-explorer) on EDITO
- **Local Files**: NetCDF, Zarr

---

# 🔍 Core Features

## Data Exploration
- **Variable Browser**: See all variables, dimensions, and metadata
- **Dimension Handling**: Time, depth, latitude, longitude
- **Data Subsetting**: Interactive selection of regions and time periods

## Visualization
- **Interactive Maps**: Cartopy-based geographic plots
- **Time Series**: Plotly charts for temporal data
- **Statistical Analysis**: Basic stats, and summaries

---

# 🌊 Marine Data Examples

## EDITO Integration
- **Biodiversity**: Species distribution data
- **Chemistry**: Water quality parameters
- **Geology**: Seafloor characteristics
- **STAC Access**: Browse collections and datasets

## Copernicus Marine 
- **Direct Access**: CMEMS credentials integration (you will need an account)
- **Multiple Formats**: NetCDF, Zarr (and others in future)
- **Real-time Data**: Latest ocean observations

---

# 🚀 Performance Features

- **Chunked Processing**: Handle datasets larger than memory
- **Lazy Loading**: Only load data when needed
- **Cloud Optimization**: Efficient S3 data access

---

# 🔧 Configuration & Deployment

## Setup
To access CMEMS datasets you may need an account using [Copernicus Marine Toolbox](https://help.marine.copernicus.eu/en/articles/7949409-copernicus-marine-toolbox-introduction#h_9172b5c79a)
```bash
# CMEMS credentials
CMEMS_USERNAME=your_username
CMEMS_PASSWORD=your_password
```

## Docker Deployment
```bash
docker build -t nczarr-viewer .
docker run -p 8050:8050 nczarr-viewer
```

---

# 🔍 Subsetting ARCO Data: Core Concepts
## Multidimensional Data Structure
```
┌─────────────────────────────────────────────────────────┐
│                    ARCO Dataset                        │
├─────────────────────────────────────────────────────────┤
│  Variables: temperature, salinity, oxygen, etc.        │
│  Dimensions: time, depth, latitude, longitude          │
│  Shape: (time: 365, depth: 50, lat: 1800, lon: 3600) │
└─────────────────────────────────────────────────────────┘
```
### Subsetting Operations
- **Variable**: Pick specific parameters
- **Temporal**: Select specific dates
- **Spatial**: Choose latitude/longitude boundaries
- **Depth**: Select depth(elevation)

---

# 🎯 Subsetting in Practice

## Example: Extract Surface Temperature for North Sea
```python
import xarray as xr

# Load ARCO dataset
ds = xr.open_zarr("s3://arco-data/ocean-temp.zarr")

# Variable: surface temperature
temp_surface = ds['temperature'].sel(depth=0)

# Temporal: August 30
august30_data = temp_surface.sel(
    time='2025-08-30'
)
# Spatial bounds: North Sea region
north_sea = august30_data.sel(
    latitude=slice(51.0, 61.0),    # 51°N to 61°N
    longitude=slice(-5.0, 15.0)    # 5°W to 15°E
)

```

---

## Visual Representation
```
┌─────────────────────────────────────────────────────────┐
│  Original: 365×50×1800×3600                           │
│  ↓ Variable selection                                  │
│  Surface: 365×1×1800×3600                             │
│  ↓ Temporal subset                                     │
│  August 30, 2025: 1×1×1800×3600                       │
│  ↓ Spatial subset                                      │
│  North Sea region: 1×1×100×200                        │
└─────────────────────────────────────────────────────────┘
```

---

# 🌊 Use the NCZarr Viewer locally or on EDITO
<div style="text-align: center; margin: 20px 0;">
  <video width="70%" controls>
    <source src="static/nczarrviewer_localoredito.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

*Click to play*

---

##### Explore a NetCDF from your Minio bucket on EDITO

<div style="text-align: center; margin: 20px 0;">
  <video width="70%" controls>
    <source src="static/nczarrviewer_minionetcdf.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

*Click to play*

---

# 🌊 Live Demo Time!
##### Explore CMEMs dataset using zarr link from EDITO STAC

<div style="text-align: center; margin: 20px 0;">
  <video width="70%" controls>
    <source src="static/nczarrviewer_cmems.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

*Click to play*

---

# 🔮 Future Developments

- **More Interactive Visualization**: More interactive global maps and plots
- **Advanced Analytics**: Statistical modeling tools/plugins
- **New ARCO Data types**: Parquet, Geoparquet
- **Collaboration**: Multi-user editing and sharing

---

# 🌊 Thank You!

**Samuel Fooks** - samuel.fooks@vliz.be 
**GitHub**: [https://github.com/EDITO-Infra/nczarr-viewer](https://github.com/EDITO-Infra/nczarr-viewer)
**Docker Hub**: samfooks/nczarr-viewer

**Questions?**