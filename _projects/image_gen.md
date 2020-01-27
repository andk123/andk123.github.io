---
layout: project
title: 'VAE vs GAN in Image Generation (Coming soon)'
date: April 2019
image: /assets/img/projects/hy-img.svg
screenshot: /assets/img/projects/imagegen/vae_vs_gan3.png
links:
  # - title: Website
  #   url: https://hydecorp.github.io/hy-img/
  - title: Source
    url: https://github.com/lebrice/IFT6135/tree/master/Assignment3
caption: Deep Learning
description: >
  Analysis of the Variational Autoencoder vs the Generative Adversarial Network in generative tasks (Coming Soon)
accent_color: '#4fb1ba'
#accent_image:
  #background: 'linear-gradient(to right,#19c9c7 0%,#57ded4 50%,#a5f9e4 100%)'
  #overlay:    true
---

# VAE vs GAN in Image Generation (Coming soon)

<!-- 
## Purpose


![](/assets/img/projects/imagegen/original.png){:.figure1 style="max-width: 75%;"} 


## Variational AutoEncoder (VAE)

## Generative Adversarial Network (GAN) 

## Implementation

In the implementation of the VAE and the GAN for this section, both models use the same archi-
tecture for the decoder and the generator. The only dierence is the GAN has a Sigmoid output
activation and the VAE has a Tanh output activation.


### 3.1 - Visual Samples
If we look at the results from both models shown in Figure 4, we see that both models are trying
to replicate the street house numbers of the SVHN dataset:

### Variational Autoencoder
In the case of the VAE, we can easily interpret the street house numbers of the samples in Figure 4
and although not perfect, the general quality of the images seems good, especially when compared
to the GAN on the right. However, the samples in the VAE are somewhat blurry. This may
be due to the fact that the VAE learns an explicit distribution of the data by sampling from a
Normal distribution [1]. Therefore during the training phase, when maximizing the likelihood of
an image given its latent representation the loss function could be favoring blurrier images over
sharper images as they are easier to represent in the latent space. Also, another observation is that
the numbers in the samples have a very similar shapes and resemble one another. It seems like
they all have the same font whereas in the SVHN dataset the street house numbers mostly have
dierent fonts. Even if the size of the numbers in the sample varies a bit more, the samples all
seem to follow a certain pattern. This can again be explained by the VAE using an explicit data
distribution.

### Generative Adversarial Network
In the case of the GAN, from a human perspective the average quality of the sample is poorer
than the VAE. Many samples are hard to recognize and some are far from resembling street house
numbers at all. However, the model is outputting some interesting results with its samples being
more diverse and irregular. They all vary in font and size, and also in thickness; some numbers of
very thin and pale while others are thicker and more conspicuous. This is something that did not
really happen in the case of the VAE. The samples do not follow any pattern at all. By contrast, we
may explain this with the GAN learning an implicit distribution of the data and having for main
focus to only make the generated images look realistic [1]. Also, one interesting thing to notice is
that although the general quality of the features is inferior to the VAE, the samples of the GAN
are generally less blurry. We can see the edges of the numbers more clearly. Also, some of the few
samples that succeeded at producing house number are clear and distinguishable as it can be seen
in Figure 5.  

In practice, GAN models are known to create very realistic and astonishing images, but our
experiment taught us that they are also very hard to train. We were expecting the GAN to realise
better images, but our model was very sensitive to parameters change and nding the right balance
between training the generator and the discriminator proved to be dicult. The discriminator
seemed to rst hit a plateau after a while and stop improving, and so would the generator. Increas-
ing the size of the network or looking for better parameters may have resulted in better looking outputs


## Compare between interpolating in the data space and in the latent space

In short, the latent space is a compressed representation of the important features of the input for
the decoder/generator to reconstruct an image or generate a new one. Therefore, by interpolating
in the latent space we interpolate between the features of the "useful" representation which changes
the structure of our output image, while interpolating in the data space directly modies the output
pixels of the image.  

Thus, when interpolating in the data space we should see a messier transition with some pixels
changing all around and new ones appearing, while interpolating in the latent space should yield a
smoother change with a transition in the structure of the image.

### GAN

We can see this in Figure 7. In the latent representation (above) we see the output shifting from
what seems to be a ve to a clearer representation of a 5 until it switches to a 13. While in the
data distribution (below) the pixel move around from a 5 to a mix between 5 and 13, and nally
clear up into a 13.

![](/assets/img/projects/imagegen/interpolation_GAN.png){:.figure1 style="max-width: 75%;"}

### VAE

This can also be seen in the VAE in Figure 8, in this case we can clearly see a shift of structure in
the latent representation (above) from a 5 to a 6. In the 5 rst interpolations, the image doesn't
really change between all the 5's, then it clearly switches to a 6 up until the end. However in the
data distribution (below) the image gets messy toward the middle with the pixels ranging between
a 5 and a 6.

![](/assets/img/projects/imagegen/interpolation_VAE.png){:.figure1 style="max-width: 75%;"}

## Using FID score

Below is our implementation of the function to evaluate the FID score and the results of running
this script over 1000 samples for both the VAE and the GAN can also be found below in Table
2. Although the images from the VAE seemed to have higher quality | this may be a subjective
opinion | the FID score of the GAN was lower. Our assumption is that the samples from our VAE
may look better to the human eye, but since the GAN's objective is to generate realer images, it
picked up more realistic features that were captured by the classier and achieved a better score.

![](/assets/img/projects/imagegen/fid_impl.png){:.figure1 style="max-width: 75%;"} 

![](/assets/img/projects/imagegen/fid_score.png){:.figure1 style="max-width: 50%;"}  -->