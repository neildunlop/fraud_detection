# Fraud Detection with R, H2O and Auto-Encoders

## Summary
This is an experiment in Machine Learning.  The aim is to improve me familarity with machine learning, allow me to get some practice with the available tools and see machine
learning in action, warts and all.    

## The Tools
The repository contains an 'R' nodebook that can be viewed, executed and edited using R-Studio.

The notebook allows you to have notes along side runnable code / script blocks and the results of that execution are embedded within the notebook.

This notebook is by no means complete and contains all my random musings, false turns and dead ends.  There may well be things that are totally wrong or I have totally 
misunderstood.  I've spent a long time learning how to do simple things in R and H2O (my machine learning library of choice).  I've spent a decent amount of time 
looking up what different terms mean.  I've spent more time than is decent trying to understand what different machine learning algorithms do and then trying to understand
the maths behind them... I still dont really understand the maths but I mostly dont need to.
 
## The Experiment

The experiment aims to correctly classify fraudulent and non-fraudent credit card transactions from a file of approximately 71000 transactions.  The data comes from a 'Kaggle'
competition and is freely available for download.  I've probably added it to this repository already.

There are lots of different machine learning algorithms that could be used to 'solve' this problem but I decided to use 'Anomaly Detection'.  I'm not interested in 
trying to predict any particular value.  I just want to know if a transaction looked fraudulent or not.. and I'm not particualrly interested in why the machine 
thought the transaction was fraudulent.  

There are lots of different ways of doing anomaly detection but I was interested to see 'autoencoders' in use.  With an autoencoder you
dont tell the machine learning algorithm anything about the domain or the data.  You just give it the data and say "figure out a pattern that characterises this data".  
Given that the majority of the data is non-fraudulent, the machine learns the characteristics of non-fraudulent transactions.

The autoencoder takes each row of data and breaks it down to its significant characteristics and then tries to reconstruct the original data from just those characteristics.  
Think of something a bit like ZIP compression but where ZIP might lose a *bit* of data, but you can still recognise the uncompressed result.

Because the autoencoder see's lots of non-fraudulent transactions is used the key characteristics of a non-fraudulent transaction to build its 'encoded' representation
of a row.  What the autoencoder has learned is used to create a model.  When we feed input data into the model, its 'encoded' to its compressed form and we can then ask
it to recreate the original row from the encoded form.  How different the original is from the output can be given a score.  The lower the score, the more the output of 
the model matches the original input.

When we feed the model a fraudulent row, it encodes the row.  However, our model is good a grabbing the characteristics of a non-fraudulent transaction so the theory
is that it will grab the wrong key characteristics of the fraudulent row.  When it tries to recreate the original row from the encoded version, it gets it very wrong 
and the score for that row is very high.  

This comparison of scores allows us to spot fraudulent and non-fraudulent transactions without us needing to know anything about what the input data is.  I dont actually
care if the input variables are time and amount and retailer.  The autoencoder will figure out if they are significantly linked to fraud or non-fraud from the data its
seen.

Anyway, thats the theory.... check out the notebook to see me slowly figuring that out with code and real data.  

