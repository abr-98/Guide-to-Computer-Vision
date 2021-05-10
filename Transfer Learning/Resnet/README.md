### Resnet

Resnet or the Residual Neural Networks was first proposed by Microsoft Research in year 2015 Imagenet competition. The paper titled "Deep Residual Learning for Image Recognition" put the idea forward. The driving concept of the Resnet is the introduction of "skip connections". 

Imagenet competitions have shown the increasingly deep neural network architecture can be used to boost network performance. But it was also seen that often deep layered networks, perform worse than shallow networks, this is because deep networks face the problems of "vanishing" and "exploding" gradients. As the gradients are muliplied a number of times, and as the differentiation of error is a very small number, it almost vanishes as we go deeper in the network, and the layers deeper fail to learn, as there is no significant update of the weight. 

To solve the problem, the authors introduced skip connection modules called residual module.

![res_module](https://media.geeksforgeeks.org/wp-content/uploads/20200424011510/Residual-Block.PNG)

The above image shows the perfect representation of the Resnet Module. The skip connections are designed to skip a few convolutional filters and directly add the gradient to the output. The idea as shown by the paper is instead of layers learn the underlying mapping, we allow network fit the residual mapping. So, instead of say H(x), initial mapping, let the network fit, F(x):= H(x)–x which gives H(x):= F(x) + x.

Now, we just add the gradient of the previous layers to the output of the next layers. This prevents the gradient from fading. The skip connections provide a free way for the gradient to move forward.

#### Architecture: Resnet V1

![Arch](https://miro.medium.com/max/3112/1*yy6Bbnp38MhcfDQbzOGf4A.png)

The above image shows the architecture for a proposed Resnet-34 network, having 34 convolutional layers. We also found that the similar one with 50 layers Resnet-50 V1 provides better performance.

#### Resnet-V2

Resnet-V2 brought a minor modification to the architecture of the Resnet-v1 module, which brought a mejor increase in the performance of the model. initially Resnet-v1 was a post-activation module, that is the ReLU and batch normlization was done in the main stem so, it effected the skip connections. Contemprary reseaech showed, that more clear the skip connections, better is the performance. So, the Resnet-V2 used a Pre-activation approach instead of the post-activation, using the Relu and the Batch normaliation as a part of the skip connection.

![V2](https://miro.medium.com/max/770/1*M5NIelQC33eN6KjwZRccoQ.png)

References:

1. https://arxiv.org/pdf/1512.03385.pdf
2. https://arxiv.org/pdf/1603.05027.pdf
3. https://towardsdatascience.com/an-overview-of-resnet-and-its-variants-5281e2f56035
4. https://towardsdatascience.com/resnet-with-identity-mapping-over-1000-layers-reached-image-classification-bb50a42af03e#:~:text=Using%20pre%2Dactivation%20unit%20can,deeper%20from%20110%20to%201001.&text=Pre%2Dactivation%20unit%20is%20on,but%20with%20lower%20test%20error.




