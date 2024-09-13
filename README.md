CSC 381 Programming and Data Analysis with R - Assignment 

Repository Overview

This repository contains the R programming assignment for the CSC 381 course. The objective of this assignment was to analyze various data points for Lithuania using R and derive insights through data visualization and statistical analysis. The dataset used comes from the R coronavirus package.

Contents

    data/: Contains the dataset used for analysis.
    scripts/: R scripts used for data cleaning, analysis, and visualization.
    output/: Plots and visualizations generated during the analysis.

R packages:

    coronavirus
    tidyverse
    skimr
    magrittr
    gridExtra
    plotly
    leaflet

Data Description

The data used for this analysis includes the following fields:

    date: Date of the observation
    country: Country name
    type: Type of case (confirmed, recovered, death)
    cases: Number of cases recorded
    lat and long: Latitude and longitude of the country

Key Features

    Visualizations:
        Time series plots of COVID-19 confirmed, active, recovered, and death cases.
        Cumulative active and death cases for Lithuania and neighboring countries.
        Interactive plots using plotly for easy exploration of data.

    Mapping:
        A leaflet map showing the geographic location of Lithuania and its neighboring countries.

    Statistical Analysis:
        Calculated statistics on COVID-19 cases in Lithuania, such as daily averages and cumulative totals.
        Percentage calculations based on population.

Insights

    Lithuania's COVID-19 Trend:
        Rapid increases and decreases in confirmed cases over the pandemic period.
        A significant spike in active cases in early 2022.

    Neighboring Countries Comparison:
        Lithuania’s confirmed cases are higher compared to other Baltic countries.
        Similar trends observed for Latvia and Estonia.

