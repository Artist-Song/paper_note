# SOFTMAX

softmax又称归一化指数函数，它是二分类函数sigmoid在多分类上的推广，目的是将多分类的结果以概率的形式展现出来。下图展示了softmax的计算方法：

![image-20220527095428673](C:\Users\76705\AppData\Roaming\Typora\typora-user-images\image-20220527095428673.png)

概率的性质：预测为非负数，各预测概率和为1.

所以softmax把在正无穷和负无穷的数值映射到概率。

**1）将预测结果转化为非负数**

下图为y=exp(x）的图像，我们可以知道**指数函数**的值域取值范围是零到正无穷。**softmax第一步就是将模型的预测结果转化到指数函数上，这样保证了概率的非负性。**

![img](https://img-blog.csdnimg.cn/2019111910482712.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2x6X3BldGVy,size_16,color_FFFFFF,t_70)

**2）各种预测结果概率之和等于1**

为了确保各个预测结果的概率之和等于1。我们只需要将转换后的结果进行归一化处理。方法就是**将转化后的结果除以所有转化后结果之和，可以理解为转化后结果占总数的百分比**。这样就得到近似的概率。





例子：

假如模型对一个三分类问题的预测结果为-3、1.5、2.7。我们要用softmax将模型结果转为概率。步骤如下：

1）**将预测结果转化为非负数**

y1 = exp(x1) = exp(-3) = 0.05

y2 = exp(x2) = exp(1.5) = 4.48

y3 = exp(x3) = exp(2.7) = 14.88

2）各种预测结果概率之和等于1

z1 = y1/(y1+y2+y3) = 0.05/(0.05+4.48+14.88) = 0.0026

z2 = y2/(y1+y2+y3) = 4.48/(0.05+4.48+14.88) = 0.2308

z3 = y3/(y1+y2+y3) = 14.88/(0.05+4.48+14.88) = 0.7666


总结一下softmax如何将多分类输出转换为概率，可以分为两步：

**1）分子：通过指数函数，将实数输出映射到零到正无穷。**

**2）分母：将所有结果相加，进行归一化**

![img](https://img-blog.csdnimg.cn/20181212223827495.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2x6X3BldGVy,size_16,color_FFFFFF,t_70)