---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Geospatial
nav_order: 2
has_children: true
heading_anchors: true
permalink: /geospatial/
has_toc: false
---

# DS Portfolio

Portfolio of my data science projects for course assignment and personal purposes.

## Attitudes Toward Wife Beating
logistic regression
{: .badge .badge-pill .badge-primary }
statistical test
{: .badge .badge-pill .badge-secondary }
EDA
{: .badge .badge-pill .badge-info }

Melihat bagaimana hubungan tingkat pendidikan, tingkat ekonomi, daerah tinggal, serta pernikahan di bawah umur perempuan mempengaruhi sikap terhadap pemukulan istri dan apakah hubungan tersebut dapat digambarkan oleh sebuah model statistik. Dibuat sebagai final project salah satu course Pacmann Analytics & Data Science.

<img src="/portfolio/static/wifebeating/poorest_vs_richest_household_vs_beatings.png" alt="drawing" width="500"/>

<span class="fs-3">
[Read more](/portfolio/wife beating){: .btn }
</span>


## Health Insurance Risk Analysis
probability
{: .badge .badge-pill .badge-primary }
EDA
{: .badge .badge-pill .badge-secondary }

Analisis variabel yang mempengaruhi tagihan asuransi kesehatan. Dibuat sebagai final project salah satu course Pacmann Analytics & Data Science.

<img src="/portfolio/static/healthinsurance/Untitled 18.png" alt="drawing" width="300"/>

<span class="fs-3">
[Read more](/portfolio/health insurance risk){: .btn }
</span>


## NY Citi Bike Performance
data viz
{: .badge .badge-pill .badge-primary }
data cleaning
{: .badge .badge-pill .badge-secondary }
EDA
{: .badge .badge-pill .badge-info }

Analisis kinerja program NY Citi Bike di tahun 2014-2016 serta eksplorasi karakteristik pengguna. Visualisasi ditampilkan dalam bentuk dashboard Tableau. Dibuat sebagai final project salah satu course Pacmann Analytics & Data Science.

<img src="/portfolio/static/nycitibike/Untitled 3.png" alt="drawing" width="500"/>

<span class="fs-3">
[Read more](/portfolio/citi bike performance){: .btn }
</span>


## NYC311 Housing and Building Complaint Analysis

data viz
{: .badge .badge-pill .badge-primary }
data cleaning
{: .badge .badge-pill .badge-secondary }
scikit-learn
{: .badge .badge-pill .badge-primary} 
decision tree
{: .badge .badge-pill .badge-info }
flask
{: .badge .badge-pill .badge-secondary }
plotly
{: .badge .badge-pill .badge-secondary }

An analysis of complaints received by NYC Department of Housing Preservation and Development (HPD) to help manage the high-volume of complaints by suggesting the most pressing complaint as well as the area the HPD should focus on. A final project for Purwadhika Data Science and Machine Learning.

![](/portfolio/static/prediction.png)

<span class="fs-3">
[Read more](/portfolio/nyc311){: .btn }
</span>


### Links
- Flask web application is available on [Heroku](http://nyc311-azka.herokuapp.com/)
- Notebooks and source code are available on [my github](https://github.com/azukacchi/nyc311_housing_buildings_analysis).


## Campus Recruitment

EDA
{: .badge .badge-pill .badge-primary }
data viz
{: .badge .badge-pill .badge-secondary }

Analysis of academic and employability factors influencing candidate's job placement. A Project for IBM Exploratory Data Analysis for Machine Learning course.

<img src="/portfolio/static/campusrec.png" alt="Campus Recruitment" width="300"/>

<span class="fs-3">
[Read more](/portfolio/campus recruitment){: .btn }
</span>


## House Price Prediction

regression
{: .badge .badge-pill .badge-primary }
property
{: .badge .badge-pill .badge-secondary }

Predict house price based on physical attributes related to property sales with linear regression. Different methods of regularization such as Ridge, Lasso, and Elastic Net were evaluated. This is a project for IBM Supervised Learning: Regression course.

<img src="/portfolio/static/housing.png" alt="House Price Prediction" width="300"/>

<span class="fs-3">
[Read more](/portfolio/house price){: .btn }
</span>

## Browsing or Purchasing?

clasification
{: .badge .badge-pill .badge-primary }
decision tree
{: .badge .badge-pill .badge-info }
retail
{: .badge .badge-pill .badge-secondary }

Predict whether a customer browsing session will end with goods purchase or not based online shop customer's browsing behavior in one year period. A Project for IBM Supervised Learning: Classification course.

![](/portfolio/static/purchasing.png)

<span class="fs-3">
[Read more](/portfolio/purchasing intention){: .btn }
</span>


## Online Retail Customer Segmentation

clustering
{: .badge .badge-pill .badge-primary }
kmeans
{: .badge .badge-pill .badge-info }
agglomerative clustering
{: .badge .badge-pill .badge-info }
retail
{: .badge .badge-pill .badge-secondary }

How should a retailer make an offering to their customer? What does the transaction data tell about the customers' purchasing behavior? We will group online retailer customers using clustering techniques, with the help of Recency, Frequency, and Monetary (RFM) analysis. A Project for IBM Unsupervised Learning course.

![](/portfolio/static/kmeans.png)

<span class="fs-3">
[Read more](/portfolio/customer segmentation){: .btn }
</span>

## The Most Impactful Attack On Titan Episodes in Each Season

EDA
{: .badge .badge-pill .badge-primary }
google trends
{: .badge .badge-pill .badge-secondary }
pytrends
{: .badge .badge-pill .badge-info }
fandom stuffs
{: .badge .badge-pill .badge-primary }

Which of the Attack On Titan season has the most impact? Which episodes garnered the most attention in each season? We'll answer both questions using the data from Google Trends.

![](/portfolio/static/merch.jpg)

<span class="fs-3">
[Read more](/portfolio/AttackOnTitan - google trends){: .btn }
</span>


---

# Others

Portfolio of my other projects in Python.

## Twitter Autobase Bot

tweepy
{: .badge .badge-pill .badge-primary }
API
{: .badge .badge-pill .badge-info }
fandom stuffs
{: .badge .badge-pill .badge-secondary }

Simple twitter autobase bot that posts incoming Direct Messages.

### Features

- Posts incoming DM that contains the trigger word.
- Posts incoming DM with media.
- Cuts post longer than 280 characters and posts them as a thread. 
- Sends a DM back for each incoming DM.
- Deletes the incoming DMs once they are posted.

<span class="fs-3">
[Read more](/portfolio/autobase){: .btn }
</span>

### Links
- Source code on [my github](https://github.com/azukacchi/twitter_autobase)
- Tutorial on [my Dev page](https://dev.to/azukacchi/making-a-simple-twitter-autobase-bot-that-posts-incoming-dm-1lmo)

## Twitter RT Bot

tweepy
{: .badge .badge-pill .badge-primary }
API
{: .badge .badge-pill .badge-info }
sqlite
{: .badge .badge-pill .badge-secondary }
fandom stuffs
{: .badge .badge-pill .badge-info }

This is a simple twitter bot that collects tweets containing a certain keyword, stores them in a database file, and retweets them at a certain time window, built in Python using Tweepy.

<span class="fs-3">
[Read more](/portfolio/RT bot){: .btn }
</span>

### Links
- Source code on [my github](https://github.com/azukacchi/DKMKbot)