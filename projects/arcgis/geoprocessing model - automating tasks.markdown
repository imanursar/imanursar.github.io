---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Geoprocessing Model - Automating tasks
nav_order: 5
parent: ArcGIS
permalink: /ArcGIS/automate tasks
---

# Geoprocessing Model - Automating tasks
geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
esri
{: .badge .badge-pill .badge-info }
snippet
{: .badge .badge-pill .badge-info }

<img src="/assets/images/esri/esri_28.png" alt="drawing" width="500"/>

In this project we will learn three ways for storing and automating multiple-operation workflows. Workflow definition, storage, and automation facilitate and standardize geospatial solutions. These capabilities are especially useful for organizations that anticipate performing a workflow many times.

- [Automating tasks](https://imanursar.github.io/ArcGIS/automate tasks) — This feature allows we to walk the user through a series of predefined steps that can incorporate (or call) commands and geoprocessing tools, including model and script tools. It can serve as a  best practices or a workflow tutorial—a documented series of instructions that call forth the correct commands or tools. And the tasks can be shared as part of a project, allowing users to share their knowledge.
- [ModelBuilder™](https://imanursar.github.io/ArcGIS/modelbuilder) — a geoprocessing environment that allows we to easily link one tool to another and run a set of operations one after another. ModelBuilder provides a helpful visual diagram of geoprocessing workflows and includes advanced capabilities such as looping and if-then scenarios.
- [Automate with Python](https://imanursar.github.io/ArcGIS/automate python) — We will write a command and use a custom script tool (created with Python) that performs multiple operations.

## Study case scenario
We are employed by a nonprofit agency whose primary objective is
to raise awareness of and develop solutions for international human rights violations. Taking advantage of the public information offered by the Armed Conflict Location and Event Data (ACLED) project, we are creating maps that convey the impact of political violence in developing countries. We will present our maps at an international human rights conference for eventual incorporation into an awareness campaign.


## The Dataset
The ACLED dataset we are using provides information on political violence in developing countries. Attributes include dates of conflict events, key actors involved (such as military forces, protesters, rebel groups, civilians, and others), and event classification (such as riots and protests, battles, nonviolent activities by conflict actors, violence against civilians, and more). In this project, We will focus on African continent. 

ACLED_2005_2018 — a point feature class that displays locations of armed conicts throughout Africa from 2005 to 2018 (Source: ACLED).

<img src="/assets/images/esri/esri_18.png" alt="drawing"/>


## Automating tasks

We will begin using the Tasks pane, an ArcGIS Pro feature that allows us to follow or define a workflow for ourself or other users.

Task item is a predefined series of steps, grouped into tasks, that walk us through a GIS workflow. Each task contains one or more related steps. Tasks are helpful to standardize business operations and promote best practices for a repeatable workflow.

In this part, we will use precongured tasks and modifing it for new task.

To access the tasks we can use this path, On the View tab, in the Windows group, click the Tasks button to show the Tasks pane. When the Tasks pane opens, we will see the Create Conflict Maps task item.

<img src="/assets/images/esri/esri_18_1.png" alt="drawing"/>

Each task contains some steps, with the Progress indicator at the bottom. 

<img src="/assets/images/esri/esri_19.png" alt="drawing"/>

<img src="/assets/images/esri/esri_19_1.png" alt="drawing"/>

### First task - definition query
The first task facilitates the creation of a `definition query`, which limits the display of features to features that meet user-defined criteria. This step opens the query builder, which is on the Definition Query tab of Layer Properties. The rest of the step relies on manual input, with the instructions documented in the task step.

The final result of the first task as shown below.

<img src="/assets/images/esri/esri_20.png" alt="drawing"/>

In this part, we filter our data on `Country = south sudan` and limit our windows time data for `year >= 2010`.

### Symbolize layer
This task has only one step, to change symbol to `Graduated symbol` on the `Fatalities` parameter with three classes. 

<img src="/assets/images/esri/esri_21.png" alt="drawing"/>

### Make Selection
This task also has one step. To select only those `EVENT_TYPE = Violence against Civilians`. The Select Layer by Attribute tool is embedded within the Tasks pane, with default parameters preselected.

The result of these tasks can be shown at below image.

<img src="/assets/images/esri/esri_22.png" alt="drawing"/>

The map shows conflicts in South Sudan between 2010 and 2018, symbolized with graduated symbols, so that the increasing size corresponds to a greater number of fatalities. Conflicts that have been classified as violence against civilians are selected in cyan.

### Add a new task item.
Next, we will add to an existing task item. In the Tasks pane, click Create Conflict Maps, and click the Options menu > Edit in Designer. This step opens the Task Designer. When the Task Designer is open, the Tasks pane reveals new buttons and tabs.

<img src="/assets/images/esri/esri_23_1.png" alt="drawing"/>

In the Tasks pane, click the New Task button. A new task is now visible in the Tasks pane, and the Task Designer is updated to reflect the new task. Clicking any task in the Tasks pane will bring up the same task in the Task Designer.

We can create new task namely `Generate summary statistics`. This task will Summarize the fatalities for the selected set of features.

To create a new task seamlessly, we can use `Record Commands button` to record all interaction that we done and will be translated into an automated step when we stop recording. 

In Example, after click record command button, we can go to the Analysis tab, In the Tools gallery, find and click the Summary Statistics tool. Do not fill out the tool. In the Tasks pane, click the Stop Recording button. Back in the Task Designer, for Run/Proceed Instructions, type Click Run to run geoprocessing tool. Click Finish to complete task. This will record all process above as steps for this task.

To create default parameter for our new task, we can use `Edit tool` at Task Designer. These are the default value that we can use:
- Input Table: ACLED_2010_2018_SouthSudan
- Output Table: Conflict.gdb\ACLED_SouthSudan_Statistics
- Field: FATALITIES
- Statistic Type: Sum

The result of this new task can be shown at below image.

<img src="/assets/images/esri/esri_23.png" alt="drawing"/>

Tasks provide the benefit of a built-in, how-to tutorial without needing separate documents to explain workflows. Whether they are commonly performed tasks or more obscure workflows that are performed only occasionally, storing the sequence of steps in a task item is a good way to ensure compliance and consistency.


## Result for other countries

### **Egypt**
<img src="/assets/images/esri/esri_24.png" alt="drawing"/>
<img src="/assets/images/esri/esri_25.png" alt="drawing"/>
<img src="/assets/images/esri/esri_26.png" alt="drawing"/>

### **Libya**
<img src="/assets/images/esri/esri_27.png" alt="drawing"/>

### **Rwanda**
<img src="/assets/images/esri/esri_29.png" alt="drawing"/>
<img src="/assets/images/esri/esri_28.png" alt="drawing"/>
























