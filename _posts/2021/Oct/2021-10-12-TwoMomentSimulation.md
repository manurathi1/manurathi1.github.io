---
title: "Two Moment Simulation - Mean and variance"
categories:
  - Maths
tags:
  - Probability 

# comments: true

--- 
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1OonMdRn8GxvdiRFQ17sm2d0qyiLISxyS?usp=sharing)

This article will look into how to simulate a series which has normal distribution where higher moments ( skew, Kurt ) is 0. for simulation with 4 moments see **here**.
in the first part, we will look into the case of 1 dimension. in the second ,we will see how to incorporate covariance for more than 1 dimension / series. 

## Univariate simulation ( 1 Dimension )
Idea is to simulate a series $$ X \sim N(\mu , \sigma) $$ if $\mu$ and $\sigma$ are given.

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2021/Oct/twoMomentNorm.png)

above image shows probability distribution for a R.V. that has a normal distribution. every point $x_{I}$ = $\mu$ + z $\times$ $\sigma$ where z $\in$ ($-\infty$, $\infty$)  
$$X \sim N(\mu , \sigma) | z \sim N(0,1)  $$
$$ X = \mu + N(0,1) \times \sigma $$

to generate N(0,1) we can use Box-Muller transformation
in excel,
```
NORM.S.INV(rand()), rand() is from univform dist.(0,1), NORM.S.INV is inverse of cumulative normal distribution  
```

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2021/Oct/TwoMomentSimulation_Mean.png) ![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2021/Oct/TwoMomentSimulation_Std.png)


as shown in this graph number of simulation / data points is critical to accuracy of the simulation. higher data points will lead to higher accuracy.  higher accuracy to expected mean and variance with less data points discussed **here** using random matrix theory


## Multivariate simulation ( >1 Dimension )

Idea is to simulate a series $$ X \sim N(\Mu , \Sigma) $$ if $\Mu$  = array of mean and $\Sigma$ = covariance are given. 

$$ X = \Mu + N(0,1) \times \sqrt{\Sigma} $$
$\sqrt{\Sigma} =L$  is cholskey decomposition of $\Sigma = LL^{T}$ 


