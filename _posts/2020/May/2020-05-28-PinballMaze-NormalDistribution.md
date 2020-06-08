---
title: "Pinball Maze"
categories:
  - Maths
tags:
  - Normal Distribution
  - Binomial Distribution
  - Probability 

# comments: true

--- 
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/googlecolab/colabtools/blob/master/notebooks/colab-github-demo.ipynb)

## Problem Statement
Imagine Pinball and a maze like this, Now one has to put the balls in the maze for a number of times let's say this "N". there are few assumption: 1. No ball will be out of the container placed below 2. At each pin (dot in the figure) ball has only two options : either (left/right). 
we have to guess if we do this for a large number of times 
$$ N\rightarrow\infty $$

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/pinball.png)


## Guess?
This is a classic example to describe normal distribution (approximate normality). Easiest way to prove this,is to think each container slot below as a random variable $$ X $$ which can either have a ball $$ X = 1 $$ or not $$ X = 0 $$.



