---
title: "Drawdown and it's Linearity"
# categories:
#   - maths
excerpt: "Conditional Drawdown at risk, special cases and it's linearity using auxiliary variable " 
tags:
  - Optimization 
  - Risk

# comments: true

--- 
<!-- [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1OonMdRn8GxvdiRFQ17sm2d0qyiLISxyS?usp=sharing) -->

In this article we will first disucss the conditional drawdown at risk (CDaR), it's special cases, maximum drawdown and average drawdown. then we will move to the optimization problem for return CDaR efficient frontier. 

### Assumption:
This approach concentrate on the portfolio equity curves over a particular sample-path (historical or most probable future sample-path), i.e. we define some sample-path risk function rather than a risk measure on set of sample-paths. Making no assumption about the underlying probabilty distribution which unlocks various practical application.

## CDaR:
For some value of the confidence parameter $\alpha$, the $\alpha$-CDaR is defined as the mean of the worst (1−$\alpha$)∗100% drawdowns experienced over some period of time on a sample-path. <br/>

The CDaR risk function is based on CVaR concept and can be viewed as a modification of the CVaR to the case when the loss-function is defined as a drawdown. Similar to CVaR, i.e. average of all losses which is greater than equal to $\alpha$-VaR, CDaR is the average of all the drawdowns which are greater than equal to $\alpha$ drawdown at risk ( $\zeta_\alpha$ ) <br/>

> Risk functions are parameterized by weights of the portfolio W, T is total time period considered for the calculation. sample path time horizon. 

\begin{equation}
\tag{1}
CDaR_\alpha(W) = \frac{1}{(1- \alpha)T} \int_{\Omega_\alpha}^{} D(W,t) \,dt
\end{equation}
where $ \Omega(W) = [ {t\varepsilon[0,T] : D(W,t) \geq \zeta_\alpha(W)} ] $




> By defination, with a specified probability $\alpha$, $\alpha$-DaR($\zeta_\alpha$) of a portfolio is the lowest amount such that probability that the drawdown will not exceed $\zeta_\alpha$ is greater than equal to $\alpha$   

We consider two risk functions that are special cases for CDaR: maximum drawdown (MaxDD) and average drawdown (AvDD) define as: 

\begin{equation}
\tag{2}
MaxDD(W) = \max_{t\varepsilon[0,T]}{D(W,t)}
\end{equation}

$$ AvDD(W) = \frac{1}{T} \int_{0}^{T} D(W,t) \,dt $$

# WIP