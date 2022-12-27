---
title: "Two Moment Simulation - Mean and variance"
# categories:
#   - maths
excerpt: "Simulate data points when first two moments are known i.e. mean and standard deviation is given" 
tags:
  - Probability 
  - Simulation

# comments: true

--- 
<!-- [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1OonMdRn8GxvdiRFQ17sm2d0qyiLISxyS?usp=sharing) -->

This article will look into how to simulate a series which has normal distribution i.e. higher moments ( Skew, Excess Kurt ) is 0. for simulation with 4 moments refer to this <a href = "/FourMomentSimulation/"> article </a> <br/>
In the first part, we will look into the case of 1 dimension. in the second ,we will see how to incorporate covariance for more than 1 dimension. 

## Univariate simulation ( 1 Dimension )
Idea is to simulate a series 

$$ X \sim N(\mu , \sigma) $$ 

if $\mu$ and $\sigma$ are given.

<figure>
    <a href="/assets/images/2021/Oct/twoMomentNorm.png"><img src="/assets/images/2021/Oct/twoMomentNorm.png"></a>
    <figcaption> </figcaption>
</figure>

<!-- ![]({{ site.url }}{{ site.baseurl }}/assets/images/2021/Oct/twoMomentNorm.png) -->

> probability distribution for a R.V. that has a normal distribution. every point <br/> $x_{i}$ = $\mu$ + z $\times$ $\sigma$ where z $\in$ ($-\infty$, $\infty$)  

$$ X \sim N(\mu , \sigma) | z \sim N(0,1)  $$

$$ X = \mu + N(0,1) \times \sigma $$

To generate N(0,1) we can use Box-Muller transformation. <br/>
in excel:
```
NORM.S.INV(rand()), rand() is from univform dist.(0,1), NORM.S.INV is inverse of cumulative normal distribution  
```

<!-- ![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2021/Oct/TwoMomentSimulation_Mean.jpg) ![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/2021/Oct/TwoMomentSimulation_Std.jpg) -->

<figure class="half">
    <a href="/assets/images/2021/Oct/TwoMomentSimulation_Mean.jpg"><img src="/assets/images/2021/Oct/TwoMomentSimulation_Mean.jpg"></a>
    <a href="/assets/images/2021/Oct/TwoMomentSimulation_Std.jpg"><img src="/assets/images/2021/Oct/TwoMomentSimulation_Std.jpg"></a>
    <figcaption> </figcaption>
</figure>


> number of simulation / data points is critical to accuracy of the simulation. higher data points will lead to higher accuracy.

Higher accuracy to expected mean and variance with less data points discussed **here** using random matrix theory


## Multivariate simulation ( >1 Dimension )

Idea is to simulate a series 

$$ X \sim N(M , \Sigma) $$ 

if $M$  = array of mean and $\Sigma$ = covariance are given. 

$$ X = M + N(0,1) \times \sqrt{\Sigma} $$ 

$\sqrt{\Sigma} =L$  is cholskey decomposition of $\Sigma = LL^{T}$ 


