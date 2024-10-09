<h1>1 数值方法A</h1>
<h2>课堂笔记</h2>
<h3>基础</h3>
<p>主要是针对N-S方程求解，有三种方法：有限体积、有限元、有限差分。</p>
<p>微分：</p>
$$\underset{\Delta x \to 0}{lim} \frac{f(x_0+\Delta x)-f(x_0)}{\Delta x}=\frac{dy}{dx}$$
<p>​<img src="assets/360albumviewer_imgproc_1712893765-20240924164238-6pripo5.png" alt="360albumviewer_imgproc_1712893765" /></p>
<p>不同尺度下物质密度：分子尺度$l_m$&lt;&lt;连续体$\eta$&lt;&lt;地理尺度L（教室、地球...）</p>
<p>​<img src="assets/Screenshot_2024-09-24-16-55-30-031_com.jideos.jnotes-20241009204042-p1grqgw.png" alt="Screenshot_2024-09-24-16-55-30-031_com.jideos.jnotes" />​</p>
<p>​本课程研究连续体尺度的问题。</p>
<h3>一维稳态扩散及其求解</h3>
<h4>一维动量守恒</h4>
<p>在高中阶段，我们已经学习了关于动量的两个基本公式：</p>
$$P=mV\\\sum F=\frac{dp}{dt}$$
<p>现在，让我们考虑一个流体微元，其体积为$dV=Adx$（参见下面讲控制体积时的图），质量为$dm=\rho dV$，速度为$u$。</p>
<p>（注意：这里$u=\frac{dx}{dt}$表示一个流体微元的位置x随着时间t的变化率；稳态下，$\frac{\partial u}{\partial t}=0$，即流体微元的运动速度在流场中的分布不随时间变化，但流体微元的位置x仍然会随着时间变化。）</p>
<p>其动量为：</p>
$$dP=dm\cdot u=\rho dV u=\rho uA dx$$
<p>其动量密度（每单位体积动量）为$\rho u$。</p>
<p>对于单位时间内，通过某一截面的动量：（注意$dV=uA$，其中A为截面面积）</p>
$$动量流量=\rho (uA)u=\rho u^2 A$$
<p>若只考虑一维，则可让A=1，动量流量=$\rho u^2$。</p>
<p>那么，对于该微元体积，其动量变化率为：</p>
$$\frac{d(\rho u)}{dt}=\frac{\partial (\rho u)}{\partial t}+\frac{\partial(\rho u^2)}{\partial x}$$
<p>注意Adx不随时间变化，上式表示动量密度随着时间和空间的变化。</p>
<p>假设流动是稳态的（不随时间变化），$\frac{\partial(\rho u)}{\partial t}=0$，则动量变化率可视为：</p>
$$\frac{d(\rho u)}{dt}=u\cdot\frac{\partial(\rho u)}{\partial x}=\rho u\frac{\partial u}{\partial x}$$
<p>根据动量定理，流体中动量的变化率等于外力作用：</p>
$$-\frac{dp}{dx}=\rho u \frac{du}{dx}$$
<p>其中，$-\frac{dp}{dx}$是压力梯度，$\rho u$代表质量流量，$\frac{du}{dx}$表示速度梯度。</p>
<p>令$F(u)=\frac{1}{2} u^2$：</p>
$$\frac{dF(u)}{dx}=\frac{dF}{du}\cdot \frac{du}{dx}=u\frac{du}{dx}$$$$-\frac{dp}{dx}=\rho u \frac{du}{dx}=\rho \frac{d(\frac{u^2}{2})}{dx}$$
<p>这里，$\frac{d(\frac{u^2}{2})}{dx}$表示动能梯度。</p>
<p>所以，<strong>当流体从高压区流向低压区时，压力梯度驱使流体加速，压力变化转化为流体动能，导致速度和动量的变化。</strong></p>
<p>进一步推导：</p>
$$\int_{x_1}^{x_2} -dp=\int_{x_1}^{x_2} \rho d(\frac{1}{2}u^2)$$$$\int_{p_1}^{p_2} -dp=\int_{u_1}^{u_2} \rho d(\frac{1}{2}u^2)$$$$p_1-p_2=\frac{1}{2}\rho (u_2^2-u_1^2)$$
<p>即伯努利方程。</p>
<h4>一维稳态扩散</h4>
<p>扩散通量：根据傅里叶定律，对于某个物理量$\phi$，单位面积上、单位时间内通过的量，与其梯度成正比。</p>
$$J=-\Gamma \frac{d\phi}{dx}$$
<p>‍</p>
<p>其中，$\Gamma$是扩散系数，因为扩散是从高浓度向低浓度，故这里用负号。</p>
<p>对扩散通量公式求导得：</p>
$$\frac{dJ}{dx}=\frac{d}{dx}(-\Gamma \frac{d\phi}{dx})$$
<p>在稳态下，系统内部扩散的增减被源项平衡，即扩散通量变化与源项的和为0.</p>
$$\frac{d}{dx} (\Gamma \frac{d \phi}{dx})+S(x,~\phi)=0$$
<p>扩散：任何物质（粒子、能量、动量...）由高浓度区域向低浓度区域传输，由浓度梯度驱动，无大规模物质对流。</p>
<p>式中：</p>
<ul>
<li>$\phi$表示待求的量（如温度、浓度、电势）；</li>
<li>$\Gamma$表示扩散系数，$\frac{d}{dx} (\Gamma \frac{d \phi}{dx})$是扩散项，表示待求量扩散的速度和系数随着空间x变化，代表能量传递的过程；</li>
<li>S表示源项（生成）或耗散项（消耗），与空间x、变量$\phi$相关，代表驱动能量传递的力量.<br />
在一维经壁热传导中，源项表示单位体积内热源或热汇的强度，如内部热源（材料本身由于其物理性质、化学反应，或内部有电阻，吸热、放热）。<br />
但高温区域、低温区域、墙壁构成的总系统的能量变化为0，系统内部能量守恒。</li>
</ul>
<p>稳态：$\frac{\partial}{\partial t}=0$，时间不再影响$\phi$的变化，扩散过程已经达到平衡。</p>
<p>应用：</p>
<ol>
<li>
<p>剪应力的跨流扩散</p>
$$\frac{d}{dx}(\mu \frac{du}{dx})-\frac{dp}{dy}=0$$
<p>​​</p>
<p>式中：</p>
<ul>
<li>$\mu$是<strong>动态粘度</strong>，描述流体的剪切变形对剪应力的响应，反映了流体的<strong>粘性</strong>，是纯物质属性，单位$N\cdot s/m^2$；</li>
<li>v（这里未出现）是动力粘度，是动态粘度与流体密度的比值，反映了流体在<strong>重力作用下的扩散性</strong>；</li>
<li>$\frac{du}{dx}$表示速度梯度，反映了流体层之间的速度差异，$\frac{d}{dx}(\mu \frac{du}{dx})$代表剪应力的扩散；</li>
<li>$\frac{dp}{dy}$是压力梯度，表示驱动流动的压力差，作为动量的来源。当流动完全发展时，$\frac{dp}{dy}=0$；</li>
</ul>
<p>稳态：速度场和压力场不随时间变化；</p>
<p>描述层流条件下的粘性流体，在粘性影响下，流体的各层相对滑动，产生剪应力。</p>
</li>
</ol>
<h4>一维稳态扩散的应用2：经壁热传导</h4>
<ol>
<li>公式：</li>
</ol>
$$\frac{d}{dx}(\lambda \frac{dT}{dx})+S(x,~T)=0$$
<p>​<img src="assets/Screenshot_2024-09-24-20-36-48-831_com.jideos.jnotes-20240924203830-uyywlaj.png" alt="Screenshot_2024-09-24-20-36-48-831_com.jideos.jnotes" /><br />
式中，$\lambda$为热导率，S代表系统中额外的热源/热汇。</p>
<p>边界条件：若绝热（adiabatic），$\frac{\partial T}{\partial x}=0$。</p>
<ol start="2">
<li>如何求数值解</li>
</ol>
<p>基本思路是离散化，目标是化为如下形式：</p>
$$\left\{\begin{matrix}a_{1,~1}T_1+a_{1,~2}T_2+...+a_{1,~n}T_n
 \\...
 \\a_{n,~1}T_1+a_{n,~2}T_2+...+a_{n,~n}T_n
\end{matrix}\right.\Longrightarrow 
[A][T]=[B]$$
<p>在该矩阵中，$a_{i,~j}$表示描述第i个节点的控制方程中，和第j个节点（如左侧$a_{i,~i-1}$、自身$a_{i,~i}$、右侧$a_{i,~i+1}$）相关的系数；[B]表示所有不与温度相关的常数项。</p>
<p>​<img src="assets/image-20240924205135-bmsqqog.png" alt="image" />​</p>
<p>如图所示，在x=0到x=L的空间内取n个点测温。注意，点1在左边墙上，点n在右边墙上（即边界条件）。</p>
<p>这里有：</p>
$$\Delta x=\frac{L-0}{n-1}$$$$\frac{dT}{dx}\mid_i~\approx \frac{T_{i+1}-T_i}{\Delta x} \approx \frac{T_{i+1}-T_{i-1}}{2\Delta x}$$
<p>离散化的具体实现：使用有限体积法，将整个域离散为n个控制体积（control volume，CV）。</p>
<p>​<img src="assets/image-20241009204123-jdq7352.png" alt="image" />​</p>
<p>原公式如下：</p>
$$\frac{d}{dx}(\lambda \frac{dT}{dx})+S(x,~T)=0$$
<p>根据控制体积，对上式进行积分，则有：</p>
$$\int_v \frac{d}{dx}(\lambda \frac{dT}{dx})dV+\int_v S(x,~T)dV=0$$
<p>​<img src="assets/Screenshot_2024-09-24-22-27-39-350_com.jideos.jnotes-20240924223221-14ja6kl.png" alt="Screenshot_2024-09-24-22-27-39-350_com.jideos.jnotes" />​</p>
<p>​<img src="assets/IMG_20240924_223429-20240924223457-zegtbur.jpg" alt="IMG_20240924_223429" />​</p>
<p>参见上图，有$dV=Adx$，则：</p>
$$\int_w^e \frac{d}{dx}(\lambda \frac{dT}{dx})Adx+\int_w^e S(x,~T)Adx=0$$
<p>这里W意为west，E意为east。</p>
<p>​<img src="assets/Screenshot_2024-09-24-22-37-40-219_com.jideos.jnotes-20241009204144-uhoijr7.png" alt="Screenshot_2024-09-24-22-37-40-219_com.jideos.jnotes" />​</p>
<p>如图，设对阴影部分积分。</p>
$$\int_a^b f(x)dx=f[a+\xi(b-a)]\cdot(b-a)$$
<p>其中$\xi$是0~1之间的任意常数。</p>
<p>又有$\int \frac{df(x)}{dx}dx=f(x)$，则方程可化为：</p>
$$[\lambda\frac{dT}{dx}]_{w}^{e}+\bar{S}[x]_w^e=0$$$$(\lambda \frac{dT}{dx})_e-(\lambda \frac{dT}{dx})_w+\bar{S} \Delta x=0$$
<p>其中$\bar{S}$是控制体积内S的均值，相当于把复杂的$S(x,~T)$简化，便于后续线性化。</p>
<p>下一步是用中心差分法近似$\frac{dT}{dx}$。</p>
<p>首先，对温度函数$T(x)$用泰勒展开，其中由于2阶以上项计算复杂、对结果影响小，故忽略。</p>
<p>假设在节点之间温度线性变化。</p>
$$T(x)=T(x_i)+(x-x_i)\frac{dT}{dx}|_{x_i}+\frac{(x-x_i)^2}2\frac{d^2T}{dT^2}|_{x_i}$$$$T(x_{P})=T(x_{e})-(\delta x)_{e^{-}}\cdot(-\frac{dT}{dx})|_{x_{e}}+\frac{(\delta x)_{e^{-}}^2}{2}\cdot(\frac{d^2T}{dT^2})|_{x_{e}}$$$$T(x_E)=T(x_e)-(\delta x)_{e^+}\cdot (\frac{dT}{dx})|_{x_e}+\frac{(\delta x)_{e^+}^2}2 \cdot(\frac{d^2T}{dT^2})|_{x_e}$$
<p>令e为P、E中点，则有$(\delta x)_{e^-}=(\delta x)_{e^+}=\frac{1}{2} (\delta x)_e$，故：</p>
$$\frac{dT}{dx}|_{x_e}=\frac{T(x_E)-T(x_P)}{(\delta x)_e}$$
<p>回代入公式$(\lambda \frac{dT}{dx})_e-(\lambda \frac{dT}{dx})_w+\bar{S} \Delta x=0$得：</p>
$$(\lambda \frac{dT}{dx})_e=\lambda_e \cdot \frac{T_E-T_P}{(\delta x)_e}$$$$(\lambda \frac{dT}{dx})_w=\lambda_w \cdot \frac{T_P-T_W}{(\delta x)_w}$$
<p>另有：</p>
$$\bar{S}=S_p \cdot T_P+S_c$$
<p>把源项在控制体积内的均值$\bar{S}$线性化，其中$S_P$为线性系数（或斜率），$S_c$为常数项（或截距），二者均应当为常数。</p>
<p>那么，将我们得到的这三个公式组合起来，可以得到最终的线性化方程：</p>
$$a_w T_w +a_p T_p+a_ET_E=b$$
<p>其中，代表三个节点（当前控制节点左边一个、它本身、右边一个）的系数，以及右边一项b，分别是：</p>
$$\quad a_W=-\frac{\lambda_w}{\delta x_w}\quad a_P=\frac{\lambda_w}{\delta x_w}+\frac{\lambda_e}{\delta x_e}-S_P\Delta x\quad a_E=-\frac{\lambda_e}{\delta x_e}\quad b=S_C\Delta x$$
<p>注意，这个式子只能用于内部控制体积，不适用于边界节点。</p>
<p>对于边界条件：</p>
<ul>
<li>
<p>已知温度：（$T(x=0)=T_a\text,~T(x=L)=T_b$）</p>
$$a_PT_P+a_ET_E=b,~a_P=1,~a_E=0,~b=T_a\\a_WT_W+a_PT_P=b,~a_P=1,~a_W=0,~b=T_b$$</li>
<li>
<p>已知温度随空间变化的导数，描述热流边界条件：<br />
​<img src="assets/image-20241009205915-4tnhskk.png" alt="image" />如图，定义热通量$q_B=-\lambda \frac{dT}{dx}$。</p>
$$(\lambda\frac{dT}{dx})_i-\left(\lambda\frac{dT}{dx}\right)_B+\bar{S}\Delta x_B=0$$
<p>这里可以把$-\left(\lambda\frac{dT}{dx}\right)_B$这一项用$q_B$代替，于是可推出最后的线性化方程：</p>
$$a_PT_P+a_ET_E=b,~a_P=\frac{\lambda_e}{\delta x_e}-S_p\Delta x_B,~a_E=-\frac{\lambda_e}{\delta x_e},~\mathrm{b}=S_p\Delta x_B+q_B$$</li>
</ul>
<p>​<img src="assets/image-20241009212205-r1d2ivw.png" alt="image" />​</p>
<p>如图，最后得到了一个三对角矩阵。每个节点只影响其左侧一个和右侧一个节点。</p>
<h4>求解线性方程组</h4>
<h5>判断解的稳定性</h5>
<ul>
<li>
<p>解是否有边界？</p>
</li>
<li>
<p>边界条件是否被遵守？</p>
</li>
<li>
<p>结果如何与理论解或实验数据比较，以验证数值解的正确性？</p>
</li>
<li>
<p>残差误差：</p>
$$R=\frac{|B-A\cdot T|}{|diag(A)\cdot T|}<tol$$
<p>其中，$|B-A\cdot T|$是残差，表示实际计算的结果$A\cdot T$与理论上应当得到的结果B之间的差；<br />
​$diag(A)\cdot T$是矩阵A的对角线部分与T的乘积，用于对残差进行非量纲化，使得残差大小与系统的尺度保持一致。<br />
若R小于某个预设的容差tol，可认为解的精读是能接受的。</p>
</li>
<li>
<p>能量平衡：能量守恒必须在每个控制体中保持。有时源项$\bar{S}=0$，则控制体内的流入和流出热量$q_w - q_e = 0$。</p>
</li>
<li>
<p>网格收敛性：若网格细化，节点间距减半，误差应减少4倍。这种收敛特性在已知精确解时表现最好，通常通过对数-对数图（log-log plot）来评估收敛行为。</p>
</li>
</ul>
<h5>直接求解：高斯消元法</h5>
<p>对如下矩阵：</p>
$$\begin{bmatrix}a_{1,1}&a_{1,2}&a_{1,3}&...&a_{1,n}\\a_{2,1}&a_{2,2}&a_{2,3}&...&a_{2,n}\\\vdots&\vdots&\vdots&\ddots&\vdots\\a_{n,1}&a_{n,2}&a_{n,3}&...&a_{n,n}\end{bmatrix}\times\begin{bmatrix}T_1\\T_2\\\vdots\\T_n\end{bmatrix}=\begin{bmatrix}b_1\\b_2\\\vdots\\b_n\end{bmatrix}$$
<ol>
<li>
<p>前向消元：将第i行减去第1行的某个倍数，使得$a_{i,~1}=0$，这样就能消去除了$a_{1,~1}$以外，矩阵A第1列的所有数；<br />
重复直到矩阵A变成上三角矩阵。<br />
​<img src="https://raw.githubusercontent.com/AnthonyBvvd/AnthonyBvvd.github.io/main/test/image-20241009215952-ahw57yi.png" alt="image" />​</p>
</li>
<li>
<p>回代：从最后一行开始，最后一行相当于解:</p>
$$a_{n,~n}^{(N-1)}\cdot T_n = b_n^{(N-1)}$$
<p>倒数第2行相当于解：</p>
$$a_{n-1,n-1}^{(N-1)}T_{n-1}+a_{n-1,n}^{(N-1)}T_n=b_{n-1}^{(N-1)}$$
<p>最后得到的通项公式为：</p>
$$T_i=\frac{b_i^{(N-1)}-\sum_{k=i+1}^na_{i,k}^{(N-1)}T_k}{a_{i,i}^{(N-1)}}$$</li>
</ol>
<h5>迭代求解：高斯-赛德尔法</h5>
<p>通项公式：</p>
$$T_i^{(m)}=\frac{b_i}{a_{i,i}}-\sum_{j=1}^{i-1}\frac{a_{i,j}}{a_{i,i}}T_j^{(m)}-\sum_{j=i+1}^n\frac{a_{i,j}}{a_{i,i}}T_j^{(m-1)}\\
=\frac{1}{a_{i,~i}}(b_i-\sum_{j=1}^{i-1}a_{i,j}T_j^{(m)}-\sum_{j=i+1}^na_{i,j}T_j^{(m-1)})$$
<p>其中：</p>
<ul>
<li>
<p>$T_i^{(m)}$表示第m次迭代中，第i个未知数的近似值；</p>
</li>
<li>
<p>$T_j^{(m)}$表示第m次迭代中，第j个未知数近似值，j&lt;i时，这些值在本次迭代中已更新；</p>
</li>
<li>
<p>$T_j^{(m-1)}$表示第m次迭代中，第j个未知数近似值，j&gt;i时，这些值在本次迭代中未更新；</p>
</li>
<li>
<p>$a_{i,~i}$：矩阵A第i行i列元素；</p>
</li>
<li>
<p>$b_i$：矩阵b第i行元素；</p>
</li>
<li>$$\sum_{j=1}^{i-1}a_{i,j}T_j^{(m)}$$
<p>这一项对在第i行中，i之前的未知数项求和（已迭代）</p>
</li>
<li>$$\sum_{j=i+1}^na_{i,j}T_j^{(m-1)}$$
<p>这一项对在第i行中，i之后的未知数项求和（未迭代）。</p>
</li>
</ul>
<p>该法的物理意义为：通过$b_i$减掉加权求和，意为扣除已知部分，剩余未知数项的影响；除以$a_{i,~i}$则解出未知数。</p>
<p>‍</p>
