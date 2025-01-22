---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: snippet code
nav_order: 5
parent: Geospatial
has_children: true
heading_anchors: true
permalink: /geospatial/snippet
has_toc: false
---

# Geospatial Snippet Collection
Personal Projects and Curiosity-Driven Explorations
<br>

geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
snippet
{: .badge .badge-pill .badge-info }

<p style='text-align: justify;'>
Welcome to the Geospatial Snippet Collection, a curated selection of code examples and practical tips for working with geospatial data.</p>

<p style='text-align: justify;'>
This page is part of my portfolio, where I share snippets that tackle real-world geospatial challenges—things like visualizing geographic patterns, analyzing spatial relationships, or even making interactive maps. Each snippet is designed to be straightforward and reusable, so you can adapt them to your own projects or just use them as inspiration.</p>

What you’ll find here:
<ul>
    <li>Mapping Magic: Snippets for creating beautiful, interactive maps using libraries like Folium, Leaflet, and Plotly.</li> 
    <li>Spatial Analysis: Quick solutions for calculating distances, identifying clusters, and performing geospatial queries.</li> 
    <li>Integrations: Tips for combining geospatial data with tools like Python, QGIS, or Google Maps APIs.</li> 
</ul>

<p style='text-align: justify;'>
I created this collection to share my journey working with geospatial data, from messy datasets to meaningful insights. So, dive in, experiment, and feel free to reach out if you have feedback, questions, or ideas!</p>


Before diving into the snippet code, here are the main libraries utilized throughout the collection:

```python
import numpy as np
import pandas as pd
import geopandas as gpd
from shapely.geometry import Point, LineString, Polygon
import json
import folium
import matplotlib.pyplot as plt
import os

from ursar_optimization import optimization
from ursar_map import maps
from ursar_statistic import statistic
from ursar_visual import visual
```