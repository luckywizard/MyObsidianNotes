## Is Deep better than Shallow?

How many neurons are needed to approximate $f(x)$?

The function space defined by the network with K neurons:  
$$  
f_m \in N(K)  
$$

Given a small number $\varepsilon$, What is the number of 𝐾 such that  
$$  
\exists f_m \in N(K), \operatorname*{max}_{0\leq{x\leq{1}} }{|f(x) - f_m(x)|}\leq{\varepsilon}  
$$

the difference between $f(x)$ and $f_m(x)$ is smaller than $\varepsilon$

All the functions in $N(K)$ are piecewise linear, Approximate $𝑓^∗$ by a piecewise linear function $f$.

$$  
L-Lipschitz function 𝑓^*:  
||f_1(x) - f_2(x)|| \leq{L \times|| x_1 - x_2||}  
$$

How to make the errors$\leq {\varepsilon}$?  
𝑙 × 𝐿 ≤ 𝜀, 𝑙 ≤ 𝜀/𝐿

### [](http://127.0.0.1:3334/mdEditor/#lower-bound-of-linear-pieces)Lower Bound of Linear Pieces

If K is width, H is depth : We can have at least $K^H$ pieces

```
Razvan Pascanu, Guido Montufar, Yoshua Bengio, “On the number of response regions of deep feed forward networks with piece-wise linear activations”, ICLR, 2014
Guido F. Montufar, Razvan Pascanu, Kyunghyun Cho, Yoshua Bengio, “On the Number of Linear Regions of Deep Neural Networks”, NIPS, 2014
Raman Arora, Amitabh Basu, Poorya Mianjy, Anirbit Mukherjee, “Understanding Deep Neural Networks with Rectified Linear Units”, ICLR 2018
Thiago Serra, Christian Tjandraatmadja, Srikumar Ramalingam, “Bounding and Counting Linear Regions of Deep Neural Networks”, arXiv, 2017
Maithra Raghu, Ben Poole, Jon Kleinberg, Surya Ganguli, Jascha Sohl-Dickstein, On the Expressive Power of Deep Neural Networks, ICML, 2017

```

#### [](http://127.0.0.1:3334/mdEditor/#example)example:

$$ f(x)=x^2 $$

Fit the function by equally spaced linear piece:

$f_m(x)$: a function with $2^m$ pieces

$$  
\operatorname*{max}_{0\leq{x\leq{1}} }{|f(x) - f_m(x)|}\leq{\varepsilon}  
$$

What is the minimum m?  
$$  
m \geq{-\cfrac{1}{2}\log_2{\varepsilon} - 1}  
$$

$$  
2^m \geq{\cfrac{1}{2}\cfrac{1}{\sqrt{\varepsilon}}}pieces  
$$

shallow: $ O(\cfrac{1}{\sqrt{\varepsilon}}) $ neurons  
deep:  
𝑂(𝑚) neurons, 𝑂(𝑚) layers  
$ O(\log_2{\cfrac{1}{\sqrt{\varepsilon}}} )$ neurons

## [](http://127.0.0.1:3334/mdEditor/#best-of-shallow)Best of Shallow

Use Euclidean: $ \sqrt{\int_0^1{|f(x) - f*(x)|2,{\rm d} x}}$

Given a piece, what is the smallest error.  
$$  
e^2 = \int_{x_0}^{x_0+l}{ (x^2 - (ax+b))^2 , {\rm d}x}  
$$  
Find $a$ and $b$ to minimize $e^2$

$$  
f_v = x^2, , f_w = x, f_u = 1  
$$

Minimize: $|| \vec{v} - (a\vec{w} - b\vec{u})||$

Minimize: $|| \vec{f_v} - (a\vec{f_w} - b\vec{f_u})||$

The minimum value of $e^2$ is $\cfrac{l^5}{180}$

Holder/s inequality:  
Given ${a_1,a_2,...,a_n}$ and ${b_1,b_2,...,b_n}$  
$$  
\sum_{i=1}^{n}{|a_ib_i|} \leq {\left( \sum_{i=1}{n}{|a_i|p} \right)^{1/p} \left( \sum_{i=1}{n}{|b_i|q} \right)^{1/q}}  
$$

