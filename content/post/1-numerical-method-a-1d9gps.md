
# 1 数值方法A

## 课堂笔记

### 基础

主要是针对N-S方程求解，有三种方法：有限体积、有限元、有限差分。

微分：

$$
\underset{\Delta x \to 0}{lim} \frac{f(x_0+\Delta x)-f(x_0)}{\Delta x}=\frac{dy}{dx}
$$

​![360albumviewer_imgproc_1712893765](https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/360albumviewer_imgproc_1712893765-20240924164238-6pripo5.png)  

不同尺度下物质密度：分子尺度$l_m$<<连续体$\eta$<<地理尺度L（教室、地球...）

​![Screenshot_2024-09-24-16-55-30-031_com.jideos.jnotes](https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/Screenshot_2024-09-24-16-55-30-031_com.jideos.jnotes-20240924165620-4nfeuh2.png)本课程研究连续体尺度的问题。

### 一维稳态扩散及其求解

#### 一维动量守恒

$$
-\frac{dp}{dx}=\rho u \frac{du}{dx}=\rho \frac{d(\frac{u^2}{2})}{dx}
$$

其中，$-\frac{dp}{dx}$是压力梯度，$\rho u$代表质量流量，$\frac{du}{dx}$表示速度梯度，$\frac{d(\frac{u^2}{2})}{dx}$表示动能梯度。

进一步推导：

$$
\int_{x_1}^{x_2} -dp=\int_{x_1}^{x_2} \rho d(\frac{1}{2}u^2)
$$

$$
\int_{p_1}^{p_2} -dp=\int_{u_1}^{u_2} \rho d(\frac{1}{2}u^2)
$$

$$
p_1-p_2=\frac{1}{2}\rho (u_2^2-u_1^2)
$$

即伯努利方程。

#### 一维稳态扩散

$$
\frac{d}{dx} (\Gamma \frac{d \phi}{dx})+S(x,~\phi)=0
$$

扩散：任何物质（粒子、能量、动量...）由高浓度区域向低浓度区域传输，由浓度梯度驱动，无大规模物质对流。

式中：

* $\phi$表示待求的量（如温度、浓度、电势）；
* $\Gamma$表示扩散系数，$\frac{d}{dx} (\Gamma \frac{d \phi}{dx})$是扩散项，表示待求量扩散的速度和系数随着空间x变化；
* S表示源项（生成）或耗散项（消耗），与空间x、变量$\phi$相关，代表在系统中出现的额外影响。

稳态：$\frac{\partial}{\partial t}=0$，时间不再影响$\phi$的变化，扩散过程已经达到平衡。

应用：

1. 剪应力的跨流扩散

    $$
    \frac{d}{dx}(\mu \frac{du}{dx})-\frac{dp}{dy}=0
    $$

    ​![Screenshot_2024-09-24-19-47-07-378_com.jideos.jnotes](https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/Screenshot_2024-09-24-19-47-07-378_com.jideos.jnotes-20240924201738-3kgjj66.png)​

    式中：

    * $\mu$是**动态粘度**，描述流体的剪切变形对剪应力的响应，反映了流体的**粘性**，是纯物质属性，单位$N\cdot s/m^2$；
    * v（这里未出现）是动力粘度，是动态粘度与流体密度的比值，反映了流体在**重力作用下的扩散性**；
    * $\frac{du}{dx}$表示速度梯度，反映了流体层之间的速度差异，$\frac{d}{dx}(\mu \frac{du}{dx})$代表剪应力的扩散；
    * $\frac{dp}{dy}$是压力梯度，表示驱动流动的压力差，作为动量的来源。当流动完全发展时，$\frac{dp}{dy}=0$；

    稳态：速度场和压力场不随时间变化；

    描述层流条件下的粘性流体，在粘性影响下，流体的各层相对滑动，产生剪应力。

#### 一维稳态扩散的应用2：经壁热传导

1. 公式：

$$
\frac{d}{dx}(\lambda \frac{dT}{dx})+S(x,~T)=0
$$

​![Screenshot_2024-09-24-20-36-48-831_com.jideos.jnotes](https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/test/Screenshot_2024-09-24-20-36-48-831_com.jideos.jnotes-20240924203830-uyywlaj.png)  
式中，$\lambda$为热导率，S代表系统中额外的热源/热汇。

边界条件：若绝热（adiabatic），$\frac{\partial T}{\partial x}=0$。

2. 如何求数值解

基本思路是离散化，目标是化为如下形式：

$$
\left\{\begin{matrix}a_{1,~1}T_1+a_{1,~2}T_2+...+a_{1,~n}T_n
 \\...
 \\a_{n,~1}T_1+a_{n,~2}T_2+...+a_{n,~n}T_n
\end{matrix}\right.\Longrightarrow 
[A][T]=[B]
$$

​![image](https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/test/image-20240924205135-bmsqqog.png)​

如图所示，在x=0到x=L的空间内取n个点测温。注意，点1在左边墙上，点n在右边墙上（即边界条件）。

这里有：

$$
\Delta x=\frac{L-0}{n-1}
$$

$$
\frac{dT}{dx}\mid_i~\approx \frac{T_{i+1}-T_i}{\Delta x} \approx \frac{T_{i+1}-T_{i-1}}{2\Delta x}
$$

离散化的具体实现：使用有限体积法，将整个域离散为n个控制体积（control volume，CV）。

​![image](https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/image-20240924221516-z6z1bxe.png)​

原公式如下：

$$
\frac{d}{dx}(\lambda \frac{dT}{dx})+S(x,~T)=0
$$

根据控制体积，对上式进行积分，则有：

$$
\int_v \frac{d}{dx}(\lambda \frac{dT}{dx})dV+\int_v S(x,~T)dV=0
$$

​![Screenshot_2024-09-24-22-27-39-350_com.jideos.jnotes](https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/nullScreenshot_2024-09-24-22-27-39-350_com.jideos.jnotes-20240924223221-14ja6kl.png)​

​![IMG_20240924_223429](https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/IMG_20240924_223429-20240924223457-zegtbur.jpg)​

参见上图，有$dV=Adx$，则：

$$
\int_w^e \frac{d}{dx}(\lambda \frac{dT}{dx})Adx+\int_w^e S(x,~T)Adx=0
$$

这里W意为west，E意为east。

​![Screenshot_2024-09-24-22-37-40-219_com.jideos.jnotes](https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/nullScreenshot_2024-09-24-22-37-40-219_com.jideos.jnotes-20240924223754-4lgyahv.png)​

如图，设对阴影部分积分。

$$
\int_a^b f(x)dx=f[a+\xi(b-a)]\cdot(b-a)
$$

其中$\xi$是0~1之间的任意常数。

又有$\int \frac{df(x)}{dx}dx=f(x)$，则方程可化为：

$$
[\lambda\frac{dT}{dx}]_{w}^{e}+\bar{S}[x]_w^e=0
$$

$$
(\lambda \frac{dT}{dx})_e-(\lambda \frac{dT}{dx})_w+\bar{S} \Delta x=0
$$

其中$\bar{S}$是控制体积内S的均值，相当于把复杂的$S(x,~T)$简化，便于后续线性化。

‍
