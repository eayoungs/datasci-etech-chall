# Clustering Analysis

Author: Emily Chao

## Goal

Myanmar has 330 townships (and population statistics and census data for each of those townships).

The main questions I try to answer are:
- How similar are these townships to each other based on their population census data?
- How likely is this to predict or influence their ability to pay?
- Can we see trends where a township has low electrification, but is not likely to be able to pay?

## Feature Selection

From the ~200 different population and household statistics in the Myanmar census data, I narrowed down my features to a set of 24 features that are normalized to population size and / or number of households.

The features can be broken up into roughly 3 categories:
- Population Characteristics
  - % of population that lives in rural area
  - % of population between ages 0-14
  - % of population currently attending school/college
  - % of population 10yr and older in paid employment
  - % of population in institutions
  - percentile of mean household size
- Housing Characteristics
  - % HQ housing
  - % LQ housing
  - % households with access to safe sanitation
  - % households w/ electricity as source
  - % households w/ solar systems as source
  - % households w/ relatively efficient sources of lighting
  - % households w/ relatively poor sources of lighting
  - % households - cooking fuel electricity
  - % households - cooking fuel that costs natural resources
  - % households - cooking fuel that is fuel-based and requires transport
- Access to Technology
  - % availability to TV
  - % availability to mobile phone
  - % availability to radio
  - % availability to computer
  - % availability to Internet
  - % availability to car/truck/van
  - % availability to 40wheel tractor
  - % availability to motor boat

HQ housing is defined as apartment/condo, bungalow/brick, semi-pacca housing.
LQ housing is defined as wooden house, bamboo, hut 2-3 years old, hut 1-year old, other.

Relatively efficient sources of lighting is defined as battery, generator (private), water mill (private).
Relatively poor sources of lighting is defined as candle, kerosene, other.

Cooking fuel that costs natural resources is defined as firewood, charcoal, coal, straw/grass.
Cooking fuel that is fuel-based and requires transport is defined as LPG, Kerosene, BioGas.

## Process

1. Extract the features.
2. Using k-means clustering through Scikit-learn, generate 3 clusters of townships.
3. Analyze pairwise relationships between a set of 10 features we care about.
  - Total Population
  - % households w/ solar systems as source
  - % households w/ electricity as source
  - % households w/ relatively efficient sources of lighting
  - % households w/ relatively poor sources of lighting
  - % cooking fuel electricity
  - % cooking fuel that is fuel-based and requires transport
  - % cooking fuel that costs natural resources
  - % households with access to safe sanitation
  - % 10yr and older in paid employment
  - % rural

## Some Conclusions

Housing variables tend to be a better indicator than technology variables. Because the data is from 2014, mobile phone access and Internet access isn't a good indicator to base ability to pay on, due to this information changing quickly. Speaking with subject matter experts, % of people employed in paid positions may not be a good indicator either due to disruption of regular income cycles. Housing variables are better indicators, more stable because infrastructure changes are much slower in general which give a more holistic picture of what can be afforded.

The three clusters found tend to have the following characteristics:
- 35 townships in cluster 1 - low rural population, high percentage of households that have electricity or solar systems, near 100% access to safe sanitation - this cluster of townships is lowest on the need scale, highest in ability to pay
- 97 townships in cluster 2 - ~60% population in rural area, ~40% electrification, majority of households use cooking fuel costs natural resources
- 198 townships in cluster 0 - >85% population in rural area, <10% of households in HQ housing, ~70% access to safe sanitation, lowest % of electrification

Cluster 0, I would define as highest need, but less ability to pay. Cluster 2, I would define as the balance of being able to pay and needing the resources. Cluster 1, I would define as lowest need.