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
#description: >
#  GambTrax is a Self-Monitoring Gambling Application that 
accent_color: '#4fb1ba'
#accent_image:
  #background: 'linear-gradient(to right,#19c9c7 0%,#57ded4 50%,#a5f9e4 100%)'
  #overlay:    true
---

# Image Compression with Autoencoders (Work in Progress)

## Idea

Image compression is an important topic in Content Delivery Network (CDN) and for content distributors. When a user asks for a specific file or image, this request is made to the root server that sends the image to the edge server. Now, if this image is requested multiple times, it will be stocked in a cache server close to the client to be distributed to a node in a timely manner and reduce overhead. These servers work with load balancers and other clusters to ensure low latency in the network. Now for the cases of images, a simple picture may have different resolutions requested by different users at the same which will be cached. User A asks for a medium resolution which is downloaded from the root server and stored in the cache, and User B ask for the same image, but in a higher resolution.  

Storing multiple images in a cache servers can prove to be costly, especially if there are many nodes in the network. To reduce the size of these nodes, we can compress the images, but what can we do about the multiple resolutions? In the case mentioned above, instead of storing the same image into 2 different resolutions, is there a way to save this image in 1 compressed resolution and when uncompressing it, having the choice to get one of the 2 resolutions.  

The solution I am currently studying is to train a network to compress *medium* resolution images, then to train a second network to compress *high* resolution images, and finally train a third network to use the compressed *high* resolution of the image and generate its *medium* resolution with high accuracy using AutoEncoders. This way, only high resolution images would have to be stored in the cache servers. Then, if this works the next step would be to train a generative network to decompress *medium* resolution images into *high* resolution.

The findings in this project could then be extended to videos---which are some of the biggest files in CDNs. This idea is explored in the Paper [Deep Generative Video Compression](https://arxiv.org/abs/1810.02845), although it only explorer the compression of videos using Variational Autoencoders and not its decompression into different resolutions.
### Deep Learning Task

**Goal**: Find compressed knowledge representation of the original input  

The goal in the first step is to find the latent, or compressed, representation of the images we want to save in the cache.  

**How**: Using Autoencoders on a large bank of images

This can be done notably by using Autoencoders. The Autoencoder is a type of artificial neural network used to learn efficient data codings in an unsupervised manner. The aim of an autoencoder is to learn a representation for a set of data (encoder), typically for dimensionality reduction, then to learn how to reconstruct the data back from the reduced encoded representation to a representation that is as close to the original input as possible (decoder).

![](/assets/img/projects/imagecompress/encoder1.png){:.figure1 style="max-width: 50%;"} 
![](/assets/img/projects/imagecompress/encoder2.png){:.figure1 style="max-width: 50%;"} 

### Methods

For this task, 3 types of Autoencoders can be used:  

**Fully connected autoencoder**  

In the case of the fully connected autoencoder, both the encoder and decoder are fully-connected feedforward neural networks. First the input passes through the encoder to produce the code. The decoder, which has a similar artificial neural network structure, then produces the output only using the code. The goal is to get an output identical with the input. Note that the decoder architecture is the mirror image of the encoder. This is not a requirement but it’s typically the case. The only requirement is the dimensionality of the input and output needs to be the same.

![](/assets/img/projects/imagecompress/fullyconnect_ae.png){:.figure1 style="max-width: 50%;"} 

-> 172 x 172 x 3 for input 
space -> Millions of parameters -> Not enough memory  
<br/>

**Convolutional autoencoders**  
 Unlike the fully connected autoencoder, the convolutional autoencoder keep the spatial information of the input image data as they are, and extract information gently in what is called the Convolution layer. This way, the number of parameters needed using the convolutional autoencoder is greatly reduced. Furthermore, it also retains the spatial relationships in the data.
 
![](/assets/img/projects/imagecompress/conv_ae.png){:.figure1 style="max-width: 75%;"}  

Model currently in use  
<br/>

**Variational autoencoders**  

A variational autoencoder can be defined as being an autoencoder whose training is regularised to avoid overfitting and ensure that the latent space has good properties that enable generative process. Just as a standard autoencoder, a variational autoencoder is an architecture composed of both an encoder and a decoder and that is trained to minimise the reconstruction error between the reconstructed data and the initial data. However, rather than building an encoder which outputs a single value to describe each latent state attribute, we formulate our encoder to describe a probability distribution for each latent attribute. This introduces some regularisation in the latent space. In this case, the encoder model can be referred to as the recognition model whereas the decoder model is can be referred to as the generative model.

![](/assets/img/projects/imagecompress/vae.jpg){:.figure1 style="max-width: 65%;"} 

Possible alternative solution,
 but generally used as a generative model

## Data from DIV2K Dataset
 
In order to train this model and provide a proof of concept, I decided to opt for the DIVerse 2K resolution high quality images (DIV2K) dataset. The DIV2K dataset includes:
- Numerous images duplicated in different resolutions
- For each resolution: 800 images for the training set
- 100 images for the validation set
- 100 images for the testing set

![](/assets/img/projects/imagecompress/DIV2K_dataset2.png){:.figure1 style="max-width: 50%; display: inline-block"} 
![](/assets/img/projects/imagecompress/DIV2K_dataset3.png){:.figure1 style="max-width: 50%; display: inline-block"}  

Dataset available at: [https://data.vision.ee.ethz.ch/cvl/DIV2K/](https://data.vision.ee.ethz.ch/cvl/DIV2K/)

## Training the data Medium resolution (172x172x3)

For each pair of images, on top you have the original image and at the bottom you have the reconstructed image. EThe first 2 lines are the first epoch, while the last two lines are the 10th epoch.

![](/assets/img/projects/imagecompress/medium_resolution.png){:.figure1 style="max-width: 50%;"} 

![](/assets/img/projects/imagecompress/medium_resolution2.png){:.figure1 style="max-width: 50%;"} 

![](/assets/img/projects/imagecompress/graph_med_resol.png){:.figure1 style="max-width: 50%;"} 

## Training the data High resolution (344x344x3)

Same idea as in the previous section using high resolution images.

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