$$  
\cfrac{1}{p} + \cfrac{1}{q} = 1  
$$  
Given ${l_1,l_2,...,l_n}$ and ${1,1,...,1}$  
$$  
\sum_{i=1}^{n}{l_i} \leq {\left( \sum_{i=1}{n}{|l_i|p} \right)^{1/p} \left( \sum_{i=1}{n}{|1|q} \right)^{1/q}}  
$$

A function expressible by a 3-layer feedforward network cannot be approximated by 2-layer network.  
• Unless the width of 2-layer network is VERY large  
• Applied on activation functions beyond relu

The width of 3-layer network is K.  
The width of 2-layer network should be 𝐴𝑒𝐵𝐾4/19$ Ae{BK{4/19}} $

```
Ronen Eldan, Ohad Shamir, “The Power of Depth for Feedforward Neural Networks”, COLT, 2016

Matus Telgarsky, “Benefits of depth in neural networks”, COLT, 2016

Itay Safran, Ohad Shamir, “Depth-Width Tradeoffs in Approximating Natural Functions with Neural Networks”, ICML, 2017

Dmitry Yarotsky, “Error bounds for approximations with deep ReLU networks”,arXiv, 2016

Dmitry Yarotsky, “Optimal approximation of continuous functions by very deep ReLU networks”, arXiv 2018

Shiyu Liang, R. Srikant, “Why Deep Neural Networks for Function Approximation?”, ICLR, 2017

Itay Safran, Ohad Shamir, “Depth-Width Tradeoffs in Approximating Natural Functions with Neural Networks”, ICML, 2017

```

If a function f has “certain degree of complexity” Approximating f to accuracy 𝜀 in the L2 norm using a fixed depth ReLU network requires at least 𝑝𝑜𝑙𝑦 1/𝜀 There exist a ReLU network of depth and width at most 𝑝𝑜𝑙𝑦 𝑙𝑜𝑔 1/𝜀 that can achieve the approximation

## [](http://127.0.0.1:3334/mdEditor/#hessian-matrix-when-gradient-is-zero)Hessian Matrix: When Gradient is Zero

local minima  
global minima  
critical point  
saddle point

### [](http://127.0.0.1:3334/mdEditor/#at-critical-point-hessian)At critical point: Hessian

### [](http://127.0.0.1:3334/mdEditor/#degenerate)Degenerate

-   Degenerate Hessian has at least one zero eigen value  
    存在某个方向的增量为0。这个点有可能是
    -   local minima
    -   local maxima
    -   saddle point

```
Kenji Kawaguchi, Deep Learning without Poor Local Minima, NIPS, 2016
Haihao Lu, Kenji Kawaguchi, Depth Creates No Bad Local Minima, arXiv, 2017
Thomas Laurent, James von Brecht, Deep linear neural networks with arbitrary loss: All local minima are global, arXiv, 2017
Maher Nouiehed, Meisam Razaviyayn, Learning Deep Models: Critical Points and Local Openness, arXiv, 2018
```

### [](http://127.0.0.1:3334/mdEditor/#under-some-conditions-initialization-data-we-can-find-global-optimal)Under some conditions (initialization, data, ……),We can find global optimal.

```
Grzegorz Swirszcz, Wojciech Marian Czarnecki, Razvan Pascanu, “Local minima in training of neural networks”, arXiv, 2016
Itay Safran, Ohad Shamir, “Spurious Local Minima are Common in Two-Layer ReLU Neural Networks”, arXiv, 2017
Yi Zhou, Yingbin Liang, “Critical Points of Neural Networks: Analytical Forms and Landscape Properties”, arXiv, 2017
Shai Shalev-Shwartz, Ohad Shamir, Shaked Shammah, “Failures of Gradient-Based Deep Learning”, arXiv, 2017

```

Almost all local minimum have very similar loss to the global optimum, and hence finding a local minimum is good enough.