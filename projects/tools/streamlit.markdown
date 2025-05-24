---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Streamlit 101
parent: Tools
permalink: /tools/streamlit
nav_order: 1
---

# Streamlit 101

tools
{: .badge .badge-pill .badge-primary }
simulation
{: .badge .badge-pill .badge-secondary }
streamlit
{: .badge .badge-pill .badge-info }

The Faster You Can Iterate, The Faster You Can Learn
<img src="/assets/images/tools/streamlit_07.webp" alt="drawing"/>

## Introduction
<p style='text-align: justify;'>
we’ve embraced Streamlit as a powerful tool to bring data to life. Whether it’s showcasing results, running proofs of concept (POCs), or conducting internal simulations, Streamlit has become an integral part of how we transform raw data into actionable insights.

With its user-friendly interface and interactive capabilities, Streamlit allows us to present complex analyses in a way that’s clear, engaging, and easy for stakeholders to understand. From visualizing trends to running dynamic models, it helps decision-makers dive deeper into the numbers and make informed choices with confidence.

This page explores how we’ve implemented Streamlit across various projects, highlighting its role in driving better insights and smarter decisions within our organization.</p>


## Common workflow
The development workflow for data projects often followed a common, linear path:

- Data: Collecting and preparing data from various sources, cleaning it up, and organizing it into a usable format.
- Visualization: converting the data into meaningful insight.
- Process: Running scripts or notebooks to transform, analyze, or preprocess the data for modeling.
- Model: Developing machine learning models or running simulations to generate insights.
- Product: Finally, packaging the results into dashboards, presentations, or reports for stakeholders.

<img src="/assets/images/tools/streamlit_01.webp" alt="drawing" width="500"/>

While this workflow seems straightforward, it often led to two major challenges:

### The Unmaintainability Trap
As the project evolves, keeping the scripts and notebooks organized becomes increasingly difficult. Small tweaks to the code or data require significant time and effort to re-run processes and validate outputs. Without a clear structure, the workflow can become fragile, with each layer dependent on manual intervention. This makes it hard to scale or revisit old projects without confusion and frustration.

<img src="/assets/images/tools/streamlit_02.webp" alt="drawing" width="500"/>

### The Frozen Zone
In traditional workflows, once insights or models are delivered, they often get "frozen" into static reports or dashboards. This leaves little room for experimentation or real-time interaction, making it challenging for stakeholders to ask "what if" questions or explore the data beyond what was initially provided. This rigidity can stifle collaboration and prevent deeper insights from emerging.

<img src="/assets/images/tools/streamlit_03.webp" alt="drawing" width="500"/>

Streamlit disrupts this cycle by providing an interactive and dynamic platform where you can combine the steps into a seamless, iterative process. It bridges the gap between static workflows and real-time decision-making, allowing developers and stakeholders to collaborate, explore, and experiment without getting stuck in the traps of unmaintainability and frozen outputs.

## Streamlit come to the rescue
> What if we could make building tools as easy as writing python scripts?
> **This is the spirit of streamlit**

Imagine if building powerful, interactive tools was as simple as writing a Python script. No complicated frameworks, no steep learning curves, and no need to be a front-end expert. That’s exactly the problem Streamlit solves—it takes the complexity out of turning data and ideas into real, interactive applications.

With Streamlit, you don’t need to worry about designing interfaces or managing countless dependencies. Instead, you focus on what matters most: your data and insights. In just a few lines of Python, you can create fully functional apps that bring your analysis to life, allowing users to interact with data, tweak parameters, and visualize results in real-time.

This is the spirit of Streamlit: simplicity, flexibility, and speed. It’s not just a tool; it’s a bridge between data scientists, developers, and decision-makers. Whether you’re running a proof of concept, simulating scenarios, or sharing insights with stakeholders, Streamlit empowers you to build and share solutions faster than ever before.

Gone are the days of static notebooks and endless PowerPoint slides. With Streamlit, you can deliver apps that spark collaboration, inspire better decisions, and drive real impact—all with the ease of writing Python. It’s data science, reimagined.

<img src="/assets/images/tools/streamlit_04.webp" alt="drawing" width="500"/>
<img src="/assets/images/tools/streamlit_05.webp" alt="drawing" width="500"/>

## Streamlit’s Three Core Principles
Streamlit is built on three guiding principles that make it a powerful yet simple tool for creating interactive apps. Here’s a closer look at how these principles work:

1. **Embrace Python Scripting**
    Streamlit eliminates the need for complex configurations or learning new languages by allowing you to build apps using pure Python.

    - Simple: If you can write a Python script, you can create a Streamlit app. No web development experience is required.
    - Intuitive: Everything feels natural. Functions and commands are designed to fit seamlessly into your existing Python workflow, letting you focus on building instead of troubleshooting.
_

2. **Treat Widgets as Variables**
    Widgets in Streamlit are designed to be as simple to use as Python variables, making your code cleaner and more readable.

    - Declare Widgets as Easily as Variables: You can declare a widget like a slider, button, or text input in one line, and Streamlit automatically manages its state.
_

3. **Reuse Data and Computation**
    Streamlit optimizes your app’s performance with a built-in caching mechanism. This allows you to reuse data and computations without re-running expensive operations every time the app updates.

    - Cache Mechanism: Simply use the @st.cache_data or @st.cache_resource decorator to store the results of a function. This ensures faster app performance and avoids redundant processing.

## Why These Principles Matter
Streamlit’s simplicity, intuitive widget handling, and caching system create an environment where building tools is fast, flexible, and fun. These principles empower you to focus on insights and creativity, rather than getting bogged down by technical hurdles. It’s development done smarter, not harder.

## Getting started with Streamlit

<img src="/assets/images/tools/streamlit_06.webp" alt="drawing"/>