---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Extract Graph Data
parent: Scraping Geospatial Data
permalink: /scraping geo data/extract graph
nav_order: 5
---

#  Extract Graph Data from OpenStreetMap (OSM)
scraping data
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-secondary }

<img src="/assets/images/scrap geo/geodata/oms_graph_01.png" alt="drawing" height="150"/>

## Introduction
<p style='text-align: justify;'>
When working with geographic networks, having access to raw road and pathway data is essential for tasks like route optimization, traffic analysis, and urban planning. OpenStreetMap (OSM) provides a wealth of such data.

With this project, we are extracting structured graph data becomes a straightforward process. This project allows us to pull detailed network information, including nodes (intersections or points of interest) and edges (roads, paths, or trails), filtered by specific network types like drive, walk, or bike networks. This makes it an invaluable tool for researchers, data scientists, and urban planners looking to model and analyze real-world transportation systems efficiently.
</p>

## The Code
By calling `maps.get_geodata_area`, we extract specific graph geographic data from the vast OpenStreetMap database. we can request difference network types to get nodes and edges for specific area. 

```python
nodes, edges = maps.get_geodata_area(places= ['5th district, Budapest'], 
                                    amenity_list= None, types= 'graph', network_type='drive')
```

This function requires the following parameters:
- **places**(`list`):               specific locations
- **amenity_list** (`list`):        amenity list that we want to extract.
- **types**(`string`):              type of data request. `['polygon', 'graph']`
- **network_type** (`string`):      What type of street network to retrieve `[“all”, “all_public”, “bike”, “drive”, “drive_service”, “walk”]`

## The result

<img src="/assets/images/scrap geo/geodata/oms_graph_01.png" alt="drawing"/>

### Nodes

|    osmid |       y |       x |   street_count |   highway | geometry                      |
|---------:|--------:|--------:|---------------:|----------:|:------------------------------|
| 26733991 | 47.4995 | 19.0548 |              4 |       nan | POINT (19.0548448 47.4995112) |
| 49405178 | 47.4988 | 19.0472 |              3 |       nan | POINT (19.0472104 47.4987813) |
| 49405188 | 47.4986 | 19.0479 |              4 |       nan | POINT (19.0478778 47.4985865) |
| 49405195 | 47.499  | 19.0481 |              3 |       nan | POINT (19.0480862 47.4989506) |
| 49405214 | 47.5004 | 19.0473 |              3 |       nan | POINT (19.0473297 47.5004243) |

### Edges

|                           | osmid                  | highway       |   lanes |   maxspeed | name                 | oneway   | reversed   |   length | geometry                                                                                                                                            |   width |   tunnel |   access |   ref |   bridge |
|:--------------------------|:-----------------------|:--------------|--------:|-----------:|:---------------------|:---------|:-----------|---------:|:----------------------------------------------------------------------------------------------------------------------------------------------------|--------:|---------:|---------:|------:|---------:|
| (26733991, 84700676, 0)   | [17275204, 217483071]  | tertiary      |       5 |         50 | József Attila utca   | False    | False      |  50.1592 | LINESTRING (19.0548448 47.4995112, 19.0545939 47.4993435, 19.0543282 47.4992295)                                                                    |     nan |      nan |      nan |   nan |      nan |
| (26733991, 260238323, 0)  | [553123799, 127553887] | secondary     |       7 |         50 | Bajcsy-Zsilinszky út | False    | False      | 101.313  | LINESTRING (19.0548448 47.4995112, 19.0548519 47.4997977, 19.0548609 47.5001582, 19.0548675 47.5004222)                                             |     nan |      nan |      nan |   nan |      nan |
| (26733991, 1433298790, 0) | 262231175              | secondary     |       6 |         50 | Bajcsy-Zsilinszky út | False    | True       |  35.9401 | LINESTRING (19.0548448 47.4995112, 19.054841 47.499415, 19.0548215 47.4991884)                                                                      |     nan |      nan |      nan |   nan |      nan |
| (49405178, 1382906629, 0) | 16608102               | tertiary_link |       1 |         50 | Széchenyi István tér | True     | False      |  21.508  | LINESTRING (19.0472104 47.4987813, 19.0472507 47.4985898)                                                                                           |     nan |      nan |      nan |   nan |      nan |
| (49405178, 49405188, 0)   | [325386555, 553110630] | tertiary      |       2 |         50 | Széchenyi István tér | True     | False      |  61.7512 | LINESTRING (19.0472104 47.4987813, 19.047362 47.4986256, 19.0474262 47.4985863, 19.0475252 47.498565, 19.0477184 47.4985655, 19.0478778 47.4985865) |     nan |      nan |      nan |   nan |      nan |