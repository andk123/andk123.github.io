---
layout: project
title: 'Image Compression with Autoencoders (Work in Progress)'
date: Dec 2019
image: /assets/img/projects/hy-img.svg
screenshot: /assets/img/projects/autoencoder.png
links:
  # - title: Website
  #   url: https://hydecorp.github.io/hy-img/
  #- title: Source
  #  url: https://github.com/andk123/Self-MonitoringGamblingApp
#caption: Mobile Application for Gambling Self-Monitoring
description: >
  GambTrax is a Self-Monitoring Gambling Application that 
accent_color: '#4fb1ba'
#accent_image:
  #background: 'linear-gradient(to right,#19c9c7 0%,#57ded4 50%,#a5f9e4 100%)'
  #overlay:    true
---

# Image Compression with Autoencoders (Work in Progress)

## Purpose

### Deep Learning Task

Goal: Find compressed knowledge representation of the original input  
How: Training on a lot of data

![](/assets/img/projects/imagecompress/encoder1.png){:.figure1 style="max-width: 50%;"} 
![](/assets/img/projects/imagecompress/encoder2.png){:.figure1 style="max-width: 50%;"} 

## 3 Types of Autoencoders

<u> Fully connected autoencoder:</u> -> 172 x 172 x 3 for input 
space -> Millions of parameters -> Not enough memory
<br />
<u> Convolutional autoencoders:</u> Model currently in use
<br />
<u> Variational autoencoders:</u> Possible alternative solution,
 but generally used as a generative model

![](/assets/img/projects/imagecompress/encode_type.png){:.figure1 style="max-width: 50%;"} 

## Data from DIV2K Dataset

DIVerse 2K resolution high quality images includes:
- Different resolutions and for each resolution:
- 1000 images divided into — 800 images
- for training — 100 images for validation — 100 images 
- for testing

Dataset available at: https://data.vision.ee.ethz.ch/cvl/DIV2K/

![](/assets/img/projects/imagecompress/DIV2K_dataset.png){:.figure1 style="max-width: 50%;"} 

## Training the data Medium resolution (172x172x3)

![](/assets/img/projects/imagecompress/medium_resolution.png){:.figure1 style="max-width: 50%;"} 

![](/assets/img/projects/imagecompress/medium_resolution2.png){:.figure1 style="max-width: 50%;"} 

![](/assets/img/projects/imagecompress/graph_med_resol.png){:.figure1 style="max-width: 50%;"} 

## Training the data High resolution (344x344x3)

![](/assets/img/projects/imagecompress/high_resolution.png){:.figure1 style="max-width: 50%;"} 

![](/assets/img/projects/imagecompress/high_resolution2.png){:.figure1 style="max-width: 50%;"} 

![](/assets/img/projects/imagecompress/graph_high_resol.png){:.figure1 style="max-width: 50%;"} 

## Main idea is to Capture the features

- Decode an image using High resolution model
- Use the latent representation from this high resolution image
- Decode this representation using the Medium resolution model

![](/assets/img/projects/imagecompress/encode_type.png){:.figure1 style="max-width: 50%;"} 

## However when put in practice...

The results are not terrible. This is the images at the start of training. The model struggles at converging.

![](/assets/img/projects/imagecompress/loss_decoding.png){:.figure1 style="max-width: 50%;"} 

![](/assets/img/projects/imagecompress/resolution_decoding.png){:.figure1 style="max-width: 50%;"} 

![](/assets/img/projects/imagecompress/resolution_decoding2.png){:.figure1 style="max-width: 50%;"} 

## Solutions tried until now...    

- Standardize and normalize the data
- Increase the capacity of the convolution network
- Have a fully connected layer in the middle
- Alternate between training the 
- Train the medium resolution to be able to decode high resolution from the start

## Have yet to try...

- Try with smaller data (3x32x32) or even smaller to infer new reasoning
- Variational autoencoders (VAE)

