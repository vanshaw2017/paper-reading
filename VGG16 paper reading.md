## VGG16 paper reading

**<<Very Deep Convolutional Networks for Large-Scale Image Recognition.>>**

- pdf:<https://arxiv.org/abs/1409.1556>

## 1.Abstract

 **Our main contribution** is a thorough evaluation of networks of **increasing depth** using an architecture with very small (**3×3**) convolution ﬁlters, which shows that a signiﬁcant improvement on the prior-art

## 2.Related work

Convolutional networks (ConvNets) have recently enjoyed a great success in large-scale image and video recognition due to **large dataset**， high-performance **computing systems**（GPU）.In particular,deep visual recognition architectures has been played  an important role.In this paper, we address another important aspect of ConvNet architecture design – **its depth**.T o this end, we ﬁx other parameters of the architecture, and steadily **increase the depth of the network by adding more convolutional layers**, which is feasible due to the **use of very small (3 × 3) convolution ﬁlters** in all layers.

##  3.CONVNET CONFIGURATIONS

### 3.1 convNet configurations

![1552381113861](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1552381113861.png)

### 3.2 dicussion

- why 3*3 filtters stacks, instead of a single7X7 and 1X1?

   **First, we incorporate three non-linear rectiﬁcation layers instead of a single one, which makes the decision function more discriminative. Second, we decrease the number of parameters:** assuming that both the input and the output of a three-layer 3 × 3 convolution stack has C channels, the stack is parametrised by 
  $$
  3(3^2 C^2)=27C^2
  $$
  weights; at the same time, a single 7 × 7 conv. layer would require
  $$
  (7^2 C^2)=49C^2
  $$
    parameters, i.e. **81% more.** This can be seen as imposing a regularisation on the 7 × 7 conv. ﬁlters, forcing them to have a decomposition through the 3 × 3 ﬁlters (with non-linearity injected in between). 

  The incorporation of 1 × 1 conv. layers (conﬁguration C, Table 1) is a way to increase the **nonlinearity of the decision function without affecting the receptive ﬁelds of the conv.** layers. Even though in our case the 1×1 convolution is essentially a linear projection onto the space of the same dimensionality (the number of input and output channels is the same), a**n additional non-linearity is introduced by the rectiﬁcation function.** It should be noted that 1×1 conv. layers have recently been utilised in the “Network in Network” architecture of Lin et al. (2014).

## 4.CLASSIFICATION FRAMEWORK

### 4.1 Trainning 

 Namely, the training is carried out by optimising the multinomial logistic regression objective **using mini-batch gradient descent** (based on back-propagation (LeCun et al., 1989)) **with momentum**. The batch size was set to 256, momentum to 0.9. **The training was regularised by weight decay** (the L2 penalty multiplier set to 5·10−4) and **dropout regularisation for the ﬁrst two fully-connected layers (dropout ratio set to 0.5).** The learning rate was initially set to 10−2, and then decreased by a factor of 10 when the validation set accuracy stopped improving. In total, the learning rate was decreased 3 times, and the learning was stopped after 370K iterations (74 epochs). We conjecture that in spite of the larger number of parameters and the greater depth of our nets compared to (Krizhevsky et al., 2012), **the nets required less epochs to converge due to**  (a) **implicit regularisation imposed by greater depth and smaller conv. ﬁlter sizes; (b) pre-initialisation of certain layers.**

**The initialisation of the network weights is important**, since bad initialisation can stall learning due to the instability of gradient in deep nets. To circumvent this problem, we began with training the conﬁguration A (Table 1), shallow enough to be trained with random initialisation. Then, when training deeper architectures, we initialised the ﬁrst four convolutionallayers and the last three fullyconnected layers with the layers of net A (the intermediate layers were initialised randomly). We did not decrease the learning rate for the pre-initialised layers, allowing them to change during learning. For random initialisation (where applicable), we sampled the weights from a normal distribution with the zero mean and 10−2 variance. The biases were initialised with zero. It is worth noting that after the paper submission we found that it is possible to initialise the weights without pre-training by using the random initialisation procedure of Glorot & Bengio (2010).

## 5.CLASSIFICATION EXPERIMENTS

- First, we note that **using local response normalisation (A-LRN network) does not improve on the model** A without any **normalisation layers.**

- （3x3 better than 1x1）This indicates that while the **additional non-linearity does help** (C is better than B), it is also important to capture spatial context by u**sing conv. ﬁlters with non-trivial receptive** ﬁelds (D is better than C).
- The error rate of our architecture saturates when the depth reaches 19 layers, but even deeper models might be beneﬁcial for **larger datasets.**
- The top-1 error of the shallow net (changing **each pair of 3x3 to 5x5**,which has the same receptive ﬁelds)was measured to be 7% higher than that of B (on a center crop), **which conﬁrms that a deep net with small ﬁlters outperforms a shallow net with larger ﬁlters.**
- This conﬁrms that training set augmentation by **scale jittering** is indeed helpful for capturing multi-scale image statistics.

## 6.Conclusion

In this work we evaluated very deep convolutional networks (up to 19 weight layers) for largescale image classiﬁcation. It was demonstrated that the **representation depth is beneﬁcial for the classiﬁcation accuracy,** and that state-of-the-art performance on the ImageNet challenge dataset can be achieved using a conventionalConvNet architecture (LeCun et al., 1989; Krizhevsky et al., 2012) with substantially increased depth. In the appendix, we also show that our models generalise well to a wide range of tasks and datasets, matching or outperforming more complex recognition pipelines built around less deep image representations. Our results yet again conﬁrm the importance of depth in visual representations.