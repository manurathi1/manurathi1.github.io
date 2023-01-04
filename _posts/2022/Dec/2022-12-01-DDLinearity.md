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

The CDaR risk function is based on CVaR concept and can be viewed as a modification of the CVaR to the case when the loss-function is defined as a drawdown. Similar to CVaR, i.e. average of all losses which is greater than equal to $\alpha$-VaR, CDaR is the average of all the drawdowns which are greater than equal to $\alpha$ drawdown at risk ( $\zeta_\alpha$ ) such that low CVaR ensures low VaR<br/>


> Risk functions are parameterized by weight matrix of the portfolio W, T is total time period considered for the calculation. sample path time horizon. 

\begin{equation}
\tag{1}
CDaR_\alpha(W) = \frac{1}{(1- \alpha)T} \int_{\Omega_\alpha}^{} D(W,t) \,dt
\end{equation}
where $ \Omega(W) = [ {t\varepsilon[0,T] : D(W,t) \geq \zeta_\alpha(W)} ] $




> By defination, with a specified probability $\alpha$, $\alpha$-DaR($\zeta_\alpha$) of a portfolio is the lowest amount such that probability that the drawdown will not exceed $\zeta_\alpha$ is greater than equal to $\alpha$   

We consider two risk functions that are special cases for CDaR: maximum drawdown (MaxDD) and average drawdown (AvDD) which are limiting cases for CDaR such that $$\alpha \to 1$$ and $$\alpha \to 0$$ respectively. 

\begin{equation}
\tag{2}
MaxDD(W) = \max_{t\varepsilon[0,T]}{D(W,t)}
\end{equation}

\begin{equation}
\tag{3}
AvDD(W) = \frac{1}{T} \int_{0}^{T} D(W,t) \,dt
\end{equation}

## Linear optimization:
### MaxDD:
we will consider the modification of classic optimization problem related to return risk efficient frontier. here we will maximize the return while constraining maximum drawdown to a pre-defined level. 

$$ \max_{W}{W^TR} $$

constrained on
$$ MaxDD(W) <= v_1C $$ <br/>


Where $$R$$ is a return matrix $$R =[r_1, r_2, r_3,...r_\gamma]; \gamma$$ is all constituents  and $$v_1$$ is percentage of the deployed capital $$C$$ allowed to be in drawdown.

Maximum drawdown is not Linear in terms of parameter $$W$$. It can be changed using auxiliary variable as follows:

\begin{equation}
\tag{4}
MaxDD(W) : \max_{k\varepsilon(0,T)}{DD_k} \leq v_1C
\end{equation}

\begin{equation}
\tag{5}
MaxDD(W) : \max_{k\varepsilon(0,T)}{((\max_{j\varepsilon(0,k)}{W^TR_j}) - W^TR_k)} \leq v_1C
\end{equation}

Converting the first maximum function in eq(5), using the property of maximum which apply constraint on each day to be less than the desired drawdown:

\begin{equation}
\tag{6}
MaxDD(W):(\max_{j\varepsilon(0,k)}{W^TR_j}) - W^TR_k \leq v_1C  \hspace{2mm} \forall\hspace{1mm} k\varepsilon[0,T]
\end{equation}


Converting second max function:

\begin{equation}
\tag{7}
MaxDD(W) : u_k- W^TR_k \leq v_1C  \hspace{2mm} \forall\hspace{1mm} k\varepsilon[0,T]
\end{equation}

where $$ u_k = \max_{j\varepsilon(0,k)}{(W^TR_j)} $$ is an auxiliary variable

Defining $u_k$ in eq(7) : <br/>
$u_k$ is equal to a maximum function hence it's an increasing function.
\begin{equation}
\tag{8}
u_k\geq u_{k-1}  \hspace{2mm} \forall\hspace{1mm} k\varepsilon[0,T] \hspace{2mm} with\hspace{1mm} u_0 = 0
\end{equation}

also $u_k$ should be equal to or greater than $W^TR_j$
\begin{equation}
\tag{9}
u_k\geq W^TR_j  \hspace{2mm} \forall\hspace{1mm}  j\varepsilon[0,k] ,\hspace{1mm} k\varepsilon[0,T] 
\end{equation}


\begin{equation}
\tag{10}
W_{min} \leq W \leq W_{max}
\end{equation}

So, the optimization converted to convex optimization problem with a linear performance function and piece-wise linear convex constraint given by maximization of return constrained on equations from (6) to (10). 

### CDaR:
 

$$ \max_{W}{W^TR} $$

constrained on
$$ CDaR_\alpha(W) <= v_2C $$ <br/>


Rewriting the eq(1):

\begin{equation}
\tag{11}
CDaR_\alpha(W) = \min_{\zeta}{[\zeta+\frac{\sum_{k\varepsilon(0,T)}[DD_k-\zeta]^+}{(1-\alpha)T}]}
\end{equation}

where function $$[x]^+$$ defined as $$max(0,x)$$

CDaR constraint function can be converted to linear as follows:


\begin{equation}
\tag{12}
\zeta+\frac{\sum_{k\varepsilon(0,T)}z_k}{(1-\alpha)T}
\end{equation}

Defining $$ z_k $$:

$$ z_k = [DD_k-\zeta]^+ $$

as $$ z_k $$ is the positive part
\begin{equation}
\tag{13}
z_k \geq DD_k - \zeta \hspace{4mm} \forall \hspace{1mm} k\varepsilon[0,T]
\end{equation}

using eq(7) $$ DD_k $$ can be written in from of $$u_k$$
\begin{equation}
\tag{14}
z_k \geq u_k - W^TR_k - \zeta \hspace{4mm} \forall \hspace{1mm} k\varepsilon[0,T]
\end{equation}

as $$z_k$$ is always positive 
\begin{equation}
\tag{15}
z_k \geq 0
\end{equation}

Similar to MaxDD, Optimization problem converted to maximization of return constrained on equations (14), (15) and from (8) to (10).






