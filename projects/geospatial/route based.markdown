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

<img src="/assets/images/geospatial/tsp/tsp_01.png" alt="drawing" width="500"/>

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

<img src="/assets/images/geospatial/tsp/tsp_03.png" alt="drawing"/>


## POC Example
<p style='text-align: justify;'>
In this example we use cities of USA, you can find their location and plot below.
</p>
<img src="/assets/images/geospatial/tsp/tsp_06.png" alt="drawing" width="500"/>

<p style='text-align: justify;'>
On this result, we use Euclidean distance to make calculation faster. After we applied TSP to our dataset, we can found the shortest route was 229,8. You can find the result in number at table below or in plot result on the right. As comparison, we provide another result from randal olson.</p>
<img src="/assets/images/geospatial/tsp/tsp_07.png" alt="drawing" width="500"/>

### Final result
<img src="/assets/images/geospatial/tsp/tsp_02.png" alt="drawing"/>


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

## Some solution for these problems
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
