# 极大似然估计MLE

了解极大似然估计之前，我们需要了解条件概率，即$P(x|\theta)$ 代表着什么？

对于上述函数： 输入有两个：$x$表示某一个具体的数据，$\theta$表示模型的参数：

如果$\theta$是已知确定的， $x$是变量，这个函数叫做**概率函数**(probability function)，它描述对于不同的样本点$x$出现概率是多少。

如果$x$是已知确定的，$\theta$ 是变量，这个函数叫做**似然函数**(likelihood function), 它描述对于不同的模型参数，出现$\theta$这个样本点的概率是多少。

实际应用如何呢？我们举一个例子

## 抓球

当我们面前有一个箱子，箱子里放了非常多的黑白球，这些黑白球的组成比例我们并不知道，我们现在想要估计这个比例，即求出上述说的这个$\theta$，我们会怎么做呢？

第一种方案是把所有的黑白球都抓出来，我们自然就知道了黑白球的比例，但是这样并不现实，成本也很高，于是我们选择第二种方案。

第二种方案的话，我们把黑白球充分混合后，抓100个球出来，根据这100个球的颜色比例来估计黑白球的比例，而且我们的估计不能乱估计，我们需要找到一种最有可能的估计，使得我们抓出来的100球的颜色比例出现概率是最为可能的。

这时候我们会发现，我们其实是根据结果反推过程，也可以说是根据小样本的结果来估计和推测大样本的构成。

现在我们抓出来了70个白球，30个黑球，我们的直觉会让我们感觉到箱子内黑白球的比例是7：3，我们通过极大似然估计的角度重新看待这个问题。

我们考虑这100次情况同时发生的概率，如下：

$$
\begin{align}P(样本结果|\theta)&=P(x_1,x_2,...,x_{100}|\theta) \\ &=P(x_1|\theta)P(x_2|\theta)...P(x_{100}|\theta)\end{align}
$$

从公式（1）到（2）的关键在于我们认为，每一次的取球之间是独立同分布的，这一假设非常重要，这一假设是极大似然估计的根基。

有人要问了那$P(x_i|\theta)$如何解呢？事实上，我们做了100次实验，假设我们每一次拿出球的概率如下：

|                  | 白球  | 黑球    |
| ---------------- | --- | ----- |
| $P(x_i\|\theta)$ | $p$ | 1-$p$ |

那么实际上，我们的（2）式能写成如下形式：

$$
\begin{align}P(样本结果|\theta)=p^{70}(1-p)^{30}\end{align}
$$

我们会发现该式变成了一个参数为$p$的函数，当$p$为不同值的时候，该函数的值也不同，我们的目的在于求解使得该函数为最大值时的$\theta$值，我们可以通过求导求解：

求导如下，可以解得$p=0.7$，确实和我们直觉是一样的。

$$
\begin{align}P'(\theta)&=70p^{69}(1-p)^{30}-30p^{70}(1-p)^{29}=0 \\ 70(1-p)&=30p \\ p&=0.7\end{align}
$$

## 求解

好了，上面那个例子已经让我们对极大似然估计入了门了，我们现在做进一步的求解，大家从上一个例子中可以看出，由于$p$非常小，其实本质上$P(\theta)$的值也会非常的小，在样本较多的情况下不利于我们的求解，所以一般我们会采用取对数的方式将乘积变成加的形式求解，如下所示：

我们首先把似然函数的表达式写成一般化的形式：

$$
\begin{align}L(p)&=L(p|x_1,...,x_n)\\&=P(X_1=x_1|p)\cdot ... \cdot P(X_n=x_n|p)\\&=\prod_{i=1}^nP(X_i=x_i|p)\end{align}
$$

我们想让$L(p)$取到最大，则就是让下式成立：

$$
\begin{align}\mathop{\arg\max}\limits_{p}L(p)=\mathop{\arg\max}\limits_{p}\prod_{i=1}^nP(X_i=x_i|p)\end{align}
$$

由于对数函数为单调递增函数，我们对（10）式右边取对数不会影响$p$的大小，故：

$$
\begin{align}\mathop{\arg\max}\limits_{p}L(p)=\mathop{\arg\max}\limits_{p}\sum_{i=1}^n\ln(P(X_i=x_i|p))\end{align}
$$

对于只有一个参数值$p$的情况，我们有：

$$
\begin{align}\frac{\partial\ln L(p)}{\partial p}=0\end{align}
$$

### 多参数情况

我们会发现式（12）只有一个参数，但是并不是分布都只有一个参数，比如正态分布就有两个参数$\sigma^2$和$\mu$，这时候我们怎么求解呢？这时候我们的$\theta$本身将代表为一个参数集合，即：

$$
\begin{align}\theta=[\theta_1,\theta_2]^T=[\mu,\sigma^2]^T\end{align}
$$

极大似然函数如下：

$$
\begin{align}L(\theta)&=\prod_{i=1}^n\frac{1}{\sqrt{2\pi}\sigma}\cdot e^{-\frac{(x_i-\mu)^2}{2\sigma^2}}\\&=(\frac{1}{\sqrt{2\pi}\sigma})^n\cdot e^{-\prod_{i=1}^n\frac{(x_i-\mu)^2}{2\sigma^2}}\end{align}
$$

对其取对数后，有如下分解：

$$
\begin{align}\ln L(\theta)&=-\frac{n}{2}\cdot\ln(2\pi\sigma^2)-\sum_{i=1}^{n}\frac{(x_i-\mu)^2}{2\sigma^2}\end{align}
$$

我们令$\mu=\theta_1$，$\sigma^2=\theta_2$，我们需要对（16）式求偏导，即分别对$\theta$中的所有参数求导，并求解参数方程，求导后如下所示：

$$
\begin{align}\begin{cases} 
\frac{\partial\ln L(\theta)}{\partial \theta_1} = \frac{1}{\theta_2}(\ln2\pi+\ln\theta_2)\sum_{i=1}^{n}(x_i-\theta_1)=0\\
\frac{\partial\ln L(\theta)}{\partial \theta_2} = -\frac{n}{2\theta_2}+\frac{1}{2\theta_2^2}\sum_{i=1}^{n}(x_i-\theta_1)^2=0 
\end{cases}\end{align}
$$
