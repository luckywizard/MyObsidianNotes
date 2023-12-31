.. _chap_notation:

Notation
========


Throughout this book, we adhere to the following notational conventions.
Note that some of these symbols are placeholders, while others refer to
specific objects. As a general rule of thumb, the indefinite article "a"
often indicates that the symbol is a placeholder and that similarly
formatted symbols can denote other objects of the same type. For
example, ":math:`x`: a scalar" means that lowercased letters generally
represent scalar values, but ":math:`\mathbb{Z}`: the set of integers"
refers specifically to the symbol :math:`\mathbb{Z}`.

Numerical Objects
-----------------

-  :math:`x`: a scalar
-  :math:`\mathbf{x}`: a vector
-  :math:`\mathbf{X}`: a matrix
-  :math:`\mathsf{X}`: a general tensor
-  :math:`\mathbf{I}`: the identity matrix (of some given dimension),
   i.e., a square matrix with :math:`1` on all diagonal entries and
   :math:`0` on all off-diagonals
-  :math:`x_i`, :math:`[\mathbf{x}]_i`: the :math:`i^\mathrm{th}`
   element of vector :math:`\mathbf{x}`
-  :math:`x_{ij}`, :math:`x_{i,j}`,\ :math:`[\mathbf{X}]_{ij}`,
   :math:`[\mathbf{X}]_{i,j}`: the element of matrix :math:`\mathbf{X}`
   at row :math:`i` and column :math:`j`.

Set Theory
----------

-  :math:`\mathcal{X}`: a set
-  :math:`\mathbb{Z}`: the set of integers
-  :math:`\mathbb{Z}^+`: the set of positive integers
-  :math:`\mathbb{R}`: the set of real numbers
-  :math:`\mathbb{R}^n`: the set of :math:`n`-dimensional vectors of
   real numbers
-  :math:`\mathbb{R}^{a\times b}`: The set of matrices of real numbers
   with :math:`a` rows and :math:`b` columns
-  :math:`|\mathcal{X}|`: cardinality (number of elements) of set
   :math:`\mathcal{X}`
-  :math:`\mathcal{A}\cup\mathcal{B}`: union of sets :math:`\mathcal{A}`
   and :math:`\mathcal{B}`
-  :math:`\mathcal{A}\cap\mathcal{B}`: intersection of sets
   :math:`\mathcal{A}` and :math:`\mathcal{B}`
-  :math:`\mathcal{A}\setminus\mathcal{B}`: set subtraction of
   :math:`\mathcal{B}` from :math:`\mathcal{A}` (contains only those
   elements of :math:`\mathcal{A}` that do not belong to
   :math:`\mathcal{B}`)

Functions and Operators
-----------------------

-  :math:`f(\cdot)`: a function
-  :math:`\log(\cdot)`: the natural logarithm (base :math:`e`)
-  :math:`\log_2(\cdot)`: logarithm with base :math:`2`
-  :math:`\exp(\cdot)`: the exponential function
-  :math:`\mathbf{1}(\cdot)`: the indicator function, evaluates to
   :math:`1` if the boolean argument is true and :math:`0` otherwise
-  :math:`\mathbf{1}_{\mathcal{X}}(z)`: the set-membership indicator
   function, evaluates to :math:`1` if the element :math:`z` belongs to
   the set :math:`\mathcal{X}` and :math:`0` otherwise
-  :math:`\mathbf{(\cdot)}^\top`: transpose of a vector or a matrix
-  :math:`\mathbf{X}^{-1}`: inverse of matrix :math:`\mathbf{X}`
-  :math:`\odot`: Hadamard (elementwise) product
-  :math:`[\cdot, \cdot]`: concatenation
-  :math:`\|\cdot\|_p`: :math:`\ell_p` norm
-  :math:`\|\cdot\|`: :math:`\ell_2` norm
-  :math:`\langle \mathbf{x}, \mathbf{y} \rangle`: dot product of
   vectors :math:`\mathbf{x}` and :math:`\mathbf{y}`
-  :math:`\sum`: summation over a collection of elements
-  :math:`\prod`: product over a collection of elements
-  :math:`\stackrel{\mathrm{def}}{=}`: an equality asserted as a
   definition of the symbol on the left-hand side

Calculus
--------

-  :math:`\frac{dy}{dx}`: derivative of :math:`y` with respect to
   :math:`x`
-  :math:`\frac{\partial y}{\partial x}`: partial derivative of
   :math:`y` with respect to :math:`x`
-  :math:`\nabla_{\mathbf{x}} y`: gradient of :math:`y` with respect to
   :math:`\mathbf{x}`
-  :math:`\int_a^b f(x) \;dx`: definite integral of :math:`f` from
   :math:`a` to :math:`b` with respect to :math:`x`
-  :math:`\int f(x) \;dx`: indefinite integral of :math:`f` with respect
   to :math:`x`

Probability and Information Theory
----------------------------------

-  :math:`X`: a random variable
-  :math:`P`: a probability distribution
-  :math:`X \sim P`: the random variable :math:`X` follows distribution
   :math:`P`
-  :math:`P(X=x)`: the probability assigned to the event where random
   variable :math:`X` takes value :math:`x`
-  :math:`P(X \mid Y)`: the conditional probability distribution of
   :math:`X` given :math:`Y`
-  :math:`p(\cdot)`: a probability density function (PDF) associated
   with distribution P
-  :math:`{E}[X]`: expectation of a random variable :math:`X`
-  :math:`X \perp Y`: random variables :math:`X` and :math:`Y` are
   independent
-  :math:`X \perp Y \mid Z`: random variables :math:`X` and :math:`Y`
   are conditionally independent given :math:`Z`
-  :math:`\sigma_X`: standard deviation of random variable :math:`X`
-  :math:`\mathrm{Var}(X)`: variance of random variable :math:`X`, equal
   to :math:`\sigma^2_X`
-  :math:`\mathrm{Cov}(X, Y)`: covariance of random variables :math:`X`
   and :math:`Y`
-  :math:`\rho(X, Y)`: the Pearson correlation coefficient between
   :math:`X` and :math:`Y`, equals
   :math:`\frac{\mathrm{Cov}(X, Y)}{\sigma_X \sigma_Y}`
-  :math:`H(X)`: entropy of random variable :math:`X`
-  :math:`D_{\mathrm{KL}}(P\|Q)`: the KL-divergence (or relative
   entropy) from distribution :math:`Q` to distribution :math:`P`

`Discussions <https://discuss.d2l.ai/t/25>`__