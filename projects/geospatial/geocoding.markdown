---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Geocoding
parent: Geospatial
permalink: /geospatial/geocoding
nav_order: 20
---

#  Geocoding

geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
geocoding
{: .badge .badge-pill .badge-info }

Transforming address to a coordinate
<img src="/assets/images/geospatial/snippet/geocoding.jpg" alt="drawing" width="500"/>

## Introduction
<p style='text-align: justify;'>
Geocoding is the process of transforming a description of a location—such as a pair of coordinates, an address, or a name of a place—to a location on the earth's surface. You can geocode by entering one location description at a time or by providing many of them at once in a table. The resulting locations are output as geographic features with attributes, which can be used for mapping or spatial analysis.</p>

<p style='text-align: justify;'>
You can quickly find various kinds of locations through geocoding. The types of locations that you can search for include points of interest or names from a gazetteer, like mountains, bridges, and stores; coordinates based on latitude and longitude or other reference systems, and addresses, which can come in a variety of styles and formats, including street intersections, house numbers with street names, and postal codes.</p>

## Dataset

### Load dataset
We’ll be working with the Zomato - India Restaurant dataset, which includes various details about restaurants. For this analysis, we’ll focus on the `Locality` parameter, which provides the addresses of restaurants across India. This will serve as the key element in mapping and analyzing restaurant locations.

```python
data = pd.read_csv(r'..\map\zomato.csv',encoding="ISO-8859-1")
df = data[['Locality']]
```
|    | Locality                                   |
|---:|:-------------------------------------------|
|  0 | Century City Mall, Poblacion, Makati City  |
|  1 | Little Tokyo, Legaspi Village, Makati City |
|  2 | Edsa Shangri-La, Ortigas, Mandaluyong City |
|  3 | SM Megamall, Ortigas, Mandaluyong City     |
|  4 | SM Megamall, Ortigas, Mandaluyong City     |


## Get the coordinate for each locations
There are several method to get the coordinate for each locations by using geocoding. The simple and common method such as :

- Openstreetmap.org (OSM)
is a digital map database of the world built through crowdsourced volunteered geographic information (VGI). **it is means free but not accurate**. You can read usage policy OSM [here](http://wiki.openstreetmap.org/wiki/Tile_usage_policy).

- Google Maps Platform
is a web mapping platform and consumer application offered by Google. We need billing to access their API. **It is means reliable but costly**.

For this project we can use OSM method, for example to see how good our result is.

<img src="/assets/images/geospatial/tsp/tsp_10.png" alt="drawing" width="300"/>


## The Code
By calling `maps.spatial_interpolation`, we can weather stations reporting data for January 1, 2022 across Ohio, and calculate interpolation for area around them.

```python
result = maps.geocoding(main_data, col_address, source='osm', key='your_API_key')
```

This function requires the following parameters:
- **main_data** (`string`):          Data location and value    
- **col_name** (`string`):           Targated column in main_data    
- **source** (`string`):             `[osm, oc, osm_v2, google]`, Type of geocoding source that we want to use.
- **key** (`string`):                key ID specific for google API


## The result
### OSM

|    | Locality       |   latitude |   longitude | geometry                       |
|---:|:---------------|-----------:|------------:|:-------------------------------|
| 1  | Addition Hills |    14.5856 |     121.038 | POINT (121.0381198 14.5856046) |
| 2  | Little Baguio  |    10.7857 |     122.3   | POINT (122.3001517 10.7857333) |

### Google API

|    | Locality       |   latitude |   longitude | geometry                       |
|---:|:---------------|-----------:|------------:|:-------------------------------|
| 1  | Addition Hills |    14.5829 |     121.038 | POINT (121.0378102 14.5829437) |
| 2  | Little Baguio  |    14.6018 |     121.037 | POINT (121.0370935 14.6018011) |

### OpenCage Geocoding API

|    | Locality       |   latitude |   longitude | geometry                       |
|---:|:---------------|-----------:|------------:|:-------------------------------|
| 1  | Addition Hills |    14.594  |      121.04 | POINT (121.0398547 14.5940121) |
| 2  | Little Baguio  |    10.7857 |      122.3  | POINT (122.3001517 10.7857333) |


## What can geocoding be used for?

<p style='text-align: justify;'>
From simple data analysis to business and customer management to distribution techniques, there is a wide range of applications for which geocoding can be used. With geocoded addresses, you can spatially display the address locations and recognize patterns within the information. This can be done by simply looking at the information or using some of the analysis tools available with ArcGIS. You can also display your address information based on certain parameters, allowing you to further analyze the information. A few of these applications are described in the sections that follow.</p>

- **Address data analysis** - With geocoded addresses, you can spatially display the address locations and begin to recognize patterns within the information.

- **Customer data management** - Geocoding acts as a crucial part of customer data management. Nearly every organization maintains address information for each customer or client. This is usually in tabular format, containing the customer name, address, buying habits, and any other information you have collected. Geocoding allows you to take your customers' information and create a map of their locations. Using a variety of related applications, you can use this information in many ways, from establishing marketing strategies to targeting specific clusters of customers to producing route maps and directions. The geocoded locations of your customers can be invaluable data.

## reference
- https://desktop.arcgis.com/en/arcmap/latest/manage-data/geocoding/what-is-geocoding.htm