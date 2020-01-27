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

File compression is an important aspect in cloud computing and in Content Delivery Network (CDN). For example, in a CDN system, when a user asks for a new file or image, the request would be propagated to the root server which would retrieve the file from the database then transfer it back to an edge server the user has access to. Now, if this data is requested multiple times, it would be stocked in a cache server close to the client to speed up access and reduce demand on the company's bandwidth. These servers usually work in tandem with reverse proxies or load balancers to ensure efficiency and improve performances. 

Now for the case of images, a simple picture may have different resolutions requested by different users that would need to be cached. Say User A asks for a medium resolution picture which is requested from the root server then stored in the cache, and User B asks for the same image, but in a higher resolution which will also be stored in the cache. Storing multiple images in a cache servers can prove to be costly, especially if there are many nodes in the network. To reduce the size of these nodes, we can compress the images, but what can we do about the fact that we have multiple resolutions? We have the same picture, but in two different resolutions stored in the cache. Is there a way to save only 1 compressed representation of that image in the cache and have the choice to uncompress it to one of the 2 resolutions when the image needs to be retrieved?

Well, the solution I am currently studying is to train a network to compress *medium* resolution images, then to train a second network to compress *high* resolution images, and finally train a third network to use the compressed *high* resolution of the image and generate its *medium* resolution with high accuracy using AutoEncoders. This way, only high resolution images would have to be stored in the cache servers. Then, if this works the next step would be to train a generative network to use the compressed *medium* resolution images to get a *high* resolution image:  
1. Network to compress/decompress medium resolution images
2. Network to compress/decompress high resolution images
3. Network to retrieve medium resolution image from compressed high resolution image
    - 3b. Network to generate high resolution image from compressed medium resolution image

The findings of this project could then be extended to videos---which are some of the largest files in CDNs. This idea is explored in the paper [Deep Generative Video Compression](https://arxiv.org/abs/1810.02845) which explores the compression of videos using Variational Autoencoders.

### Deep Learning Task

**Goal**: Find compressed knowledge representation of the original input  

The goal in the first step is to find the latent, or compressed, representation of the images we want to save in the cache.  

**How**: By training Autoencoders on a large bank of images

This can be done notably by using a specific type of artificial neural network: the autoencoder. The autoencoder is a technique used to discover efficient data codings in an unsupervised manner. The aim of an autoencoder is to learn a representation for a set of data (encoder), typically for dimensionality reduction, then to learn how to reconstruct the data back from the reduced encoded representation to a representation that is as close to the original input as possible (decoder).

![](/assets/img/projects/imagecompress/encoder1.png){:.figure1 style="max-width: 50%;"} 
![](/assets/img/projects/imagecompress/encoder2.png){:.figure1 style="max-width: 50%;"} 

### Methods

For this task, 3 types of Autoencoders can be used:  

**Fully connected autoencoder**  

In the case of the fully connected autoencoder, both the encoder and decoder are fully-connected feedforward neural networks. First the input passes through the encoder to produce the code. Then, the decoder which has a similar neural network structure produces the output only using the code. The goal is to get an output identical with the input. Note that the decoder architecture is the mirror image of the encoder. This is not a requirement but it’s typically the case. The only requirement is the dimensionality of the input and output needs to be the same.

![](/assets/img/projects/imagecompress/fullyconnect_ae.png){:.figure1 style="max-width: 50%;"} 

However, this model would not suited for our task as the number of parameters in the fully connected layers would be way too large since we are dealing with images. For example, the number of parameters in the first layer assuming only 100 neurons and a 172x172 colored image would be 172 x 172 x 3 x 100 + 100 = 8,875,300 parameters only for the first layer.
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

First I trained the model using 172x172x3 images to represent the medium resolution images. Due to the limited computation power available, I had to limit the number of pixels that would be treated in the model. The images displayed in the graph below are validation samples at the end of the training epoch. For each pair of images, the top image is the original data and the bottom image is the reconstructed data through the model. 

![](/assets/img/projects/imagecompress/medium_resolution_juxta_done.png){:.figure1 style="max-width: 100%;"} 

![](/assets/img/projects/imagecompress/graph_med_resol.png){:.figure1 style="max-width: 100%;"} 

## Training the data High resolution (344x344x3)

Same idea as in the previous section using high resolution images. For this case, I trained the model using 344x344x3 images to represent the high resolution images. Again, the images displayed in the graph below are validation samples at the end of the training epoch. For each pair of images, the top image is the original data and the bottom image is the reconstructed data through the model. 

![](/assets/img/projects/imagecompress/high_resolution_juxta_done.png){:.figure1 style="max-width: 100%;"} 

![](/assets/img/projects/imagecompress/graph_high_resol.png){:.figure1 style="max-width: 100%;"} 

## Main idea is to Capture the features

The main idea when using the autoencoder in this problem is to capture the features of the images while disregarding the noise. Now, the next idea is to find a relation between the features collected from a high resolution image and the features of the same image in a lower resolution. 
- Decode an image using High resolution model
- Use the latent representation from this high resolution image
- Decode this representation using the Medium resolution model

![](/assets/img/projects/imagecompress/encode_type.png){:.figure1 style="max-width: 50%;"} 

## However when put in practice...

The results are not terrible. The figure below represents compressed representation of high resolution images being processed through a feedforward neural network and then to the decoder of the medium resolution images throughout the epochs. The model struggles at converging. 

![](/assets/img/projects/imagecompress/rebuild_image_juxta_done.png){:.figure1 style="max-width: 50%;"} 

![](/assets/img/projects/imagecompress/loss_decoding.png){:.figure1 style="max-width: 100%;"}

## Solutions tried until now...    

- Standardize and normalize the data
- Increase the capacity of the convolution network
- Have a fully connected layer in the middle
- Fine-tuning the modelsll
- Alternate between training the 
- Train the medium resolution to be able to decode high resolution from the start

## Have yet to try...

- Try with smaller data (3x32x32) or even smaller to infer new reasoning
- Variational autoencoders (VAE)

