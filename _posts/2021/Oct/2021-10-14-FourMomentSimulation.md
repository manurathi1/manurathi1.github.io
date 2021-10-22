---
title: "Four Moment Simulation - Mean, Variance, Skew, Kurtosis"
# categories:
#   - maths
excerpt: "Simulate non normal data points using Fleishman power method targeting first four moments" 
tags:
  - Probability 
  - Simulation

# comments: true

--- 
<!-- [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1OonMdRn8GxvdiRFQ17sm2d0qyiLISxyS?usp=sharing) -->


In the previous  <a href = "/TwoMomentSimulation/"> article </a>  we discussed how to simulate normal distribution points for a given mean and standard deviation / covariance matrix <br/>
Here, we will discuss how to generate non normal numbers with unimodal distribution i.e. simulate using all four moments ( mean , standard deviation, skewness and kurtosis ) ignoring coskewness and cokurtosis <br/>

We refer to paper by Hao Luo[1], which uses Fleishman's power method[2] to simulate non normal data 

The idea is to first simulate a series

$$ G \sim D(0,1, \gamma_{1}, \gamma_{2}) $$ 

where $\gamma_{1}$, $\gamma_{2}$  is the skewness and excess kurtosis of the distribution D, resp. <br/>

Second, we will use our understanding from previous article ^link to covert first two moments of D from 0,1 to $\mu$ , $\sigma$ / $\Sigma$

As per power method, Y can be defined as the third degree polynomial of X

$$ Y = a + bX + cX^{2} + dX^{3} $$ 

where $X \sim N(0,1)$  

we would solve for 

$$ E(Y) = 0 , E(Y^{2}) = 1, E(Y^{3}) = \gamma_{1}, E(Y^{4}) = \gamma_{2} + 3 $$

The following 4 equations we got by solving the above equations:

$$ F_1(b,c,d) : b^2+6bd+ 2c^2 +15d^2-1 =0 $$

$$ F_2(b,c,d) : 2c(b^2+24bd+105d^2+2)-\gamma_1=0$$

$$ F_3(b,c,d) : 24(bd + c^2[1 + b^2 + 28bd] + d^2[12 + 48bd + 141c^2 + 225d^2])-\gamma_2 = 0 $$

$$ a = -c $$

To solve for a,b,c,d:

$$ minimize F(b,c,d) = F_1^2(b,c,d)+F_2^2(b,c,d)+F_3^2(b,c,d) $$ constrained on 

$$ F_i(b,c,d) =0  \forall i \in (1,3) $$

Solution for above only exist when

$$ \gamma_2 = −1.2264489 + 1.6410373 \gamma_1^2  $$


<p align="center"><img src="/assets/images/2021/Oct/FourMomentSimulation_Gamma.png"></p>


Finally, apply the transformation:

$$ G[\mu, \Sigma, \gamma_1, \gamma_2] = \mu + \sqrt{\Sigma} \times G[0, 1, \gamma_1, \gamma_2] $$

Let's take beta distribution for example with $\alpha$  = 4.5 and $\beta$ = 1. Let's also include a normal distribution with mean = $\mu$($\beta$($4.5,1$)), std = $\sigma$($\beta$($4.5,1$))


<p align="center"><img src="/assets/images/2021/Oct/FourMomentSimulation_Sim.jpg"></p>


Table:

| Stats | Beta | Normal | Simulation |
| :-------: | :---------: | :---------: | :---------: | 
| Mean | 0.817758 | 0.814272| 0.812858| 
| Std | 0.150223 |0.150879 | 0.156247|
| Skew | -1.108570| 0 | -1.221340|
| Kurt | 0.815587| 0 | 1.672359|



### Link:
[1] Hao Luo (2011). Generation of Non-normal Data – A Study of Fleishman’s Power Method. <a href = "https://www.diva-portal.org/smash/get/diva2:407995/FULLTEXT01.pdf"> here</a> <br/>
[2] Fleishman, A. I. (1978). A method for simulating non-normal distributions.Psychometrika. <a href = "https://link.springer.com/article/10.1007/BF02293811"> here</a>

