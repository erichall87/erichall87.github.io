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
Hawkes process we add robustness to model mismatch. This algorithm (Algorithm 1) is described in Section V-A of the [paper](http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=7469837). To test the importance of this method, we can compare the performance of directly calculating $$\mu(t)$$ from the observed
event times and known network, compared to doing some estimate which allows $$\mu(t)$$ to deviate slightly from an exact Hawkes process. An experiment of this type is described in Section VII-A of the paper and code to reproduce this experiment is found in `MismatchMain.m` in the GitHub [repo](https://github.com/erichall87/HawkesCode).
<center><img src = "{{ site.baseurl }}static/img/Fig1A.png" height = "200">
<img src = " {{site.baseurl }}static/img/Fig1B.png" height = "200">
<img src = " {{site.baseurl }}static/img/Fig1B.png" height = "200"></center>


### Learning the Underlying Network
Importantly, we want to not only estimate the rate at a given moment, but also to learn the underlying network. To this end we have created an algorithm which simultaneously estimats the network and rate (Algorithm 2, Section V-B), and code that mimics the experiments of Section VII-B is found in `HawkesSynthMain.m` in the [repo](https://github.com/erichall87/HawkesCode) 

<center><img src = "{{ site.baseurl }}static/img/Fig4A.png" height = "200"></center>
