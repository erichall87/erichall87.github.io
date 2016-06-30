---
layout: post
title: Hawkes Code
---


# <center>Dynamic Mirror Descent [<a href="https://arxiv.org/abs/1307.5944">arXiv 1307.5944</a>]</center>

### DMD for Dynamic Textures
Dynamic Mirror Descent can be used to create predictions of the hidden state of a system in an autoregressive model, which obeys the following update equations:

$$\begin{align}
x_t & =  C_0 + C \theta_t + w_t \\
\theta_{t+1} & =  A \theta_t + B u_t \\
w_t & \sim  \mathcal{N}(0,R), u_t \sim \mathcal{N}(0, Q)
\end{align}$$

where $$x_t$$ are the observations, $$C$$ is the sensing matix, $$\theta_t$$ is the hidden state of the system, and $$A$$ is the matrix which encodes the linear evolution of the system. The provided code has a function `DMD_Autoregressive.m` which takes in observations and parameters of the system and produces estimates of $$\theta_t$$.
<center><img src = "{{ site.baseurl }}static/img/dynamic_textures_image.png" height = "200"></center>

&nbsp;
A script, called `DynamicTexturesExamples.m` shows how this function is used by generating synthetic dynamic texture data from parameters stored in `Water_params_forward.mat` and `Water_params_backward.mat`.
<center><img src = "{{ site.baseurl }}static/img/Instant_loss_textures.png" height = "200"></center>


Fork the repo [here](https://github.com/erichall87/DMD_Autoregressive).

### DMD for Compressed Sensing

Dynamic Mirror Descent can be used to recover signals which have been undersampled according to the compressed sensing paradigm:

$$\begin{align}
x_t  = A_t \theta_t + n_t \\
x_t \in \mathbb{R}^d, \theta_t \in \mathbb{R}^n \\
A_t \in \mathbb{R}^{d\times n}, d << n
\end{align}$$

where $$x_t$$ are the observations, $$\theta_t$$ is the signal of interest, and $A_t$ is the sensing matrix. The goal of compressed sensing is to recover the signal with only a small number of measurements and the added knowledge that the signal is sparse in some basis. DMD is used in this setting when the signal may be changing in time according to some dynamical model.

The script `CompressedSEnsingExample.m` generates 1000 time instances of a dynamically changing scene and attempts to recover the scene using DMD and its variant Dynamic Fixed Share (DFS).

<center><img src = " {{ site.baseurl }}static/img/CS_image_eg.png" height = "350"></center>

Fork the repo [here](https://github.com/erichall87/DMD_CompressedSensing)

### DMD with Additive Dynamics in Exponential Families

DMD with additive dynamics in exponential families (DMD Exp) can be used to simultaneously predict the likelihood of an agent acting in a network at a given moment in time and estimate the structure the network. Assuming a model of the form

$$\begin{align}
x_t  & \sim {\rm{Poisson}}(\mu_t)\\
\mu_{t+1} & = \tau \mu_t + W x_t + (1-\tau) \bar{\mu}
\end{align}$$

where $$x_t$$ are the observed counts from each actor, $$\mu_t$$ are the time varying rates for each actor, and $W$ is a matrix which encodes the amount of influence each actor has on the rest of the network.

The function `DMD_Self_Excite.m` take in observations, and parameters of the dynamics and ouputs the time varying estimate of the intensities and the network structure. The script `NeuronSpikeExample.m` gives an example of how the function can be used.

<center><img src = "{{ site.baseurl }}static/img/Network_estimates.png" height = "200"></center>
&nbsp;

Fork the repo [here](https://github.com/erichall87/DMD_Exp).
