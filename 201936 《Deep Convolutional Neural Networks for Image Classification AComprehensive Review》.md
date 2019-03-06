# 《Deep Convolutional Neural Networks for Image Classification: AComprehensive Review》

# 1.Overview of CNN architecture

CNNs are **feedforward** networks in that information flow takes place in one direction only, from their inputs to their outputs.

![1551858272729](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1551858272729.png)

### 1.1 Convolutional Layers

The convolutional layers serve as feature extractors, and thus they learn the feature representations of their input images.Moreformally, the kth output feature map Yk can be computed as
$$
Yk = f(Wk ∗x)
$$
where the input image is denoted by x; the convolutional filter related to the kth feature map is denoted by Wk; the multiplication sign in this context refers to the 2D convolutional operator, which is used to calculate the inner product of the filter model at each location of the input image; and f(·) represents the nonlinear activation function.

### 1.2 Pooling Layers

The purpose of the pooling layers is to reduce the spatial resolution(空间分辨率) of the feature maps and thus achieve spatial invariance（空间不变性） to input distortions（失真） and translations .

### 1.3 Fully Connected Layers

The fully connected layers that follow these layers interpret these feature representations and perform the function of high-level reasoning.（跟随这些层的完全连接层**解释**这些特征表示并执行**高级推理**的功能）

### 1.4 Training

The most common algorithm used for this purpose is backpropagation.Backpropagation computes the gradient of an objective (also referred to as a cost/loss/ performance) function to determine how to adjust a network’s parameters in order to minimize errors that affect performance. 

### 1.5 需要补充看的书

 (1)Further detailed explanations on the convolution function and its variants and the convolutional and pooling layers.

<<Goodfellow, I., Bengio, Y., & Courville, A. (2016). ***Deep learning***. Cambridge, MA: MIT Press.>>

(2) Detailed explanations on the backpropagtion algorithm and general training protocols for deep neural networks

<LeCun, Y., Bottou, L., Bengio, Y., & Haffner, P. (1998). ***Gradient-based learning applied to document recognition*.** Proceedings of the IEEE, 86(11), 2278–2324.>

