# Rain-Prediction
Erdos Institute Deep Learning Course Project

The goal is to predict whether it rains or not in the next 6 hours using Convolutional Neural Network (CNN) and Graph Neural Network (GNN). The weather forecasting data is from ERA5 (European Centre for Medium-Range Weather Forecasts (ECMWF) https://cds.climate.copernicus.eu/) single-level hourly data. Only the months of January, February, March of 2025 have been used. 

## Dataset

The weather dataset is spatial-temporal data. We restrict the spatial region to the US continent (excluding Hawaii and Alaska), the grid spacing is 0.25 degree. The temporal duration is every hour from 01/01/2025 to 03/31/2025. At each grid point, there are 10 variables: tp (Total Precipitation), t2m (2-meter Temperature), d2m (2-meter Dewpoint Temperature), u10(10-meter U-component of Wind), v10( 10-meter V_component of Wind), msl (Mean Sea Level Pressure), tcwv (Total Column Water Vapor), cape (Convective Available Potential Energy), slhf (Surface Latent Heat Flux), sshf (Surface Sensible Heat Flux). The dimensions are time: 2160, latitude: 105, longitude: 237. 

## Data Processing

We use data in the previous 12 hours to predict raining or not in the next 6 hours. We use 12-hour sliding window to construct the sample and 6-hour sliding window to construct the corresponding target label. The target is labeled raining if the total precipitation in the next 6 hours are larger than 1mm. To train GNN model, the data is converted to graph format. Each grid is treated as a node on the graph. The edges are from the 4 nearest grid points and 4 nearest diagonal grid points, in total 8 edge lines. 

The dataset is highly imbalanced with less than 10% labeled as raining. 

## Modeling 
- Convolutional Neural Network
- Graph Neural Network

Loss function: a combination of F1 loss, Focal loss and Cross Entropy loss.

## Results

- Graph Neural Network models give very inaccurate predictions (less than 20% accuracy, f1 score around 0.2).
- Convolutional Neural Network models have much better performance in predicting raining (The scores on test dataset are F1: 0.7679, Accuracy: 0.9388, Precision: 0.7712, Recall: 0.7646).
  
  See the following visualizations: confusion matrix and the sample visualization on the spatial map. 
  
   <img src="https://github.com/user-attachments/assets/c8db090b-6246-4a79-99fb-f01c45c08a30" width = "600">

  <img src="https://github.com/user-attachments/assets/071e5dc6-2b86-4dbb-86ae-377ce31d8a86" width = "800">

## Outlook

Of course, if more computational resources are available, one should scale up the dataset and the CNN structure. It will be very interesting to figure out why the GNN model behaves much worse than a typical CNN model. 

