---
title: 'Validation InMachine Learning'
date: 2024-09-03
tags:
  - ML
---
### What is validation 
In ML validation means assessing how performant a system is on previously unseen data. 

- Direct validation (DV - train and test) also known as holdout validation, is the most straightforward method. A part of the dataset is used to train the model and another is used to test the performance of the model. 

Depending on the dimension of the dataset there will be different strategies for training and testing of the model. 

Cross-Validation (CV) is a good strategy if the available datasets are small. 
- Leave-Out-One CV (LOOCV). One at the time a datapoint is left out from the model. 
- K-fold CV is very economical because it allows to use all the data for training but also for testing. You cannot exclude that data used training are also used in the testing. 
- Nested CV
- 
---
### References:
- [Validation in the age of ML](https://www.sciencedirect.com/science/article/pii/S2666521223000042#bib75)
- [ML algorithm validation with a limited sample size](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0224365)
- 
