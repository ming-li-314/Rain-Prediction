# Rain-Prediction
Erdos Institute Deep Learning Course Project

The goal is to predict whether it rains or not in the next 6 hours using Convolutional Neural Network (CNN) and Graph Neural Network (GNN). The weather forecasting data is from ERA5 (European Centre for Medium-Range Weather Forecasts (ECMWF) https://cds.climate.copernicus.eu/) single-level hourly data. Only the months of January, February, March of 2025 have been used. 

## Dataset

The weather dataset is spatial-temporal data. We restrict the spatial region to the US continent (excluding Hawaii and Alaska), the grid spacing is 0.25 degree. The temporal duration is every hour from 01/01/2025 to 03/31/2025. At each grid point, there are 10 variables: tp (Total Precipitation), t2m (2-meter Temperature), d2m (2-meter Dewpoint Temperature), u10(10-meter U-component of Wind), v10( 10-meter V_component of Wind), msl (Mean Sea Level Pressure), tcwv (Total Column Water Vapor), cape (Convective Available Potential Energy), slhf (Surface Latent Heat Flux), sshf (Surface Sensible Heat Flux). The dimensions are time: 2160, latitude: 105, longitude: 237. 

## Data Processing

We use data in the previous 12 hours to predict raining or not in the next 6 hours. We use 12-hour sliding window to construct the sample and 6-hour sliding window to construct the corresponding target label. The target is labeled raining if the total precipitation in the next 6 hours are larger than 1mm. To train GNN model, the data is converted to graph format. Each grid is treated as a node on the graph. The edges are from the 4 nearest grid points and 4 nearest diagonal grid points, in total 8 edge lines. 

## Modeling 
