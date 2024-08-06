# Stata-Navigation

## Overview
An image-based system for navigating MIT's Stata Center, a notoriously complex building.

Methods:
1. The user uploads an image from the first floor of the Stata Center and a desired destination.
2. The system uses ResNet-18 to identify the user's location based on the uploaded image.
3. The system uses Dijkstra's algorithm to find the shortest path between the user's location and their destination.
4. The system returns navigation instructions to the user.

Results:
- The location identification step achieves a top-1 accuracy of 46.5%, a top-5 accuracy of 63.8%, and a median error of 29 feet on our test set.
- Using the location identified by ResNet-18, the system produces high-quality navigation instructions, helping the user reach their destination easier.

This project was conducted in collaboration with [Krish Datta](https://www.linkedin.com/in/krishanudatta/) and [Sara Pasquino](https://www.linkedin.com/in/sarapasquino/), as part of MIT's 6.8300: Advances in Computer Vision course.

## Repository Contents
This repository contains project [code](https://github.com/haydenratliff/stata-navigation/blob/main/code), [model checkpoints](https://github.com/haydenratliff/stata-navigation/blob/main/model_checkpoints), [image embeddings](https://github.com/haydenratliff/stata-navigation/blob/main/embeddings), and our [final report](https://github.com/haydenratliff/stata-navigation/blob/main/report.pdf).

The code is organized into three sections. First, we pre-process the data and use several foundation models to compute image emebeddings. Next, we use PyTorch to train classification heads using the embeddings. Last, we use the foundation models + the custom classification head to navigate the building. As a note, we separated the embedding computation from the classification head training to minimize the compute required for the project. This allowed us to complete the project without a Google Colab subscription.

We store the model checkpoints so that each component can easily load the requisite models. And, we store image embeddings so that the model training code can easily load in training data.

## Dataset
The image dataset for this project is comprised of 10,189 images from 37 locations on the first floor of Stata. See [here](https://github.com/haydenratliff/stata-navigation/blob/main/data_collection.pdf) for a map of our data collection locations. We built the dataset by taking a 10-15 second video at each location. In each video, we slowly turn to cover all 360 degrees of the location, while panning upwards and downwards to vary the angle. Finally, we extracted all frames from the videos.

Due to unintended leakage from our training dataset into the testing dataset, we collected a secondary test set at all 37 locations of 185 total images. Our results use this secondary test set.

This dataset is currently private, but may be published to this repository at a later date. At this moment, the dataset can be made available upon request.
