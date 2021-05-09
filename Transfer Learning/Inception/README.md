### Inception Network

Inception Network was put forward by Google on the ImageNet Visual Recognition Challenge (in 2014). It was first introduced in the paper "Going deeper with convolutions. 

Inception network was seen to perform better than most other networks on the benchmark dataset. Apart from the network, Inception networks in its different versions, put forward several concepts like, the Inception module, the use of 1x1 convolutions for dimensionality reduction and the factorized convolutions.

The basic driving idea behind the basic inception module is, different sized kernels provide different features from the same image data. For instance, a 3x3 convolution provides a feature map different from a 5x5 convolution. If we stack up these different kernels, it will create a deep network, but there is a chance of loss of information and a vanishing gradient problem. So, the authors decided to create a wider network instead of a deep network, so that the units of different convolutional layers will work parallely on the same data, and all the obtained results will be stacked up and concatenated. So, several feature maps highlighting different features are present in the final stack.

![Naive](https://miro.medium.com/max/770/1*DKjGRDd_lJeUfVlY50ojOA.png)

The above image shows the naive inception model, but it causes a problem, a dimension explosion problem. As we can see a number of convolution layers a present here, with kernel dimension upto 5x5. This results in a huge number parameters and a huge time complexity. The problem was solved by using by adopting a dimensionality reduction strategy using 1x1 convlutions.

![Mod](https://miro.medium.com/max/770/1*U_McJnp7Fnif-lw9iIC5Bw.png)

#### Inception V1

![v1](https://miro.medium.com/max/770/1*uW81y16b-ptBDV8SIT1beQ.png)

The above image represents the version 1 of the inception networks. It used 9 inception modules, having 22 layers of convolutions. One of the most important challenge faced by inception v1 was the vanishing gradient problem because of the depth of the network. So, two **auxillary classifiers** were added to the network (shown in box), which injected new gradient and didn't let it vanish.

#### Inception V2

Inception V2 uncovered that a combination of two 3x3 covolutional layers instead of a single 5x5 convolutional improves the speed and performance of the network. Using 5x5 kernels was found to be 2.78 times expensive. It put forward the idea of **factorization** of the convolutional layers. So, it factorized 5x5 kernel into 2 3x3 network. It was also observed that if we factorize nxn kernel into assymetric kernel filters like 1xn and nx1, the arrangement provides an improvement in the performance as well as the operations become cheaper. In v2, the inception module is modified as:

![v2](https://miro.medium.com/max/633/1*DVXTxBwe_KUvpEs3ZXXFbg.png)

#### Inception V3

Inception V3 brought some changes as compared to inception v2 as it introducedm RMSProp Optimizer, a 7x7 convolution in a factorized manner and batch normalization.

There has been other models like inception v4 and Inception-Resnet which are currently being used as State-of-Art architecture.

References:
1.https://arxiv.org/pdf/1409.4842.pdf

3.https://arxiv.org/pdf/1512.00567v3.pdf

5.https://arxiv.org/pdf/1602.07261.pdf

7.https://www.geeksforgeeks.org/ml-inception-network-v1/
8.https://www.geeksforgeeks.org/inception-v2-and-v3-inception-network-versions/
9.https://medium.com/analytics-vidhya/inception-network-and-its-derivatives-e31b14388bf9
10.https://towardsdatascience.com/a-simple-guide-to-the-versions-of-the-inception-network-7fc52b863202



