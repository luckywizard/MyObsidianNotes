
https://zhuanlan.zhihu.com/p/31584464


https://blog.csdn.net/enjoy_pascal/article/details/81478582

[快速傅里叶变换（FFT）超详解 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/347091298)

https://blog.csdn.net/liyuanbhu/article/details/40925873

# GSL 学习笔记（快速傅立叶变换）

GNU Scientific Library (GSL)是一个开源的科学计算的函数库，里面实现了大量的数学函数，还提供了方程求解、傅立叶变换等多种功能。

GSL 中FFT 的定义如下，

正变换（forward）：
![[Pasted image 20220909111717.png]]
逆变换（inverse）：
![[Pasted image 20220909111804.png]]


还有一个叫做反向变换，反变换（backward）：
![[Pasted image 20220909111839.png]]


## 复数FFT，长度为2^N

这是最简单的一种。C89标准中没有定义复数类型，不过gsl 倒是给了个gsl_complex 类型。我们可以使用这个类型，或者直接实部虚部交替着放置。

下面是三个计算函数，都是在原位进行FFT计算，也就是计算结果仍然在 data 所指向的数据区。

```c
int gsl_fft_complex_radix2_forward (gsl complex packed array data, size t stride, size t n)
int gsl_fft_complex_radix2_backward (gsl complex packed array data, size t stride, size t n)
int gsl_fft_complex_radix2_inverse (gsl complex packed array data, size t stride, size t n)
```
还有一个既可以算正变换，也可以算逆变换。用法也很简单。

```c
int gsl_fft_complex_radix2_transform (gsl complex packed array data, size t stride, size t n, gsl fft direction sign)
```

因为用法非常简单，就不多说了，下面是个简单的算例。
```c
#include <stdio.h>
#include <math.h>
#include <gsl/gsl_errno.h>
#include <gsl/gsl_fft_complex.h>
 
#define REAL(z,i) ((z)[2*(i)])
#define IMAG(z,i) ((z)[2*(i)+1])
 
int
main (void)
{
    int i;
    double data[2*128];
 
    for (i = 0; i < 128; i++)
    {
        REAL(data,i) = 0.0;
        IMAG(data,i) = 0.0;
    }
 
    REAL(data,0) = 1.0;
 
    for (i = 1; i <= 10; i++)
    {
        REAL(data,i) = REAL(data,128-i) = 1.0;
    }
 
    for (i = 0; i < 128; i++)
    {
        printf ("%d %e %e\n", i,
                REAL(data,i), IMAG(data,i));
    }
    printf ("\n");
 
    gsl_fft_complex_radix2_forward (data, 1, 128);
 
    for (i = 0; i < 128; i++)
    {
        printf ("%d %e %e\n", i,
                REAL(data,i)/sqrt(128),
                IMAG(data,i)/sqrt(128));
    }
 
    return 0;
}
```


## 复数FFT，任意长度

用法也很简单。比如我们要计算N点的FFT。首先要先生成一个 wavetable
```c
gsl_fft_complex_wavetable *wavetable = gsl_fft_complex_wavetable_alloc (N);
```

然后还要分配workspace。
```c
gsl_fft_complex_workspace * workspace = gsl_fft_complex_workspace_alloc (N);
```

之后就可以具体的计算工作了。计算的结果还是原位存放。
```c
gsl_fft_complex_forward (data, stride, N, wavetable, workspace );
gsl_fft_complex_transform (data, stride, N, wavetable, workspace, sign);
gsl_fft_complex_backward  (data, stride, N, wavetable, workspace );
gsl_fft_complex_inverse  (data, stride, N, wavetable, workspace );
```

算完之后记得释放分配的空间。
```c
gsl_fft_complex_workspace_free (workspace);
gsl_fft_complex_wavetable_free (wavetable);
```

下面还是一个简单的例子：

