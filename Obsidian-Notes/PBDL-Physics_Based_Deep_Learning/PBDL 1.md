## Coming up

As a _sneak preview_, the next chapters will show:

- How to train networks to infer a fluid flow around shapes like airfoils, and estimate the uncertainty of the prediction. This gives a _surrogate model_ that replaces a traditional numerical simulation.

- How to use model equations as residuals to train networks that represent solutions, and how to improve upon these residual constraints by using _differentiable simulations_.

- How to more tightly interact with a full simulator for _inverse problems_. E.g., we'll demonstrate how to circumvent the convergence problems of standard reinforcement learning techniques by leveraging simulators in the training loop.

- We'll also discuss the importance of _inversion_ for the update steps, and how higher-order information can be used to speed up convergence, and obtain more accurate neural networks.
如何训练网络来推断翼型等形状周围的流体流动，并估计预测的不确定性。这提供了一个替代模型，取代了传统的数值模拟。如何使用模型方程作为残差来训练表示解的网络，以及如何通过使用可微模拟来改进这些残差约束。如何更紧密地与反问题的完整模拟器交互。例如，我们将演示如何通过利用训练循环中的模拟器来规避标准强化学习技术的收敛问题。我们还将讨论反转对更新步骤的重要性，以及如何使用高阶信息来加速收敛，并获得更准确的神经网络。

Throughout this text,we will introduce different approaches for introducing physical models into deep learning, i.e., _physics-based deep learning_ (PBDL) approaches.
These algorithmic variants will be introduced in order of increasing
tightness of the integration, 

and **the pros and cons of the different approaches will be discussed. It's important to know in which scenarios each of the different techniques is particularly useful.**


  >[!note]
  >We focus on Jupyter notebooks, a key advantage of which is that all code examples
can be executed _on the spot_, from your browser. You can modify things and 
immediately see what happens -- give it a try by 
[[running this teaser example in your browser]](https://colab.research.google.com/github/tum-pbs/pbdl-book/blob/main/intro-teaser.ipynb).
Plus, Jupyter notebooks are great because they're a form of [literate programming](https://en.wikipedia.org/wiki/Literate_programming).


## Citation

If you find this book useful, please cite it via:
```
@book{thuerey2021pbdl,
  title={Physics-based Deep Learning},
  author={Nils Thuerey and Philipp Holl and Maximilian Mueller and Patrick Schnell and Felix Trost and Kiwon Um},
  url={https://physicsbaseddeeplearning.org},
  year={2021},
  publisher={WWW}
}
```

