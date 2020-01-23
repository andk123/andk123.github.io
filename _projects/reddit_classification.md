---
layout: project
title: 'Reddit Comments Classification - Text Classification'
date: Nov 2019
image: /assets/img/projects/hy-img.svg
screenshot: /assets/img/projects/reddit_kaggle_comp2.png
links:
  # - title: Website
  #   url: https://hydecorp.github.io/hy-img/
  - title: Source
    url: https://drive.google.com/drive/folders/1pfQdeh5e90la2Mh0rqhpGUk2wnFrOT_u?usp=sharing
caption: Machine Learning
# description: >
#   Text Classification
accent_color: '#4fb1ba'
#accent_image:
  #background: 'linear-gradient(to right,#19c9c7 0%,#57ded4 50%,#a5f9e4 100%)'
  #overlay:    true
---

# Reddit Comments Classification - Kaggle Competition

## Motivation
Here, my colleague Ilyas Amaniss and I analyzed the different techniques used in text classification, notably the various ways of performing feature extraction and the performance of the different algorithms used in this task. To test and compare these techniques, we entered the 2019 Kaggle Competition on Reddit comments classification where the goal was to design a machine learning algorithm to automatically sort short texts into a pre-determined set of topics. These texts were extracted from raw posts and comments written by Reddit users.

In most classification tasks, working on raw data can prove to be tedious. Therefore, it is beneficial to process and treat the data before starting any analysis. This process is the feature design and feature extraction. While they comprise of countless methods, some may speed up the learning process, reduce the size of the dataset or increase the accuracy of the model. However, it is important to carefully choose the feature extraction methods as they may also decrease the model's efficiency. For the Reddit comments classification competition, some of the techniques we decided to use are, but not limited to:  

**Feature design phase**
- Tokenization
- Removal of stop words
- Stemming and Lemming
- Term Frequency-Inverse Document Frequency (TF-IDF)

After processing the data, it is then time to choose the model to categorize the different text corpus into topics. Obviously, depending on the feature extractions methods used, some models may before better than others. For this project, we focused on 3 methods:  

**Algorithms**
- Naive Bayes 
- Support Vector Machine (SVM)
- Mulilayer Perceptron/Feedforward Neural Network

## Article

For the complete methodology, results, analysis and the rest of our findings see the full article below.

<html>
<head>
  <meta charset="UTF-8">
  <title>PDF.js Example</title>
  <script src="/assets/js/pdfjs/build/pdf.js"></script>
  <script src="/assets/js/pdfjs/build/kaggle/simple.js"></script>
</head>
<body>
  <a target="_blank" href="/assets/js/pdfjs/web/viewer.html?file=/assets/js/pdfjs/build/kaggle/Kaggle_reddit_classification.pdf">
    <canvas id="pdf"></canvas>
  </a>
</body>
</html>

[Link to the article](/assets/js/pdfjs/web/viewer.html?file=/assets/js/pdfjs/build/kaggle/Kaggle_reddit_classification.pdf). 