---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Unsupervised Classification - ISO Cluster
nav_order: 13
parent: ArcGIS Pro
permalink: /ArcGIS/isocluster
---

# Unsupervised Classification - ISO Cluster
arcgispro
{: .badge .badge-pill .badge-primary }
geospatial
{: .badge .badge-pill .badge-primary }
map
{: .badge .badge-pill .badge-secondary }
esri
{: .badge .badge-pill .badge-info }

<img src="/assets/images/esri/iso_cluster_04.webp" alt="drawing" width="500"/>

Image classification is a process that sorts individual pixels based on their spectral values into informational classes or categories. A pixel is assigned to a class corresponding to a specific set of criteria. Two methods to classify individual pixels are:

- Unsupervised Classification
- Supervised Classification

With unsupervised classification, the pixels are clustered together based on spectral homogeneity and spectral distance. Spectral distance is measured using various techniques. 

Unsupervised classification produces classes of homogeneous spectral identities that may not exactly correspond to informational classes. While spectral classes denote pixels grouped by uniform brightness values, informational classes refer to groups that convey useful information with designations such as land use, soil classes, or agricultural productivity. 

When using unsupervised classification, the informational class may contain a variety of spectral identities. Therefore, a spectral class identified by unsupervised classification seldom matches exactly to an informational class.

In this project we will apply unsupervised classification using ISO Cluster. ISO is an algorithm in which a mean is derived from the spectral values for the input bands. Variance and co-variance are also calculated. The algorithm automatically recalculates the statistical values as pixels are added to each spectral class. 


## Study case scenario

We would like to classified landcover from sentinel 2. We breakdown the objective as follow:
- Complete an unsupervised classification on a Landsat 9 image.
- Determine the land use/landcover category associated with each spectral class.
- Create color-coded informational classes according to the following scheme:

|  Class Number  |   Information Class |   Color designation |
|:---:|:-----------:|:---------:|
|  1 | Urban/built-up/transportation|  Red |
|  2 | Mixed agriculture | Yellow |
|  3 | Forest & Wetland |  Green |
|  4 | Open water | Blue |

- Calculate the percentage of the total area for each informational class.


## The Dataset

