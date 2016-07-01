---
layout: post
title: Hawkes Code
---


# <center><a href="http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=7469837">Tracking Dynamic Point Processes on Networks</a> [<a href="https://arxiv.org/abs/1409.0031">arXiv 1409.0031</a>]</center>

### Hawkes Process
The Hawkes process is a multivariate, autoregressive point process defined with the following time-varying intensity function for node $$k$$ in the network:

$$\begin{align}
\mu_k(t) = \mu + \sum_{n=1}^t h_{k,k_{n}}(t - \tau_n)
\end{align}$$

where $$\tau_n$$ is the time of the $$n^{th}$$ event time and $$k_n$$ is the node involved in the $$n^{th}$$ event. We are interested in 
learning relationships between nodes in the network, and to that end we assume the function $$h_{i,j}(t) = W_{i,j} h(t)$$ for some matrix $$W$$ and 
the "influence function" $$h(t)$$. Thus we are interested in learning the values of $$W$$. Our paper and methods aim to learn values of this matrix while simultaneously generating time-evolving estimates of $$\mu (t)$$ in a fast, online framework.

A repo of code to reproduce some experiments and to use our Online Hawkes method can be found [here](https://github.com/erichall87/HawkesCode)

### Comparing Our Method to Direct Calculation
A key aspect of our method is the simulataneous estimate of not only the underlying network, but also the rates. 
By estimating the rates as opposed to just estimating the network and plugging the network in the definition of the 
Hawkes process we add robustness to model mismatch. This algorithm is described in Section V-A of the [paper](http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=7469837).
<center><img src = "{{ site.baseurl }}static/img/Fig1A.png" height = "200">
<img src = " {{site.baseurl }}static/img/Fig1B.png" height = "200">
<img src = " {{site.baseurl }}static/img/Fig1B.png" height = "200"></center>

Code to reproduce this experiment is found in `MismatchMain.m` in the GitHub [repo](https://github.com/erichall87/HawkesCode).


