# Unsupervised Anomaly Detection in Multivariate Time Series through Transformer-based Variational Autoencoder



## 亮点

**提出了新的异常检测算法TransAnomaly，这个算法结合了VAE和transformer，既可以考虑future dependency，也提高了并行能力**

****

**引入了GTF（TODO:干嘛用的？）**

****





## 预备工作

### 问题定义

![image-20220526205225736](C:\Users\76705\AppData\Roaming\Typora\typora-user-images\image-20220526205225736.png)

### 变分自编码器，VAE（Variational AutoEncoder）是什么？

#### 相关背景

##### 生成模型（Generative model）

	生成模型是指能够随机生成观测数据的模型，尤其是在给定某些隐含参数的条件下。它给观测值和标注数据序列指定一个联合概率分布。换句话说，生成模型首先研究的是特征 X  与标签 y  之间的联合分布，然后再求条件概率 P ( y ∣ X ) P(y|X)P(y∣X) ，预测时应用最大后验概率法得到预测结果。
##### 隐变量模型（Latent Variable Models）

- **隐变量：** 不可直接观测的综合性变量。
- **隐变量模型：** 隐变量模型是一种概率模型，其中某些变量是不可观测的。（即包隐变量的概率模型）A latent variable model is a probability model for which certain variables are never observed.

##### 自编码器（AutoEncoder）

自编码器是一类在半监督学习和非监督学习中使用的人工神经网络，其功能是通过将输入信息作为学习目标，对输入信息进行表征学习。

AutoEncoder 包括 编码器(Encoder) 和 解码器(Decoder) 两部分。Encoder 过程是将原先的数据（常用于图像方向）压缩为低维向量；Decoder 则是把低维向量还原为原来数据。

因为自编码常用于图像方向，因为一张图每一个像素点都被看作是一个特征，所以随便一张现实中的图都属于高维向量。所以很多教程直接把这里提到的数据用 图片 来代替，Decoder 的过程也就是转换为原来的图像。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200920141932355.png#pic_center)

##### 自编码器的特点

- 非监督学习 (Unsupervised Learning)
- 是一种前馈神经网络，没有任何反馈
- 是一种生成模型
- 具有较好的特征提取能力
- 它的降维可以是非线性的，而 PCA 是线性的
- 常用于 特征提取、文档检索、分类和异常检测





#### 继续说VAE([李宏毅2020机器学习深度学习(完整版)国语_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1JE411g7XF?p=61))

VAE 模型是一种包含隐变量的生成模型，它利用神经网络训练得到两个函数（也称为推断网络和生成网络），进而生成输入数据中不包含的数据



VAE 模型在生成多种复杂数据方面已经显示出了巨大的潜力，包括手写数字图像、人脸图像、门牌号图像、CIFAR 图像、场景物理模型、分割图像以及从静态图像进行预测等。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200922150939717.png?#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200923095127685.png?#pic_center)

图片左边部分是 AutoEncoder 的简单例子：我们把一张满月的图片 Encoder 后得到 code，这个code被decoder 后又转换为满月图，弦月图也是如此。注意它们直接的一对一关系。

图片右边部分是 VAE 的简单例子，在 code 中添加一些 noise，这样可以让在满月对应 noise 范围内的code 都可以转换为满月，弦月对应的noise 范围内的code也能转换成弦月。
但当我们在code中进行采样时，在不是满月和弦月对应的noise的code中采样时，decoder出来的图片可能是介于满月和弦月之间的图。

也就是说，VAE 产生了输入数据中不包含的数据，（可以认为产生了含有某种特定信息的新的数据），而 AE 只能产生尽可能接近或者就是以前的数据（当数据简单时，编码解码损耗少时）。

图片左边那个问号的意思是当对 AE 中的code进行随机采样时，它介于满月与弦月之间的数据，decoder后可能会输出什么？
可能会输出满月，可能会输出弦月，但是最有可能输出的是奇奇怪怪的图片。

##### 隐变量(Latent Variable)

上面已经讲过隐变量的基本概念，这里介绍隐变量在 VAE模型中的作用及特点。

隐变量 z zz 是可以认为是隐藏层数据，它是不限定数目的符合 高斯分布 特征的数据。（根据实际情况确定数目）
z zz 由输入数据 X XX 的采样以及参数生成，它既包含 X XX 的信息（这个于 AutoEncoder 的隐藏层类似），同时也满足 高斯分布，方便接下来进行梯度下降或者其他优化技术（By having a Gaussian distribution, we can use gradient descent (or any other optimization technique) to increase P ( X ) P(X)P(X) by making f ( z ; θ ) f(z; \theta)f(z;θ) approach X XX for some z zz ,i.e., gradually making the training data more likely under the generative model.）。
隐变量的作用除了让生成网络尽可能还原原来的数据 X XX，同时也能生成原来数据中不存在的数据





之后的VAE内容不做过多介绍，可以参阅博客：

[(46条消息) VAE 模型基本原理简单介绍_smile-yan的博客-CSDN博客_vae模型](https://blog.csdn.net/smileyan9/article/details/107362252?ops_request_misc=%7B%22request%5Fid%22%3A%22165356965216782390553530%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=165356965216782390553530&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-107362252-null-null.142^v10^pc_search_result_control_group,157^v12^control&utm_term=VAE&spm=1018.2226.3001.4187)



### transformer

transformer是一个完全基于自注意力机制的一个模型，这里就不展开叙述了。这篇文章中也借鉴了transformer的思想。



### POT（Peaks-Over-Threshold）

总的来说这个就是个检测异常的阈值。



## ANOMALY DETECTION FRAMEWORK（检测框架）

首先说明为啥加了所谓了future dependency之后效果会变好。

受Transformer的启发，作者在VAE模型中embed了TransformerBlock（啥东西？），后文提到，这个东西可以捕获每对儿vector在不同location上的关系。所以输出有所有输入的信息。下面解释根据概率为啥这个东西能起作用。

![image-20220526211857894](C:\Users\76705\AppData\Roaming\Typora\typora-user-images\image-20220526211857894.png)

作者计算了关于时间的后验分布，

![image-20220526211931089](C:\Users\76705\AppData\Roaming\Typora\typora-user-images\image-20220526211931089.png)

这句话没看懂。

这个公式提示说，The dependency of zt on future input xt+1:T使得后验推论难以得到解决，所以就把xt:T改成et，这个et有以前，现在和未来的信息，而不是直接用后验概率分布xt+1:T.

![image-20220526212304703](C:\Users\76705\AppData\Roaming\Typora\typora-user-images\image-20220526212304703.png)



上面的证明主要是证明transformer的可行性，具体细节可以自行把握，本文不做过多叙述了。



最主要的是网络结构，对于transAnomaly来说，变分网络结构是这样子的：

![image-20220526212459213](C:\Users\76705\AppData\Roaming\Typora\typora-user-images\image-20220526212459213.png)

可以看到和transformer差不多，但是也有一定的变化。



### 生成网络（Generative Network）

