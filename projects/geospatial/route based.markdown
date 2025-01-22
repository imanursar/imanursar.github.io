---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Route-based combinatorial optimization problems
parent: Geospatial
permalink: /geospatial/route_based/
nav_order: 5
---

# Route-based combinatorial optimization problems

geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
heatmap
{: .badge .badge-pill .badge-info }

<img src="/assets/images/geospatial/tsp/tsp_08.png" alt="drawing" width="1500"/>

## Introduction
<p style='text-align: justify;'>
Route-based combinatorial optimization problems set out to solve the most efficient route from point A to a set of destination points.
</p>

<p style='text-align: justify;'>
These problems can be simple, where a person or a vehicle departs a starting point and must travel to a set of destination points while visiting each point only once before returning to the origin point, all while minimizing the distance traveled. This is formally known as the <b>Traveling Salesperson Problem (TSP)</b>. 

In another words, <b>Travelling salesman problem (TSP)</b> Try to solve this question: </p>

> Given a set of cities and the distances between each pair of cities, what is the shortest possible tour that visits each city exactly once, and returns to the starting city?

<p style='text-align: justify;'>
This problem can easily become more complicated when you add in a set of vehicles or people visiting destinations instead of a single vehicle or person in the TSP problem. This is known as a <b>Vehicle Routing Problem (VRP)</b>. 

To solve this problem, you must find the optimal routes for a set of vehicles to traverse to visit a given set of customers. Additional complexity can be added to this problem class in instances where the vehicles have a set capacity that can be loaded into them. This is known as a <b>Capacitated Vehicle Routing Problem (CVRP)</b>.
</p>

<img src="/assets/images/geospatial/tsp/tsp_03.png" alt="drawing" width="500"/>


## POC Example
<p style='text-align: justify;'>
In this example we use cities of USA, you can find their location and plot below.
</p>

<img src="/assets/images/geospatial/tsp/tsp_07.png" alt="drawing" width="500"/>

<p style='text-align: justify;'>
On this result, we use Euclidean distance to make calculation faster. After we applied TSP to our dataset, we can found the shortest route was 229,8. You can find the result in number at table below or in plot result on the right. As comparison, we provide another result from randal olson.</p>

<img src="/assets/images/geospatial/tsp/tsp_02.png" alt="drawing" width="500"/>


## Schema
<img src="/assets/images/geospatial/tsp/tsp_09.png" alt="drawing" width="500"/>


## Get the distances for each locations
There are several method to get the distances for each locations. I.e.:

- Openstreetmap.org (OSM)
is a digital map database of the world built through crowdsourced volunteered geographic information (VGI). **it is means free but not accurate**. You can read usage policy OSM [here](http://wiki.openstreetmap.org/wiki/Tile_usage_policy).

- Google Maps Platform
is a web mapping platform and consumer application offered by Google. We need billing to access their API. **It is means reliable but costly**.

For this project we use OSM to proving our method. we can use combination of distance and other values as long as the goal is align with TSP which is to minimization value (to be specific for TSP is minimization distance value).

<img src="/assets/images/geospatial/tsp/tsp_10.png" alt="drawing" width="300"/>


## Finding the shortest route
There are several methods that we can use to find the shortest route in TSP. Although All of them can’t to be the best method due to TSP is NP-hard, but we can use approximation method such as:
- OR optimization
- Genetic algorithm

Both of them have advantages and disadvantages. Because these methods were approximation, there is no guarantee that the resulting model is the best model.

The input of this model is distance matrix that contain distances from and to every locations.

<img src="/assets/images/geospatial/tsp/tsp_11.png" alt="drawing" width="300"/>


## Example with our data
For this example we take the data at jember point.

<img src="/assets/images/geospatial/tsp/tsp_12.png" alt="drawing" width="300"/>


## The Result
In this result we use OSM as distance measurement and OR optimization to calculate shortest distance.

We found that if we start from jember point office at 0, we can go to user 4, user 8 and so on, to get shortest distance (80.54 km) to visit all user in jember area and back to jember point again.

The route start from 0,4,8, and so on, where number base on index column from previous slide.

<img src="/assets/images/geospatial/tsp/tsp_13.png" alt="drawing" width="1000"/>

### Find more interactive map in HTML here [link](https://drive.google.com/file/d/1k1B-CQh-KaVTcK8JX5ybk-J_Gutw8kkY/view?usp=sharing)

Number in this map base on suggest visiting order i.e. from jember point at blue marker, we go to 2,3,4, and so on. There is user information (using tooltip) if you open HTML file above.
<img src="/assets/images/geospatial/tsp/tsp_14.png" alt="drawing" width="1000"/>


## Some challenges to implement this method
- **Completeness of the data and how to collect them**
- **TSP is NP-Hard***
    - There are several models to solve this problem (all of them fail to become the best solution so far)
    - Trade-off between shortest path and time complexity
- **Is it like trying to herd cats?** - (if we want to implement this, is there any impact to our business?)

### what is TSP is NP-Hard*?
The simplest method to solve TSP problem (so far) is Permutation. All the paths are **permutations** of the set of all points / cities. The total time required for n cities should be roughly proportional to n!. This means that the time grows rapidly with the number of cities. **Really rapidly!**

But we can use **approximation methods** to get shorter computation time with slightly low in accuracy.

<img src="/assets/images/geospatial/tsp/tsp_04.png" alt="drawing" width="300"/>

## Some solutions for these problems
- **Completeness of the data and how to collect them**
    - Collect location data right now (i.e. by GPS apps, Implement GPS measurement on sales team apps).
    - make location data as mandatory field in the registration form.
- **TSP is NP-Hard**
    - Use approximation methods to overcome this issue.
    - Breakdown the big chunk problem into few simpler problems. (I.e. create a smaller visiting area to get higher efficiency from our model)
- **Is it like trying to herd cats?** 
    - Is field team really need this guidance to visiting our users?
    - Will sales team use this guidance clearly?
	    Why this matter? Because it is important to measuring how much improvement that we will make with this method.

<img src="/assets/images/geospatial/tsp/tsp_05.png" alt="drawing" width="300"/>
