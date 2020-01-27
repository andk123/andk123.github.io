---
layout: project
title: 'Language Modelling: RNN vs GRU vs Transformer (Coming soon)'
date: March 2019
image: /assets/img/projects/hy-img.svg
screenshot: /assets/img/projects/transformer.png
links:
  # - title: Website
  #   url: https://hydecorp.github.io/hy-img/
  - title: Source
    url: https://github.com/lebrice/IFT6135/tree/master/Assignment2
caption: Deep Learning
description: >
  Compare the performances of a Vanilla RNN vs GRU vs the attention module of a transformer network on the Penn Treebank dataset (Coming Soon)
accent_color: '#4fb1ba'
#accent_image:
  #background: 'linear-gradient(to right,#19c9c7 0%,#57ded4 50%,#a5f9e4 100%)'
  #overlay:    true
---

# Language Modelling: RNN vs GRU vs Transformer (Coming soon)

<!-- ## Purpose

The purpose of this project was to implement and train sequential language models on the Penn
Treebank dataset. Language models learn to assign a likelihood to sequences of text. The elements
of the sequence (typically words or individual characters) are called tokens, and can be represented
as one-hot vectors with length equal to the vocabulary size, e.g. 26 for a vocabulary of English
letters with no punctuation or spaces, in the case of characters, or as indices in the vocabulary for
words. In this representation an entire dataset can be representedmby a 3-dimensional tensor, with axes corresponding to: (1) the example within the dataset/minibatch, (2) the time-step within the sequence, and (3) the index of the token in the vocabulary.
Sequential language models do next-step prediction, in other words, they predict tokens in a
sequence one at a time, with each prediction based on all the previous elements of the sequence. A
trained sequential language model can also be used to generate new sequences of text, by making
each prediction conditioned on the past predictions (instead of the ground-truth input sequence). 

Therefore, me and my colleagues first started by implement the Vanilla RNN, followed by the GRU and lastly[...]

## The Penn Treebank Dataset 

This is a dataset of about 1 million words from about 2,500
stories from the Wall Street Journal. It has Part-of-Speech annotations and is sometimes used
for training parsers, but it's also a very common benchmark dataset for training RNNs and other
sequence models to do next-step prediction.

## RNN

A simple recurrent neural network (SRNN) is also
called a \vanilla" RNN or \Elman network". The equations for an SRNN are:

## GRU

The use of \gating"
(i.e. element-wise multiplication, represented by the  symbol) can signicantly improve the
performance of RNNs. The Long-Short Term Memory (LSTM) RNN is the best known example of
gating in RNNs; GRU-RNNs are a slightly simpler variant (with fewer gates).

## Transformer network with attention module

