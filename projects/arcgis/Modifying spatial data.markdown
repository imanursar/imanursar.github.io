---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Modifying Spatial Data
nav_order: 3
parent: ArcGIS Pro
permalink: /ArcGIS/modify
---

# Modifying Spatial Data
argispro
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
esri
{: .badge .badge-pill .badge-info }


We work in the GIS department of Troutdale, Oregon. One of our jobs is to maintain the city’s GIS database. We are considering converting all the city’s shapefiles into the geodatabase feature class format because we want to take advantage of the benefits offered by the geodatabase. 

<img src="/assets/images/esri/esri_10.webp" alt="drawing"/>


# Editting and Snapping
The WaterLines layer is missing a line feature. In this part we will create it. We utilize snapping, snapping is an editing option that acts like a magnet. When editing, if the point you create is within a specified distance of another feature’s vertex, endpoints, edge, or intersection, it will jump (or snap) to coincide with another feature. Snapping allows you to accurately connect features, such as waterlines and valves, without impossibly precise sketching.
<img src="/assets/images/esri/esri_11.webp" alt="drawing"/>


## Split and Merge Polygons 
In this part we will modify existing features in the CityMaintain geodatabase. To stabilize water pressure throughout Troutdale, two new water towers were built, resulting in changes to water pressure zones. You will split an existing zone into two zones and then merge one of the new, smaller zones into an adjacent zone.
<img src="/assets/images/esri/esri_12.webp" alt="drawing"/>
<img src="/assets/images/esri/esri_13.webp" alt="drawing"/>
<img src="/assets/images/esri/esri_14.webp" alt="drawing"/>
<img src="/assets/images/esri/esri_15.webp" alt="drawing"/>


## Modify lines
A waterline was placed incorrectly. You will fix the error by moving its vertices. 
<img src="/assets/images/esri/esri_16.webp" alt="drawing"/>
<img src="/assets/images/esri/esri_17.webp" alt="drawing"/>
