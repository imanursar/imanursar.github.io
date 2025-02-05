---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Extract Specific Geographic Data
parent: Scraping Geospatial Data
permalink: /scraping geo data/extract spatial
nav_order: 3
---

#  Extract Specific Geographic Data
scraping data
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-secondary }

<img src="/assets/images/scrap geo/oms_extract_01.png" alt="drawing" width="500"/>

## Introduction
<p style='text-align: justify;'>
The OpenStreetMap (OSM) Overpass API is a powerful tool that allows users to query and extract specific geographic data from the vast OpenStreetMap database. Unlike traditional map APIs that focus on rendering maps, Overpass is designed for retrieving raw geospatial data, making it especially useful for developers, researchers, and data analysts. With Overpass, users can filter and fetch details like place names, amenities, and exact geolocations, all without needing to download the entire OSM dataset. This makes it an efficient and flexible solution for anyone looking to work with location-based data in real time.

One of the key advantages of using the Overpass API is its ability to execute highly customized queries using OverpassQL, a query language specifically designed for OSM data. For example, if you need a list of restaurants, hospitals, or public parks in a specific city, you can craft a simple query to return only the relevant points of interest along with their names and coordinates. This is particularly useful for applications like location-based services, urban planning, or geographic analysis. Since OpenStreetMap is constantly updated by a global community, the data you get is often more current and detailed than other proprietary mapping services, making Overpass an invaluable resource for working with open geospatial data.
</p>

## The Code
By calling `maps.extract_spatial`, we extract specific geographic data from the vast OpenStreetMap database by create specific filter such as: boundary and amenity.

```python
boundary= [47.46, 19.03, 47.53, 19.07]
amenity_list = [('amenity','cafe'), ('amenity','pub'),]

result = maps.extract_spatial(boundary, amenity_list= amenity_list, place_at='jakarta')
```

This function requires the following parameters:
- **boundary** (`list`):            list of longitude and latitude.
- **amenity_list** (`list`):        amenity list that we want to extract.
- **place_at**(`string`):           specific location

## The result

|    | name          | amenity_cat   | amenity   | geometry                      |   longitude |   latitude |
|---:|:--------------|:--------------|:----------|:------------------------------|------------:|-----------:|
|  0 | Cookie Beacon | amenity       | cafe      | POINT (19.0528557 47.5022714) |     19.0529 |    47.5023 |
|  1 | Kino          | amenity       | cafe      | POINT (19.0517508 47.5121665) |     19.0518 |    47.5122 |
|  2 | N/A           | amenity       | cafe      | POINT (19.0531945 47.504527)  |     19.0532 |    47.5045 |
|  3 | Szamos Today  | amenity       | cafe      | POINT (19.0478428 47.505579)  |     19.0478 |    47.5056 |
|  4 | À la Maison   | amenity       | cafe      | POINT (19.0526831 47.4953643) |     19.0527 |    47.4954 |

<img src="/assets/images/scrap geo/oms_extract_01.png" alt="drawing"/>

|                     | geometry                      | addr:city   |   addr:housenumber |   addr:postcode | addr:street            | amenity   |   capacity | check_date:opening_hours   | contact:email            |   contact:facebook |
|:--------------------|:------------------------------|:------------|-------------------:|----------------:|:-----------------------|:----------|-----------:|:---------------------------|:-------------------------|-------------------:|
| ('node', 260896310) | POINT (19.0528557 47.5022714) | Budapest    |                 15 |            1051 | Hercegprímás utca      | cafe      |         67 | 2024-07-11                 | tanya@cookiebeacon.com   |        1.00076e+14 |
| ('node', 260900823) | POINT (19.0547717 47.5083433) | Budapest    |                 72 |            1055 | Bajcsy-Zsilinszky út   | pub       |         50 | nan                        | nan                      |        1.00057e+14 |
| ('node', 260911188) | POINT (19.0485417 47.5121822) | Budapest    |                 32 |            1055 | Falk Miksa utca        | pub       |         35 | nan                        | tokajiborozo@gmail.com   |        1.0007e+14  |
| ('node', 263984860) | POINT (19.0531945 47.504527)  | Budapest    |                  1 |            1054 | Nagysándor József utca | cafe      |        nan | nan                        | nan                      |      nan           |
| ('node', 263988027) | POINT (19.0478428 47.505579)  | Budapest    |                 10 |            1055 | Kossuth Lajos tér      | cafe      |         50 | nan                        | parlament.cafe@szamos.hu |        1.79802e+15 |