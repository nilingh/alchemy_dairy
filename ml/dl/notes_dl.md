# Basics of Deep Learning

Readings:

[神经网络（容易被忽视的基础知识）](https://zhuanlan.zhihu.com/p/29633019)

[神经网络浅讲：从神经元到深度学习](https://www.cnblogs.com/subconscious/p/5058741.html)

[Deep Learning 神经网络基础](https://www.cnblogs.com/maybe2030/p/5597716.html)

---



![image-20200521143059325](https://i.loli.net/2020/06/04/xdn2TKfF1IPHV6s.png)

[ML landscape](http://vas3k.com) : Neural Nets & Deep Learning are sub-branches of ML.



### Simple perceptron

* Limitation: Decision boundary is linear
* Cannot solve non linear separable problems

#### Perceptron

* $\Sigma(Inputs * Weights)$
* Activation Function $g(\Sigma(Inputs * Weights))$ 
* Output is $\hat{y}$

![image-20200521145235394](https://i.loli.net/2020/06/04/ZYL8EjDowbyUf7C.png)

##### Neuro

* Neuro is a generalization of the idea of the perceptron.
* (A Neuro has **two parts**: 1. $\Sigma(wx+b)$ 2. $f(a)$) 一个神经元可以看成**包含两个部分**，一个是对输入的加权求和加上偏置，一个是激活函数对求和后的激活或者抑制。

#### Common Activation Funcitions

* Linear activation function $\hat{y}=w_0+X^TW$ (multiple linear)

* **may generate Non-Linearity** (for picking up complex pattern)

![image-20200521145522284](https://i.loli.net/2020/06/04/oMDJZCiztKaFHuR.png)

#### Sigmoid

* Binary classification
* Linear boundry

![image-20200521150631092](https://i.loli.net/2020/06/04/FXAmsaTErVJ69dx.png)

![image-20200521151244043](https://i.loli.net/2020/06/04/JYFbhM7A8sz6xj1.png)



#### Softmax

* Multiple outputs $[p_1, p_2, ..., p_n]$ for multi-class classification
* Still linear boundary without hidden layers

![image-20200521182526691](https://i.loli.net/2020/06/04/3F1sfPrmld6BcoT.png)

### Multi-Layer Perceptron (MLP)

* Solve Non-linearity problems
* Avoiding feature engineering by adding more layers to solve non-linearity problems
* Advantage over Simple Perceptron
* Typical ReLu in hidden layers and Sigmoid in the last layer

![image-20200521151824300](https://i.loli.net/2020/06/04/nKHvOkfxIX5zwZY.png)

Source [vas3k.com](http://vas3k.com)



##### Hidden layers

**2 activation function in One hidder layer NN**

* g1 for the hidden layer
  * input: W * X + B = A
  * output: H = g1(A)
* g2 in f(x)
  * input: H
  * output: g2(H)

1. Two inputs

![image-20200521170632032](https://i.loli.net/2020/06/04/fKlERv1S5nJL26A.png)

2. Calculated in three "neurons" with inputs, weights and biases

$h_1=g(W_{1,1}*x_1+W_{1,2}*x_2+b_1)$

$h_2=g(W_{2,1}*x_1+W_{2,2}*x_2+b_2)$

$h_3=g(W_{3,1}*x_1+W_{3,2}*x_2+b_3)$

, which is calculated in matrix form **$[H]=g_1[A]$** is the results of hidden layer.

![image-20200521172026601](https://i.loli.net/2020/06/04/lg8Zxyknjv9c643.png)

3. Second groups of three weights $W_i^2$ * the results of hidden layer $h_{i}$ + second bias $b^2$ was the **Input** of last "neuron"

4. The final result calculated by the **last Activation Function** $g_2$ and resutl of linear combination of $W$ and $H$



##### The dimension of inputs and outputs

Weight[ number of Inputs, number of Outpus]

![image-20200523105921973](/Users/neil/Library/Application Support/typora-user-images/image-20200523105921973.png)