```cpp

#include <stdio.h>
#include <math.h>
#include <gsl/gsl_errno.h>
#include <gsl/gsl_fft_complex.h>
 
#define REAL(z,i) ((z)[2*(i)])
#define IMAG(z,i) ((z)[2*(i)+1])
 
int main (void)
{
    int i;
    const int n = 630;
    double data[2*n];
    gsl_fft_complex_wavetable * wavetable;
    gsl_fft_complex_workspace * workspace;
 
    for (i = 0; i < n; i++)
    {
        REAL(data,i) = 0.0;
        IMAG(data,i) = 0.0;
    }
    data[0] = 1.0;
 
    for (i = 1; i <= 10; i++)
    {
        REAL(data,i) = REAL(data,n-i) = 1.0;
    }
 
    for (i = 0; i < n; i++)
    {
        printf ("%d: %e %e\n", i, REAL(data,i), IMAG(data,i));
    }
    printf ("\n");
 
    wavetable = gsl_fft_complex_wavetable_alloc (n);
    workspace = gsl_fft_complex_workspace_alloc (n);
 
    for (i = 0; i < wavetable->nf; i++)
    {
        printf ("# factor %d: %d\n", i,
                wavetable->factor[i]);
    }
    gsl_fft_complex_forward (data, 1, n, wavetable, workspace);
    for (i = 0; i < n; i++)
    {
        printf ("%d: %e %e\n", i, REAL(data,i), IMAG(data,i));
    }
 
    gsl_fft_complex_wavetable_free (wavetable);
    gsl_fft_complex_workspace_free (workspace);
    return 0;
 
}
```

实数FFT，长度为2^M
长度为2^M的实数向量的FFT得到是长度为2^M的共轭对称复数向量。由于是共轭对称的，因此理论上只需要2^M 个存储空间就可以存下。 所谓共轭对称指的是：
![[Pasted image 20220909112547.png]]

所以变换后，N元素只要知道前 N/2个元素的值就可以得到后面N/2个元素的值。

 

GSL 中采用的存储方式如下：

设数组长度为N，变换后，数据按照如下方式存放。
![[Pasted image 20220909112622.png]]

反变换时数据必须也按照这种方式存放。
>[!note]
>int gsl_fft_real_radix2_transform (double data[], size_t stride, size_t n)
int gsl_fft_halfcomplex_radix2_inverse (double data[], size_t stride, size_t n)
int gsl_fft_halfcomplex_radix2_backward (double data[], size_t stride, size_t n)

## 实数FFT，任意长度

当数据长度为任意长度时，GSL 库采用另外一种方式存储变换后的结果。这种存储方式与Paul Swarztrauber编写的fftpack 相同。

当N为偶数时，

complex[0].img = 0

complex[N/2].img = 0
![[Pasted image 20220909112747.png]]

当N为奇数时，complex[0].img = 0
![[Pasted image 20220909112818.png]]


上面的表格还是挺复杂的，GSL 还提供了两个辅助函数，帮我们转换数据格式。
```c
int gsl_fft_real_unpack (const double real_coefficient[], gsl_complex_packed_array complex_coefficient[], size_t stride, size_t n)
```

这个函数可以把实数数组转换为复数数组。之后就可以用复数fft 函数来计算了。
```c
int gsl_fft_halfcomplex_unpack (const double halfcomplex_coefficient[], gsl_complex_packed_array complex_coefficient, size_t stride, size_t n)
```


这个函数可以把 gsl_fft_real_transform 函数计算出的 half-complex 数组扩充为正常的复数数组。

不过GSL 没有提供将 gsl_fft_real_radix2_transform 计算结果展开的函数。如果需要，只能自己实现。

 

具体计算时与复数的fft 类似，正变换时按如下的顺序调用。
```c
gsl_fft_real_wavetable * gsl_fft_real_wavetable_alloc (size_t n);
gsl_fft_real_workspace * gsl_fft_real_workspace_alloc (size_t n);
 
int gsl_fft_real_transform (double data[], size_t stride, size_t n, const gsl_fft_real_wavetable * wavetable, gsl_fft_real_workspace * work);
 
void gsl_fft_real_workspace_free (gsl_fft_real_workspace * workspace);
gsl_fft_real_wavetable_free (gsl_fft_real_wavetable * wavetable);
```


逆变换时按如下的顺序调用。
```c
gsl_fft_halfcomplex_wavetable * gsl_fft_halfcomplex_wavetable_alloc (size_t n);
gsl_fft_real_workspace * gsl_fft_real_workspace_alloc (size_t n);
 
int gsl_fft_halfcomplex_transform (double data[], size_t stride, size_t n, const gsl_fft_halfcomplex_wavetable * wavetable, gsl_fft_real_workspace * work);
 
void gsl_fft_real_workspace_free (gsl_fft_real_workspace * workspace);
gsl_fft_halfcomplex_wavetable_free (gsl_fft_halfcomplex_wavetable * wavetable);
```


