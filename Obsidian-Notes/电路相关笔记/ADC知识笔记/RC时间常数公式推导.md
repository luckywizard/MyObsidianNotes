
RC滤波电路里的时间常数


## RC电路
![[Pasted image 20221109210207.png]]

> [!note] 
> 电容的电荷$q=C\times u$； 
> 流过电容的电流：$$i = \cfrac{\mathrm{d}q}{\mathrm{d}t} = \cfrac{\mathrm{d}(Cu)}{\mathrm{d}t} = C {{\mathrm{d}u} \over {\mathrm{d}t}}$$

这时候假设初始状态开关未闭合，这时候电容C两端的电压为0V； 开关闭合后的时间t时刻，由于蓄电池U一直在给电容充电，这时候电容的电荷为：
$$
q(t)=\int_0^ti\mathrm{d}t
$$

$$
u(t) = {1 \over c}\int_0^ti\mathrm{d}t
$$
根据电路的基尔霍夫电压定律(KVL：沿任一回路的，所有支路电压的点数和恒等于零)，电容充电的过程中，电流的方向是顺时针，列出方程如下：
$$
\begin{array}{c}
U=Ri+u(t) \\
u(t)=U-Ri=U-RC{ \dfrac{du}{dt} }

\end{array}
$$
非齐次一阶微分方程
$$
u(t)=U\times \Big(1-e^{(-\dfrac{t}{RC})} \Big)
$$