For this purpose we use Landsat 9 image from [Earth Explorer]( https://earthexplorer.usgs.gov/). We will use this tile `LC08_L1TP_017034_20160614_20200906_02_T1_B5` that contains information about this tile such as it's `WRS path`, `WRS row`, time acquisition, etc. For more details for how to access and get this image we can see [this page](https://imanursar.github.io/scraping%20geo%20data/remote_sensing).

<img src="/assets/images/esri/iso_cluster_01.webp" alt="drawing"/>


## ISO Cluster Process

ArcGIS Pro provides multiple ways to complete the unsupervised classifications. Two methods are to use: 
- The Classification Wizard from the Imagery tab on the ribbon. 
- Using geo-processing toolbox such as ISO Cluster Unsupervised Classification.

For this time, we will focus on ISO Cluster Unsupervised Classification.

<img src="/assets/images/esri/iso_cluster_03.webp" alt="drawing"/>

To utilize `ISO Cluster Unsupervised Classification` tool at geo-processing toolbox, we will set parameters as follow:
- input raster bands = raster file
- Number of classes = number of classes for Unsupervised Classification.

## Determining the Number of Classes

We can set numerous value for this number of classes. The image has over 65,000 different pixel values. Each category of features or informational classes—water, agriculture, urban, forest—may consist of a range of spectral values. Unsupervised classification generates groups of pixels that form homogenous spectral identities. 

The number of spectral classes used will depend on the number of informational classes, the complexity of the area of interest, employer or government requirements, and the goals of the analysis. Determining the appropriate number of spectral classes may require running the ISO Cluster Unsupervised Classification tool multiple times using different numbers of spectral classes.

A new layer appears in Contents, with its image in the map viewer. Because the number of classes was set to 25 clusters of spectral values, there are 25 unique values in the symbology. Colors have been randomly assigned to the new image of homogenous spectral classes (not informational classes).

<img src="/assets/images/esri/iso_cluster_02.webp" alt="drawing"/>


## Classifying the Unsupervised Clusters

Now we need to decide which informational class contains each spectral class. Which classified image will we use? From here on, we will use the image with 25 spectral classes strictly for simplicity and instruction.

To give more information, we can change base map layer into more imagery to help us to decide which spectral classes belong to a particular information class.

For our first step, please change the color for any spectral class that has any of our final informational color classes (red, yellow, green, blue) to any other color. To change the spectral class color, start with water. Water is symbolized as blue, so zoom in to water body (Lake, river, etc) to determine the pixel value and color.

<img src="/assets/images/esri/iso_cluster_04.webp" alt="drawing"/>

Zoom to the rivers in the areas and change their colors to the same blue if they still need to be changed. But be careful since we only have 25 spectral classes—mountain shadows and cloud shadows can mimic water.

Associate agriculture fields with yellow.

<img src="/assets/images/esri/iso_cluster_07.webp" alt="drawing"/>

Associate forests with green.

<img src="/assets/images/esri/iso_cluster_06.webp" alt="drawing"/>

Urban areas should be red.

<img src="/assets/images/esri/iso_cluster_05.webp" alt="drawing"/>

Using unsupervised classification with this image, was it easy to identify clouds? For purposes of this project, clouds were placed into their own class. How about cloud shadows? What were cloud shadows classified? Again, increasing the number of spectral clusters would have enabled us to provide more definitive land cover class assignments.

After assigning all 25 spectral classes, look at the overall image (Figure 21.24). Are the informational classes generally correct? Do we have any blue areas within the mountains that are not water? Urban classes, that are in the water? For our image, the answer is yes to all of these questions, which again tells us that 25 spectral clusters were insufficient to separate all of the spectral clusters so we could categorize them into information classes.

<img src="/assets/images/esri/iso_cluster_08.webp" alt="drawing"/>

<img src="/assets/images/esri/iso_cluster_09.webp" alt="drawing"/>

We are not yet finished because, in Contents, the symbology lists 25 spectral values but only four colors that pertain to our informational classes (five colors if we have included a separate class for clouds).


## Reclassifying Spectral Classes into Informational Classes

The 25 spectral classes have been assigned the colors of the four informational classes. To change this to four informational classes, we utilize `Reclassify` tool from Geoprocessing toolbox.

<img src="/assets/images/esri/iso_cluster_10.webp" alt="drawing"/>

After Reclassifying, we must assign the correct colors by using `symbology` and change the color scheme. The two images, the spectral class image with the 25 values and the informational class image with four values, should look the same if the Reclass process was completed correctly.


## Calculating the Percent of Total Area for Each Informational Class

Once the pixels have been reclassified into four classes, the percentage of the total area for each class can be easily calculated. The percentage of the total area for each informational class can be calculated within the Attribute Table. 

We first need to know how many pixels are in the entire image to calculate the percentage for each informational class. Since we only have four categories (actually five categories including clouds), add them together (answer = 60.073.101). Is this correct? Check the number of rows and columns under Properties (7681 x 7621 = 60.073.101).

To calculate the value for the field, right-click the new field in the attribute table and select Calculate Field, enter the expression under Percent= exactly as follows

> (!Count! / 60073101) * 100

<img src="/assets/images/esri/iso_cluster_11.webp" alt="drawing"/>

The new field now shows the percentage of the total for each informational class

<img src="/assets/images/esri/iso_cluster_12.webp" alt="drawing"/>


## Additional information
Before we finish up, let's discuss one option under the ISO Cluster Unsupervised Classification Geoprocessing tool that we did not use—Output signature file.

<img src="/assets/images/esri/iso_cluster_13.webp" alt="drawing"/>

We did not create this during our geoprocessing operation. Entering a name here and saving a signature file generates multivariate statistics for each cluster. The signature file can be read using any text editor, such as Microsoft Notepad. The statistics generated are related to the spectral values, not the informational categories. They can be used to evaluate co-variance between any of the bands within our multispectral image. 

