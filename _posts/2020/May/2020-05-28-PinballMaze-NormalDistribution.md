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
<!-- [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/googlecolab/colabtools/blob/master/notebooks/colab-github-demo.ipynb) -->

## Problem Statement
Imagine Pinball and a maze like this, Now one has to put the balls in the maze for a number of times let's say this "N". there are few assumption: 1. No ball will be out of the container placed below 2. At each pin (dot in the figure) ball has only two options : either (left/right). 
we have to guess if we do this for a large number of times 
$$ N\rightarrow\infty $$ what will be distriution of the balls ( frequency of balls in each container)

![no-alignment]({{ site.url }}{{ site.baseurl }}/assets/images/pinball.png)


## Simulation
Let's try to simulate the situation in python

```python
#function for simulating one throw 
def oneThrow(numOfLayers):
  # generate left(-1) / right(+1) using binomial distribution equal probability
  bernoulliNumbers = np.random.binomial(1, 0.5, numOfLayers)
  decideNumbers = (lambda Arr : [-1 if x == 0 else 1 for x in Arr])(bernoulliNumbers)
  # final container slot 
  finalContainerSlot = 0
  for decide in decideNumbers:
    finalContainerSlot += decide 
  return decideNumbers,finalContainerSlot

```
numberOfLayers = 100, 
numberOfThrows = 10000

```python
finalContainerSlotArr = [ oneThrow(numberOfLayers)[1] for i in range(numberOfThrows)]
```