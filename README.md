# Classification of Pulsar Candidates using Gaussian Generative Modeling

## Introduction
<p>Radio pulsars are rapidly rotating neutron stars that emit radiofrequency waves with regular periodicity.
The signals from these objects are extremely weak, meaning that artificial radio sources can easily disturb observations. 
As a result, we may observe signals that look significant but are actually just a product of this interference. It then becomes a 
challenge to discern whether we have observed a real pulsar or not. </p>

<p>In the context of machine learning, this can be viewed as a binary clasification problem. 
We can use the pulse profiles of various known pulsars and the profiles of artificial sources to construct a model of what a
a real pulsar looks like. We can then use it to judge whether a new candidate is likely to be a real pulsar or not.</p>

<p>The HTRU2 data set supplied in the 'pulsar_stars.csv' file contains information about pulsar candidates collected in the High Time Resolution Universe Survey. 
Each candidate is described using 8 features: </p>

<ol>
<li> Mean of the integrated pulse profile. </li>
<li> Standard deviation of the integrated pulse profile. </li>
<li> Excess kurtosis of the integrated pulse profile. </li>
<li> Skewness of the integrated pulse profile. </li>
<li> Mean of the DM-SNR curve. </li>
<li> Standard deviation of the DM-SNR curve. </li>
<li> Excess kurtosis of the DM-SNR curve. </li>
<li> Skewness of the DM-SNR curve. </li>
<li> Class </li>
</ol>

<p>The 'class' feature in this data set indicates whether the candidate is a actually pulsar (1) or just radiofrequency interference/noise (0). 
Out of the 17,898 candidates in this data set, 1,639 are pulsars. We will use 16,000 data points from this set to train our model and the rest of the data 
to evaluate its performance.


## The Model
<p> Every feature in the above list has an associated mean and variance. We will separate our training data into pulsars (class 1) 
and non pulsars (class 0) and get the mean and variance of every feature for each class. We may think of a class as having an 
8 dimensional vector associated with it whose entries are the mean values of the features 1-8. Similarly, we can construct a 
covariance matrix for both classes. </p>

<p>We may then use these two parameters to fit a Gaussian probability density function to each class. This function is given by</p>

<img src="https://docs.scipy.org/doc/scipy-0.14.0/reference/_images/math/3e1b1a5eef9c95b3a62ee32069e3e772adabce34.png">

<p> Here, k denotes the number of features (8 in this case), sigma is the covariance matrix and mu is the 8D vector containing the means
of the features.</p>

<p> We have now constructed a mathematical model for what a real pulsar/noise looks like. When we are introduced to a new candidate, 
we can use Bayes' Rule to determine the probability of this candidate belonging to a particular class. We predict the most likely class
given that the candidate has the feature values it does.</p>

## Results
<p> After testing the model using 1,898 candidates, it was found to have a classification error of 3.11%. </p>

## Technologies
Python 3.8.3

## Sources
This code is based on UCSanDiegoX: Machine Learning Fundamentals (2019) winery-classification-gaussian [Source code]. 
Available at https://prod-edxapp.edx-cdn.org/assets/courseware/v1/2f3a287f717d464a8c58caf77f69881e/asset-v1:UCSanDiegoX+DSE220x+1T2019a+type@asset+block/winery-multivariate.zip
