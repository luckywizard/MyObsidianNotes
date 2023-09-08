# 1D harmonic oscillator physics-informed neural network (PINN)

  

This notebook contains the code to reproduce the plots presented in my blog post ["So, what is a physics-informed neural network?"](https://benmoseley.blog/my-research/so-what-is-a-physics-informed-neural-network/).

  

Please read the post for more details!

  

## Problem overview

  

The example problem we solve here is the 1D damped harmonic oscillator:

$$

m \dfrac{d^2 x}{d t^2} + \mu \dfrac{d x}{d t} + kx = 0~,

$$

with the initial conditions

$$

x(0) = 1~~,~~\dfrac{d x}{d t} = 0~.

$$

We will focus on solving the problem for the under-damped state, i.e. when

$$

\delta < \omega_0~,~~~~~\mathrm{with}~~\delta = \dfrac{\mu}{2m}~,~\omega_0 = \sqrt{\dfrac{k}{m}}~.

$$

This has the following exact solution:

$$

x(t) = e^{-\delta t}(2 A \cos(\phi + \omega t))~,~~~~~\mathrm{with}~~\omega=\sqrt{\omega_0^2 - \delta^2}~.

$$

  

This problem was inspired by the following blog post: https://beltoforion.de/en/harmonic_oscillator/.

  

## Workflow overview

  

>First we will train a standard neural network to interpolate a small part of the solution, using some observed training points from the solution.

  

>Next, we will train a PINN to extrapolate the full solution outside of these training points by penalising the underlying differential equation in its loss function.

  
  

## Environment set up

  

We train the PINN using PyTorch, using the following environment set up:

```bash

  

conda create -n pinn python=3

conda activate pinn

conda install jupyter numpy matplotlib

conda install pytorch torchvision torchaudio -c pytorch

```
