

Moseley, B., Markham, A., & Nissen-Meyer, T. (2021). [Finite Basis Physics-Informed Neural Networks (FBPINNs): a scalable domain decomposition approach for solving differential equations](https://arxiv.org/abs/2107.07871). _ArXiv_.

Moseley, B., Markham, A., & Nissen-Meyer, T. (2020). [Solving the wave equation with physics-informed deep learning](https://arxiv.org/abs/2006.11894). _ArXiv_.

## physics-informed neural networks (PINNs)求解微分方程
physics-informed neural networks (PINNs) have offered a powerful new paradigm for solving problems relating to differential equations. 

### 优势Compared to classical numerical methods PINNs have several advantages：
- 提供无网格微分方程解的能力以及在同一优化问题中进行正向和逆建模的能力。_their ability **to provide mesh-free solutions of differential equations**   and their ability to carry out forward and inverse modelling within the same optimisation problem. 

### 问题：
- 对于解决大域或多尺度计算方案中的问题。_a key limitation to date is that PINNs have struggled to accurately and efﬁciently solve problems with large domains and/or multi-scale solutions, which is crucial for their real-world application. 

__具体就是__：随着问题规模的增长，潜在的PINN优化问题日益复杂，以及神经网络的频谱偏差的问题。_Multiple signiﬁcant and related factors contribute to this issue, including the increasing complexity of the underlying PINN optimisation problem as the problem size grows and the spectral bias of neural networks.

__这篇文章的创新点：__
- 提出了一种新的、可伸缩的方法来解决与微分方程有关的大型问题。 _In this work we propose a new, scalable approach for solving large problems relating to differential equations called Finite Basis PINNs (FBPINNs)._
> [! important]-
> **有限基PINNS（FBPINNS）**
> FBPINNS受经典有限元法的启发，将微分方程的解表示为具有紧支集的有限基函数集的和。在FBPINNS中，神经网络被用来学习这些基函数，这些基函数被定义在小的、重叠的子域上。 FBINNS的设计是通过在每个子域上使用单独的输入归一化来解决神经网络的频谱偏差，并通过使用许多较小的神经网络以并行分而治之的方法来降低潜在优化问题的复杂性。_FBPINNs are inspired by classical ﬁnite element methods, where the solution of the differential equation is expressed as the sum of a ﬁnite set of basis functions with compact support. In FBPINNs neural networks are used to learn these basis functions, which are deﬁned over small, overlapping subdomains. FBINNs are designed to address the spectral bias of neural networks by using separate input normalisation over each subdomain, and reduce the complexity of the underlying optimisation problem by using many smaller neural networks in a parallel divide-and-conquer approach._

> [!question]-
> 什么叫可伸缩--scalable？

> [!summary]
我们的数值实验表明FBPINNS在解决小型和大型多尺度问题上都是有效的，在精度和所需计算资源方面都优于标准PINNS，为PINNS在大型现实问题上的应用铺平了道路。
 Our numerical experiments show that FBPINNs are effective in solving both small and larger, multi-scale problems, outperforming standard PINNs in both accuracy and computational resources required, potentially paving the way to the application of PINNs on large, real-world problems.




