# What happens when we merge GAN and CNN together for stock price prediction?

## Answer: You get a FinTech project with high accuracy!

## Project Arch
Capstone.ipynb contains all the CNN model training see below for an explanation, done over Google Colab
GAN.ipynb contains all the GAN model training and generating, done through Kaggle with a free Nvidia P100 GPU

## Project Description

### Idea

We find that human traders (mostly unprofessional ones, taking up a huge portion of trading system) uses visual cues and pattern recognitions to try identify when to buy and when to sell. To replicate this process with ML, we propose to use a model to see if we can capture some patterns, namingly head and shoulder and inverse head and shoulders patterns.

### Problem 0

The problem is we lack dataset for image model training as the most dominant models used are timeseries models, hence timeseries data. To solve this problem, we manually collected 420 images as a toy dataset of two patterns.

### Solution Pt.1

We trained CNN, specifically pretrained inception V3 model, on 70 images, achieved a 58% accuracy.
We later scaled to 420 images, and achieved 80% accuracy. This is a promising result to show that we can indeed replicate some level of human traders' habits when identifying patterns of stocks.

### Problem 1, emerged

We found that to collect these amount of data for training is quite time consuming, and we aim to fix this by introducing another ML model, GAN.
We want to leverage Deep Convolution GAN to generate images of the two patterns based on existing, samll sample image dataset of 70 images. Thus we can reduce the time and effort needed to have enough data for CNN to train and run with promising result.

### Experiment, DCGAN

We used Nvidia P100 GPU to load, train, and generate images with Deep Convolution GAN. Previouly, we spent ~6 hours to collect data. With DCGAN, we acquired 840 images, 420 for each pattern, in 3 minutes entirely. This massively reduced our workload.

### Solution with GAN + CNN, and result

We integrated the images, 70 small sample images and 840 generated images, together to train a new Inception V3 model. After training CNN on the new GAN + Raw dataset, we then tested the accuracy of prediction of GAN + Raw dataset to be as high as 98%.

### Unfortunate failure

We tested the new Inception V3 model on the previously collected, 420 images. It turns out we are not able to generate statistically significant result. The experiment solution fails unfortunately.

### Conclusion

Our failure comes directly from lack of computing power. From the example images we are able to generate, it is clear that the images are looking more and more similar to their category patterns, and with higher resolutions. We believe with more compute power, this new approach could help us capture patterns of candlestick images with a more life-like behavior, achieving better performance than only on timeseries data for daily traders who are not professionals to build and deploy.
