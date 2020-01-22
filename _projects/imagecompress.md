---
layout: project
title: 'Image Compression with Autoencoders (Work in Progress)'
date: Jan 2020
image: /assets/img/projects/hy-img.svg
screenshot: /assets/img/projects/autoencoder.png
links:
  # - title: Website
  #   url: https://hydecorp.github.io/hy-img/
  #- title: Source
  #  url: https://github.com/andk123/Self-MonitoringGamblingApp
caption: Deep Learning
description: >
  GambTrax is a Self-Monitoring Gambling Application that 
accent_color: '#4fb1ba'
#accent_image:
  #background: 'linear-gradient(to right,#19c9c7 0%,#57ded4 50%,#a5f9e4 100%)'
  #overlay:    true
---

# Image Compression with Autoencoders (Work in Progress)

## Idea

Image compression is an important topic in Content Delivery Network (CDN) and for content distributors. When a user asks for a specific file or image, this request is made to the root server that sends the image to the edge server. Now, if this image is requested multiple times, it will be stocked in a cache server close to the client to be distributed to a node in a timely manner and reduce overhead. These servers work with load balancers and other clusters to ensure low latency in the network. Now for the cases of images, a simple pciture may have different resolutions requested by different users at the same which will be cached. User A asks for a medium resolution which is downloaded from the root server and stored in the cache, and User B ask for the same image, but in a higher resolution.  

Storing multiple images in a cache servers can prove to be costly, especially if there are many nodes in the network. To reduce the size of these nodes, we can compress the images, but what can we do about the multiple resolutions? In the case mentioned above, instead of storing the same image into 2 different resolutions, is there a way to save this image in 1 compressed resolution and when uncompressing it, having the choice to get one of the 2 resolutions.  

The solution I am currently studying is to train a network to compress *medium* resolution images, then to train a second network to compress *high* resolution images, and finally train a third network to use the compressed *high* resolution of the image and generate its *medium* resolution with high accuracy using AutoEncoders. This way, only high resolution images would have to be stored in the cache servers. Then, if this works the next step would be to train a generative network to decompress *medium* resolution images into *high* resolution.

The findings in this project could then be extended to videos---which are some of the biggest files in CDNs. This idea is explored in the Paper [Deep Generative Video Compression](https://arxiv.org/abs/1810.02845), although it only explorer the compression of videos using Variational Autoencoders and not its decompression into different resolutions.

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

