# Fabric Map Geospatial Data Preparation with Apache Sedona

This repository contains a **Fabric Spark notebook** that prepares large-scale geospatial datasets—such as nationwide building footprints—for visualization in **Fabric Map**.

Using **Apache Sedona** for geospatial processing, the notebook:

- Ingests geospatial source data into OneLake  
- Converts data to **GeoJSON**
- Reprojects geometry to **EPSG:4326 (WGS 84)**
- Subsets outputs into **≤ 1 GB GeoJSON files**
- Produces map‑ready data that Fabric Map converts to **PMTiles** for scalable visualization

The approach keeps geospatial complexity out of the visualization layer so **Fabric Map** can focus on high‑performance, interactive insights.

---

## Contents

- `01_geo_preprocess.ipynb` – Fabric Spark notebook with the full preprocessing logic

---

## Prerequisites

- Microsoft Fabric workspace
- A **Lakehouse** (set as *default* for the notebook)
- Fabric **Spark** runtime
- **Apache Sedona** libraries available to the Spark session

For Sedona setup guidance in Microsoft Fabric, see:  
https://sedona.apache.org/latest/setup/fabric/

---

## Getting started in Microsoft Fabric

### 1) Prepare Apache Sedona JARs in your default Lakehouse

In your **default Lakehouse**, do the following:

1. Create a folder to store Sedona dependencies:
2. Upload these JARs into that folder:
- `geotools-wrapper-1.8.0-33.1.jar`
- `sedona-spark-shaded-3.5_2.12-1.8.0.jar`
> These versions align with the example notebook. Adjust if your environment uses different Spark/Sedona versions.

### 2) Configure the notebook to load Sedona JARs (ABFS paths)

At the **top of the notebook**, add a Fabric‑specific `%%configure` cell and reference the JARs using their **ABFS** paths.

## Outputs
Output files are stored in a versioned folder under the Lakehouse Files area, e.g.:

/lakehouse/default/Files/

  BAG_geojson_province_WGS84_4326_YYYYMM_vXX/
  
    BRK_provincies.geojson
    
    BAG_<province>_01.geojson
    
    BAG_<province>_02.geojson
    
    BAG_verblijfsobject_<province>_01.geojson
    
    ...

## License
This project uses Apache Sedona, which is licensed under the Apache License, Version 2.0.

BAG data: Creative Commons Public Domain Mark v1.0 https://creativecommons.org/publicdomain/zero/1.0/deed.nl 

BRK data: http://creativecommons.org/licenses/by/4.0/deed.nl

  http://inspire.ec.europa.eu/metadata-codelist/ConditionsApplyingToAccessAndUse/noConditionsApply
  
  http://inspire.ec.europa.eu/metadata-codelist/LimitationsOnPublicAccess/noLimitations
  
    
