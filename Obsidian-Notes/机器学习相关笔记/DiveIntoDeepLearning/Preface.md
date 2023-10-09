### Preface
Chris Bishop的优秀教科书 [[Bishop, 2006]](https://zh.d2l.ai/chapter_references/zreferences.html#bishop-2006) ，对每个主题都教得很透彻，以至于要读到线性回归这一章需要大量的工作。虽然专家们喜欢这本书正是因为它的透彻性，但对于初学者来说，这一特性限制了它作为介绍性文本的实用性。

Bishop, 1995

Bishop, C. M. (1995). Training with noise is equivalent to tikhonov regularization. _Neural computation_, _7_(1), 108–116.

Bishop, 2006

Bishop, C. M. (2006). _Pattern recognition and machine learning_. springer.

### 内容和结构[](https://zh.d2l.ai/chapter_preface/index.html#id6 "Permalink to this headline")

全书大致可分为三个部分，在 [图1](https://zh.d2l.ai/chapter_preface/index.html#fig-book-org) 中用不同的颜色呈现：

![../_images/book-org.svg](https://zh.d2l.ai/_images/book-org.svg)

图1 全书结构[](https://zh.d2l.ai/chapter_preface/index.html#id15 "Permalink to this image")

The book can be roughly divided into three parts, focusing on preliminaries, deep learning techniques, and advanced topics focused on real systems and applications ([Fig. 1](https://d2l.ai/chapter_preface/index.html#fig-book-org)).

![../_images/book-org.svg](https://d2l.ai/_images/book-org.svg)

Fig. 1 Book structure[¶](https://d2l.ai/chapter_preface/index.html#id5 "Permalink to this image")

-   第一部分包括基础知识和预备知识。 [1节](https://zh.d2l.ai/chapter_introduction/index.html#chap-introduction) 提供深度学习的入门课程。然后在 [2节](https://zh.d2l.ai/chapter_preliminaries/index.html#chap-preliminaries) 中，我们将快速向你介绍实践深度学习所需的前提条件，例如如何存储和处理数据，以及如何应用基于线性代数、微积分和概率基本概念的各种数值运算。 [3节](https://zh.d2l.ai/chapter_linear-networks/index.html#chap-linear) 和 [4节](https://zh.d2l.ai/chapter_multilayer-perceptrons/index.html#chap-perceptrons) 涵盖了深度学习的最基本概念和技术，例如线性回归、多层感知机和正则化。
    
-   接下来的五章集中讨论现代深度学习技术。 [5节](https://zh.d2l.ai/chapter_deep-learning-computation/index.html#chap-computation) 描述了深度学习计算的各种关键组件，并为我们随后实现更复杂的模型奠定了基础。接下来，在 [6节](https://zh.d2l.ai/chapter_convolutional-neural-networks/index.html#chap-cnn) 和 [7节](https://zh.d2l.ai/chapter_convolutional-modern/index.html#chap-modern-cnn) 中，我们介绍了卷积神经网络（convolutional neural network，CNN），这是构成大多数现代计算机视觉系统骨干的强大工具。随后，在 [8节](https://zh.d2l.ai/chapter_recurrent-neural-networks/index.html#chap-rnn) 和 [9节](https://zh.d2l.ai/chapter_recurrent-modern/index.html#chap-modern-rnn) 中，我们引入了循环神经网络(recurrent neural network，RNN)，这是一种利用数据中的时间或序列结构的模型，通常用于自然语言处理和时间序列预测。在 [10节](https://zh.d2l.ai/chapter_attention-mechanisms/index.html#chap-attention) 中，我们介绍了一类新的模型，它采用了一种称为注意力机制的技术，最近它们已经开始在自然语言处理中取代循环神经网络。这一部分将帮助你快速了解大多数现代深度学习应用背后的基本工具。
    
-   第三部分讨论可伸缩性、效率和应用程序。 首先，在 [11节](https://zh.d2l.ai/chapter_optimization/index.html#chap-optimization) 中，我们讨论了用于训练深度学习模型的几种常用优化算法。下一章 [12节](https://zh.d2l.ai/chapter_computational-performance/index.html#chap-performance) 将探讨影响深度学习代码计算性能的几个关键因素。在 [13节](https://zh.d2l.ai/chapter_computer-vision/index.html#chap-cv) 中，我们展示了深度学习在计算机视觉中的主要应用。在 [14节](https://zh.d2l.ai/chapter_natural-language-processing-pretraining/index.html#chap-nlp-pretrain) 和 [15节](https://zh.d2l.ai/chapter_natural-language-processing-applications/index.html#chap-nlp-app) 中，我们展示了如何预训练语言表示模型并将其应用于自然语言处理任务。