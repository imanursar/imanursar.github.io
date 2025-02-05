---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Extract Polygon Data
parent: Scraping Geospatial Data
permalink: /scraping geo data/extract polygon
nav_order: 4
---

#  Extract Administrative Areas Polygon Data and Its Amenity in The Area
scraping data
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-secondary }

<img src="/assets/images/scrap geo/geodata/oms_polygon_01.png" alt="drawing" width="500"/>

## Introduction
<p style='text-align: justify;'>
Working with geographic data often requires precise boundaries for cities, districts, or other administrative areas. In this project, we want to create this process seamless by allowing users to extract detailed polygon data directly from OpenStreetMap (OSM). Instead of manually searching for shapefiles or relying on third-party sources, this project enables us to retrieve administrative boundaries programmatically with just a few lines of code. This is especially useful for urban planning, spatial analysis, and mapping applications, as it provides accurate and up-to-date data sourced from the global OSM community.
</p>

## The Code
By calling `maps.get_geodata_area`, we extract specific polygon geographic data from the vast OpenStreetMap database. we can request multiple polygon data in this code. we also can specifically to get amenity for single area by input dict amenity at `amenity_list`.

```python
amenity_list= {'amenity': ['cafe', 'pub'], 
                'tourism': ['gallery']}

maps.get_geodata_area(places= ['Jakarta'], amenity_list=amenity_list)
```

This function requires the following parameters:
- **places**(`list`):               specific locations
- **amenity_list** (`list`):        amenity list that we want to extract.

## The result

<img src="/assets/images/scrap geo/geodata/oms_polygon_01.png" alt="drawing"/>
<img src="/assets/images/scrap geo/geodata/oms_polygon_02.png" alt="drawing"/>
<img src="/assets/images/scrap geo/geodata/oms_polygon_03.png" alt="drawing"/>

### Combination between Polygon and amenity at that polygon
<img src="/assets/images/scrap geo/geodata/oms_polygon_04.png" alt="drawing"/>


### Geometry data

|    | geometry      |   bbox_west |   bbox_south |   bbox_east |   bbox_north |   place_id | osm_type   |   osm_id |     lat |     lon | class    | type           |   place_rank |   importance | addresstype   | name         | display_name                                     |
|---:|:-----------|------------:|-------------:|------------:|-------------:|-----------:|:-----------|---------:|--------:|--------:|:---------|:---------------|-------------:|-------------:|:--------------|:-------------|:-------------------------------------------------|
|  0 | POLYGON ((19.0237592 47.4956175, 19.023763 47.4955493, )) |     19.0238 |      47.4857 |     19.0513 |      47.5081 |   59096160 | relation   |   221984 | 47.4992 | 19.0351 | boundary | administrative |           18 |     0.459212 | borough       | 1st district | 1st district, Budapest, Central Hungary, Hungary |


### POI / amenity data

|                     | geometry                      | addr:city   |   addr:postcode | addr:street        | amenity   | contact:email          | contact:facebook   |   contact:tripadvisor | contact:website            | indoor_seating   |
|:--------------------|:------------------------------|:------------|----------------:|:-------------------|:----------|:-----------------------|:-------------------|----------------------:|:---------------------------|:-----------------|
| ('node', 344907128) | POINT (19.0381341 47.502793)  | Budapest    |            1011 | Corvin tér         | cafe      | corvincoffee@gmail.com | CorvinCafeBistro   |           4.74387e+06 | https://www.corvincafe.hu/ | yes              |
| ('node', 735186601) | POINT (19.0397733 47.4962283) | Budapest    |            1014 | Szent György tér   | nan       | nan                    | nan                |         nan           | nan                        | nan              |
| ('node', 735220869) | POINT (19.0361743 47.4988089) | Budapest    |            1014 | Dísz tér           | cafe      | nan                    | nan                |         nan           | nan                        | nan              |
| ('node', 735221987) | POINT (19.0325501 47.5009532) | Budapest    |            1014 | Úri utca           | cafe      | nan                    | nan                |         nan           | nan                        | nan              |
| ('node', 735222199) | POINT (19.0329039 47.5012693) | Budapest    |            1014 | Szentháromság utca | cafe      | nan                    | nan                |         nan           | nan                        | yes              |