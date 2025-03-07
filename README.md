# pysal_snow_cholera

Spatial Analysis using the Pysal Library: Student-Led Tutorial

Chanmi Lee, Michael Gutnajer, and Kelley Simon

GUS 5031: GIS Programming 

April 2021

## PySAL Library

The PySAL library is a spatial analysis library composed of multiple packages. Its applications range from data visualization and statistical analysis to modeling spatial relationships in data.

This project focuses on the data visualization module, one of the 22 packages within PySAL. Specifically, it demonstrates PySAL’s capability for the following:

(1) Global and Local Moran's I

(2) Standard Distance Circle and Stadard Deviational Ellipse

(3) Kernel Density Estimation

## Dr. John Snow and 1854 Broad Street cholera outbreak

This project investigates the monumental 19th-century spatial epidemiology case using Python’s PySAL library, retracing the steps Dr. John Snow might have taken to identify the cholera death cluster near the Broad Street water pump.

While running this analysis, it may seem obvious to us in the 21st century that cholera deaths were clustered around the Broad Street water pump. However, in the 19th century, spatially linking disease events to a potential source was groundbreaking. Dr. Snow’s investigation ultimately led the local council to recognize the Broad Street pump as the source of the outbreak and remove its handle to prevent further spread of the disease.

![220px-Barker--John_Snow--1847](https://github.com/user-attachments/assets/226d8455-3295-4eb8-a1f9-e5e75c9c4438)

Dr. John Snow

![300px-Snow-cholera-map-1](https://github.com/user-attachments/assets/2e546f37-96c5-46b7-98da-6a26cf778f10)

Clusters of cholera deaths

Data source: https://blog.rtwilson.com/john-snows-famous-cholera-analysis-data-in-modern-gis-formats/ (download no longer available)

## Project Aim

This project revisits this 19th-century case using the PySAL library to investigate its spatial patterns and demonstrate its applicability to the spatial analysis of other epidemiological cases.

## Global and Local Moran's I

Global Moran's I is a measure of spatial autocorrelation that evaluates the relationship between a variable and its neighboring locations. It determines whether clustering exists within the study area, which is the primary purpose of using Global Moran's I in this analysis. The term 'global' refers to the fact that this measure provides a single statistic summarizing spatial patterns across the entire study area. 

It is a form of multi-dimensional and multi-directional autocorrelation measurement in which the distance between the signal and nearby locations is measured through the use of weights of “neighbors” these can be given a weight of 1 for the nearest neighbor as opposed to 0 for a far away neighbor.

Local Moran's I, in contrast, differs from Global Moran's I by providing a unique statistic for each location (i), rather than a single value for the entire area. Each location receives its own Moran’s I value and corresponding variance (z-score), allowing for the identification of localized clusters. Local Moran’s I measures how much an individual observation deviates from the mean and how this deviation interacts with the deviations of its neighboring locations.

![Global_Moran](https://github.com/user-attachments/assets/1b467fbe-02f9-4b80-8923-1f2ae63ff5f7)

Global Moran's I

![Local_Moran](https://github.com/user-attachments/assets/2464b69f-a875-4346-9cdb-695173512107)

Local Moran's I

As seen in this scatterplot, there is a noticeable clustering around the spatial lag values between 0 and 1.

## Standard Distance Circle and Stadard Deviational Ellipse

The standard distance circle is a useful statistic for summarizing the spatial distribution of features around the dataset's mean center. It provides a visual indication of dispersion. Additionally, we utilize the standard deviational ellipse tool from PySAL's pointpats module.

![Standard_Distance](https://github.com/user-attachments/assets/7de864b1-d940-4fea-8a5c-4ac7ffd49b2c)\

This plot suggests strong evidence that the water pump located near the mean center may be linked to the surrounding cholera deaths. It also reveals a slight directional trend extending toward the northeast and southwest.

The standard deviational ellipse is a method for identifying spatial trends by displaying the orientation and distribution of data. When the ellipse is elongated, it indicates a directional pattern, suggesting that the data is spatially skewed.

![std_ellipse](https://github.com/user-attachments/assets/8f51e89f-9d3a-4668-9154-306e5d820b12)

The relationship between the pump location and cholera deaths suggests that the Broad Street pump was central to the outbreak. Its proximity to the mean center further reinforces the idea that the surrounding cholera deaths form a structured spatial pattern, aligning closely with the street network around the pump.

## Kernel Density Estimation

Kernel Density Estimation (KDE) is a method for estimating probability density, allowing inferences about a population based on data samples. At each point of interest, kernel functions are applied across a grid of points. The density at a given location is computed by weighting nearby points based on their distance from the target location. The result is a continuous surface representing the probability distribution, highlighting areas of higher concentration.

![Figure 2021-04-06 204702](https://github.com/user-attachments/assets/6d90f847-a7df-43ee-8a58-e85dd3cc6d94)

This KDE analysis reveals a concentration of cholera cases around the Broad Street water pump, consistent with previous findings. It visually reinforces the impact of the pump's location on the spatial distribution of cholera deaths in the neighborhood.
