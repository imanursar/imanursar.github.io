---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Scraping Geospatial Data
nav_order: 93
has_children: true
heading_anchors: true
permalink: /scraping geo data
has_toc: false
---

# Data Science Portfolio
Personal Projects and Curiosity-Driven Explorations
<br>

## Scraping Data with Google Maps API for Market Expansion
scraping data
{: .badge .badge-pill .badge-primary }
google maps API
{: .badge .badge-pill .badge-secondary }


### Introduction
<p style='text-align: justify;'>To grow our acquisition efforts and truly understand the market potential—both for Upstream and downstream buyers— we need access to the right data. This means identifying and targeting untapped potential customers, whether they are small-scale farmers, distributors, or retailers who haven't yet been engaged with our platform.</p>


<p style='text-align: justify;'>One of the most effective ways to gather this data is through data scraping, particularly from sources like Google Maps API. By utilizing Google Maps, we can collect valuable information about businesses, locations, and customer segments in both upstream and downstream markets.</p>

<img src="/assets/images/scrap geo/google_map/scraping_02.png" alt="drawing" width="500"/>

<span class="fs-3">
[Read more](../scraping geo data/google map data){: .btn }
</span>


## Exploring Nearby Places with Spatial Data: Fetching Points of Interest
scraping data
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-secondary }

### Introduction
<p style='text-align: justify;'>When you're looking for places around you—whether it's coffee shops, ATMs, parks, or gas stations—you’re essentially looking for Points of Interest (POIs). These are specific locations that serve a purpose for people, like businesses, landmarks, or public facilities. One of the best ways to fetch and analyze POIs is by using OpenStreetMap (OSM), a rich, community-driven map database.</p>

<img src="/assets/images/scrap geo/nfs/nfs_03.png" alt="drawing" width="500"/>

<span class="fs-3">
[Read more](../scraping geo data/nearby feat spatial){: .btn }
</span>


## Extract Specific Geographic Data
scraping data
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-secondary }

### Introduction
<p style='text-align: justify;'>The OpenStreetMap (OSM) Overpass API is a powerful tool that allows users to query and extract specific geographic data from the vast OpenStreetMap database. Unlike traditional map APIs that focus on rendering maps, Overpass is designed for retrieving raw geospatial data, making it especially useful for developers, researchers, and data analysts. With Overpass, users can filter and fetch details like place names, amenities, and exact geolocations, all without needing to download the entire OSM dataset. This makes it an efficient and flexible solution for anyone looking to work with location-based data in real time.</p>

<img src="/assets/images/scrap geo/geodata/oms_extract_01.png" alt="drawing" width="500"/>

<span class="fs-3">
[Read more](../scraping geo data/extract spatial){: .btn }
</span>


##  Extract Administrative Areas Polygon Data
scraping data
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-secondary }

<p style='text-align: justify;'>
Working with geographic data often requires precise boundaries for cities, districts, or other administrative areas. In this project, we want to create this process seamless by allowing users to extract detailed polygon data directly from OpenStreetMap (OSM). Instead of manually searching for shapefiles or relying on third-party sources, this project enables us to retrieve administrative boundaries programmatically with just a few lines of code. This is especially useful for urban planning, spatial analysis, and mapping applications, as it provides accurate and up-to-date data sourced from the global OSM community.
</p>

<img src="/assets/images/scrap geo/geodata/oms_polygon_01.png" alt="drawing" width="500"/>

<span class="fs-3">
[Read more](../scraping geo data/extract polygon){: .btn }
</span>


##  Extract Graph Data from OpenStreetMap (OSM)
scraping data
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-secondary }

<p style='text-align: justify;'>
When working with geographic networks, having access to raw road and pathway data is essential for tasks like route optimization, traffic analysis, and urban planning. OpenStreetMap (OSM) provides a wealth of such data.

With this project, we are extracting structured graph data becomes a straightforward process. This project allows us to pull detailed network information, including nodes (intersections or points of interest) and edges (roads, paths, or trails), filtered by specific network types like drive, walk, or bike networks.
</p>

<img src="/assets/images/scrap geo/geodata/oms_graph_01.png" alt="drawing" height="150"/>

<span class="fs-3">
[Read more](../scraping geo data/extract graph){: .btn }
</span>








### Links
- Source code on [my github](https://github.com/imanursar/)