# IBM
IBM projects
cognitiveclass.ai logo
Generating Maps with Python
Estimated time needed: 30 minutes

Objectives
After completing this lab you will be able to:

Visualize geospatial data with Folium
Introduction
In this lab, we will learn how to create maps for different objectives. To do that, we will part ways with Matplotlib and work with another Python visualization library, namely Folium. What is nice about Folium is that it was developed for the sole purpose of visualizing geospatial data. While other libraries are available to visualize geospatial data, such as plotly, they might have a cap on how many API calls you can make within a defined time frame. Folium, on the other hand, is completely free.

Table of Contents
Exploring Datasets with pandas
Downloading and Prepping Data
Introduction to Folium
Map with Markers
Choropleth Maps
Exploring Datasets with pandas and Matplotlib
Toolkits: This lab heavily relies on pandas and Numpy for data wrangling, analysis, and visualization. The primary plotting library we will explore in this lab is Folium.

Datasets:

San Francisco Police Department Incidents for the year 2016 - Police Department Incidents from San Francisco public data portal. Incidents derived from San Francisco Police Department (SFPD) Crime Incident Reporting system. Updated daily, showing data for the entire year of 2016. Address and location has been anonymized by moving to mid-block or to an intersection.

Immigration to Canada from 1980 to 2013 - International migration flows to and from selected countries - The 2015 revision from United Nation's website. The dataset contains annual data on the flows of international migrants as recorded by the countries of destination. The data presents both inflows and outflows according to the place of birth, citizenship or place of previous / next residence both for foreigners and nationals. For this lesson, we will focus on the Canadian Immigration data

Downloading and Prepping Data 
Import Primary Modules:

import numpy as np  # useful for many scientific computing in Python
import pandas as pd # primary data structure library
Introduction to Folium 
Folium is a powerful Python library that helps you create several types of Leaflet maps. The fact that the Folium results are interactive makes this library very useful for dashboard building.

From the official Folium documentation page:

Folium builds on the data wrangling strengths of the Python ecosystem and the mapping strengths of the Leaflet.js library. Manipulate your data in Python, then visualize it in on a Leaflet map via Folium.

Folium makes it easy to visualize data that's been manipulated in Python on an interactive Leaflet map. It enables both the binding of data to a map for choropleth visualizations as well as passing Vincent/Vega visualizations as markers on the map.

The library has a number of built-in tilesets from OpenStreetMap, Mapbox, and Stamen, and supports custom tilesets with Mapbox or Cloudmade API keys. Folium supports both GeoJSON and TopoJSON overlays, as well as the binding of data to those overlays to create choropleth maps with color-brewer color schemes.

Let's install Folium
Folium is not available by default. So, we first need to install it before we are able to import it.

!conda install -c conda-forge folium=0.5.0 --yes
import folium
​
print('Folium installed and imported!')
Collecting package metadata (current_repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Collecting package metadata (repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/jupyterlab/conda/envs/python

  added / updated specs:
    - folium=0.5.0


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    altair-4.1.0               |             py_1         614 KB  conda-forge
    attrs-21.2.0               |     pyhd8ed1ab_0          44 KB  conda-forge
    branca-0.4.2               |     pyhd8ed1ab_0          26 KB  conda-forge
    entrypoints-0.3            |  pyhd8ed1ab_1003           8 KB  conda-forge
    folium-0.5.0               |             py_0          45 KB  conda-forge
    jsonschema-3.2.0           |     pyhd8ed1ab_3          45 KB  conda-forge
    pyrsistent-0.17.3          |   py36h8f6f2f9_2          89 KB  conda-forge
    vincent-0.4.4              |             py_1          28 KB  conda-forge
    ------------------------------------------------------------
                                           Total:         900 KB

The following NEW packages will be INSTALLED:

  altair             conda-forge/noarch::altair-4.1.0-py_1
  attrs              conda-forge/noarch::attrs-21.2.0-pyhd8ed1ab_0
  branca             conda-forge/noarch::branca-0.4.2-pyhd8ed1ab_0
  entrypoints        conda-forge/noarch::entrypoints-0.3-pyhd8ed1ab_1003
  folium             conda-forge/noarch::folium-0.5.0-py_0
  jsonschema         conda-forge/noarch::jsonschema-3.2.0-pyhd8ed1ab_3
  pyrsistent         conda-forge/linux-64::pyrsistent-0.17.3-py36h8f6f2f9_2
  vincent            conda-forge/noarch::vincent-0.4.4-py_1



Downloading and Extracting Packages
pyrsistent-0.17.3    | 89 KB     | ##################################### | 100% 
folium-0.5.0         | 45 KB     | ##################################### | 100% 
branca-0.4.2         | 26 KB     | ##################################### | 100% 
altair-4.1.0         | 614 KB    | ##################################### | 100% 
attrs-21.2.0         | 44 KB     | ##################################### | 100% 
jsonschema-3.2.0     | 45 KB     | ##################################### | 100% 
entrypoints-0.3      | 8 KB      | ##################################### | 100% 
vincent-0.4.4        | 28 KB     | ##################################### | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
Folium installed and imported!
Generating the world map is straightforward in Folium. You simply create a Folium Map object, and then you display it. What is attractive about Folium maps is that they are interactive, so you can zoom into any region of interest despite the initial zoom level.

# define the world map
world_map = folium.Map()
​
# display world map
world_map
Make this Notebook Trusted to load map: File -> Trust Notebook
Go ahead. Try zooming in and out of the rendered map above.

You can customize this default definition of the world map by specifying the centre of your map, and the initial zoom level.

All locations on a map are defined by their respective Latitude and Longitude values. So you can create a map and pass in a center of Latitude and Longitude values of [0, 0].

For a defined center, you can also define the initial zoom level into that location when the map is rendered. The higher the zoom level the more the map is zoomed into the center.

Let's create a map centered around Canada and play with the zoom level to see how it affects the rendered map.

# define the world map centered around Canada with a low zoom level
world_map = folium.Map(location=[56.130, -106.35], zoom_start=4)
​
# display world map
world_map
Make this Notebook Trusted to load map: File -> Trust Notebook
Let's create the map again with a higher zoom level.

# define the world map centered around Canada with a higher zoom level
world_map = folium.Map(location=[56.130, -106.35], zoom_start=8)
​
# display world map
world_map
Make this Notebook Trusted to load map: File -> Trust Notebook
