

A radial basis function (RBF) is a mathematical function that maps the distance between two points in a multi-dimensional space to a scalar value. The RBF is typically used as a basis function in various machine learning and optimization algorithms.

The RBF is defined as:
$$ \phi(r) = \exp(-\gamma r^2)$$

where r is the distance between two points in the multi-dimensional space, $\gamma$ is a parameter that determines the width of the RBF, and exp() is the exponential function.

The RBF has a bell-shaped curve that decreases rapidly as the distance between two points increases. This means that the RBF assigns high values to points that are close together and low values to points that are far apart.

The RBF is often used in machine learning algorithms such as support vector machines (SVMs) and k-means clustering. In SVMs, the RBF is used as a kernel function to transform the input data into a higher-dimensional space where it can be more easily separated. In k-means clustering, the RBF is used to measure the distance between data points and cluster centers.

Overall, the RBF is a useful tool for modeling complex data that cannot be easily separated by linear functions. Its ability to capture non-linear relationships between data points makes it a popular choice in many machine learning applications.

径向基函数是一个取值仅仅依赖于离原点距离的实值函数，也就是 $\phi = \phi(\lVert x \rVert)$ ,或者还可以是到任意一点c的距离，c点称为中心点，也就是$\phi(x,c) = \phi(\lVert x-c \rVert)$。任意一个满足$\phi(x) = \phi(\lVert x \rVert)$ 特性的函数Φ都叫做径向基函数，标准的一般使用欧氏距离（也叫做欧式径向基函数），尽管其他距离函数也是可以的。

