物理信息神经网络（Physics-informed Neural Networks, PINNs）作为一种强形式的无网格方法，在各个领域有了很多发展，产出了很多文章。总所周知，弱形式对解空间需求更低，可以估出各种Bound，对应的也有类似PINN的深度学习求解方法，比如今天讲一个DeepRitz方法：

> Weinan, E.; Yu, B. The Deep Ritz Method: A Deep Learning-Based Numerical Algorithm for Solving Variational Problems. _Communications in Mathematics and Statistics_ **2018**, _6_ (1), 1–12.  

是跟PINN（17年底挂在Arxiv上）几乎同一时期甚至还早一点的工作，可能数学形式稍微复杂了一点点，火爆度是不如Raissi的PINN了。也侧面说明影响大的工作的形式一定得非常简单，高中生都能看懂使用发paper

https://zhuanlan.zhihu.com/p/584419137