While prototypical
RNNs \remember" past information by taking their previous hidden state as input at each step,
recent years have seen a profusion of methodologies for making use of past information in dierent
ways. The transformer 2 is one such fairly new architecture which uses several self-attention networks
(\heads") in parallel, among other architectural specics.

## Results

Lower PPL is better.

![](/assets/img/projects/sentencegen/experiment_results.png){:.figure1 style="max-width: 75%;"} 

## Analysis of the results

### What ended up happening

Before the start of this assignment, some of our assumptions were that the Transformer would
be a very eective model, that the Gated Recurrent Units (GRU) would generalize better and
learn faster than the Recurrent Neural Network (RNN), and that the Adaptive Moment
Estimation (ADAM) optimizer would make the models train faster and be more ecient than
other optimizers. Also, we were expecting the training perplexity to always be lower than
the validation perplexity, but one model showed the inverse behaviour (this will be discussed
further in question 2.)  

Based on the recent progress in Attention [1], we expected the Transformer to be the most
eective and have the best generalization performance using its self-attention mechanism
to make a correlation between the current words and the previous part of the sentence.
However, the GRU generally performed better in our experiments according to our table of
Table 2. We believe this discrepancy can be explained by the fact that Transformers are
known to be dicult to train, and often very sensitive to changes in hyper-parameter settings
[1]. Furthermore, in their paper, the authors trained on bigger datasets while our resources
were limited. Therefore, with more time and resources, we believe a more optimal set of
hyperparameters could be found, which would allow the Transformer to outperform the GRU
with sucient training.  

However, our assumptions of the GRU performing better than the Vanilla RNN proved to be
correct. We believe this to be due to the GRU being designed as an improvement over the
traditional RNN, with its gating mechanism allowing for deeper propagation of the gradients.
In the case of the ADAM optimization, it made the models train and converge faster, but in
terms of eciency there was no clear winners between ADAM and the Stochastic Gradient
Descent with a Learning Rate Schedule (SGD LR SCH), as can be seen in Figure 7. This
can be explained with their eciency being largely dependent on the other hyperparameters.
This will also be discussed in the answer to question 2.

### Best optimizer, generalization performance and architecture

If we look at the results of Figure 7 we can notice that the two SGD optimizers have similar
curves and similar behavior | the curve 4_2_a does not appear in the given range, but you
can nd it in Figure 2. However, the SGD_LR_SCH is a much better optimizer and looking at
the results we notice that it always converges to a lower perplexity because of its learning rate
decay (as the gradients are able to increase the model's performance for a longer period of
time). In fact, the SGD_LR_SCH may take more time to reach its optimal value than the SGD,
but its perplexity is usually better. Because of this, we will mostly compare SGD_LR_SCH with
ADAM, as we assume SGD_LR_SCH is more ecient than SGD.  

Now, comparing the SGD_LR_SCH to the ADAM optimizer, ADAM clearly has a shorter train-
ing time thanks to its implementation using momentum and adaptive learning rates. In terms 
of performance and best validation perplexity, from the results shown in Table 2 there is no
clear winner between SGD_LR_SCH and ADAM. Both methods behaved well depending on
the architectures and hyperparameters. Using the Transformer, ADAM was more eective,
while using the GRU, the SGD_LR_SCH was the winner. However, using the simple RNN, both
optimizers were close to one another.  

Yet, an interesting observation we can make is that although the validation perplexity for both
optimizers was similar, the training perplexity of the SGD_LR_SCH was generally smaller than
the training perplexity of ADAM for the three architectures, especially for the Transformer
where the validation perplexity was better than the training perplexity according to Table 2.
What we could infer from this is that SGD_LR_SCH will have a lower variance on a training set
and should generalize better on unseen data while ADAM will converge faster but could be
more prone to overtting if not tuned appropriately.  

Lastly, while tuning the hyperparameters to nd the best model, we realized that the opti-
mizers, especially ADAM, are sensitive to the learning rate and the batch size. A smaller
batch size would often require a smaller learning rate. Also, using a learning rate too big with
SGD would prevent it from converging and improving, while a wrong combination of learning
rate/batch size with ADAM would generally cause the model to overt and the validation
perplexity of the model would start degrading after only a few epochs (Figure 7 and Figure 8
for reference). The optimal sequence length was between 20 and 35 and the number of hidden
units and hidden layers was dependent on the architecture and optimizer chosen.

### Most reliable architecture for this problem (and most unstable)

Based on our hyperparameter search and the results listed in Table 1 and Table 2, we found
that the GRU with SGD_LR_SCH was generally performing very well and was the most reliable.
This is also true with the ADAM and the SGD optimizer when using the GRU. The GRU
was the best architecture in our search.  

Although the Transformer with the right settings was performing decently, it was the most
unstable during the hyperparameters search. Indeed, the Transformer is very sensitive to
changes in its parameters. This is illustrated in Figure 6 where we can see many of the
validation perplexities in the plot growing out of proportion. The Vanilla RNN had the poorest
best perplexities, but generally its results were more stable than those of the Transformer.


![](/assets/img/projects/sentencegen/rnn_loss_timestep.png){:.figure1 style="max-width: 75%;"} 

![](/assets/img/projects/sentencegen/gru_loss_timestep.png){:.figure1 style="max-width: 75%;"} 

![](/assets/img/projects/sentencegen/transformer_loss_timestep.png){:.figure1 style="max-width: 75%;"} 

![](/assets/img/projects/sentencegen/grad_timestep.png){:.figure1 style="max-width: 75%;"} 
 -->
