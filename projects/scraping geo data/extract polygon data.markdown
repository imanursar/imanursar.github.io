---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Extract Polygon Data
parent: Scraping Geospatial Data
permalink: /scraping geo data/extract polygon
nav_order: 3
---

#  Extract Administrative Areas Polygon Data
scraping data
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-secondary }

<img src="/assets/images/scrap geo/oms_polygon_01.png" alt="drawing" width="500"/>

## Introduction
<p style='text-align: justify;'>
Working with geographic data often requires precise boundaries for cities, districts, or other administrative areas. In this project, we want to create this process seamless by allowing users to extract detailed polygon data directly from OpenStreetMap (OSM). Instead of manually searching for shapefiles or relying on third-party sources, this project enables us to retrieve administrative boundaries programmatically with just a few lines of code. This is especially useful for urban planning, spatial analysis, and mapping applications, as it provides accurate and up-to-date data sourced from the global OSM community.
</p>

## The Code
By calling `maps.get_poly_area`, we extract specific polygon geographic data from the vast OpenStreetMap database. we can request multiple polygon data in this code.

```python
maps.get_poly_area(places= ['Jakarta'])
```

This function requires the following parameters:
- **places**(`list`):           specific locations

## The result

<img src="/assets/images/scrap geo/oms_polygon_01.png" alt="drawing"/>
<img src="/assets/images/scrap geo/oms_polygon_02.png" alt="drawing"/>
<img src="/assets/images/scrap geo/oms_polygon_03.png" alt="drawing"/>