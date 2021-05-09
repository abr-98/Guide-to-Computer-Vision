### VGG Network

VGG16 is a convolutional neural network model proposed by K. Simonyan and A. Zisserman from the University of Oxford. It was one of the famous model submitted to ILSVRC-2014. The architecture was put forward in a paper titled "Very Deep Convolutional Networks for Large-Scale Image Recognition”. The model is trained on the Imagenet dataset. 

The paper proposes, several variants of the main stem architecture, namely, VGG-11, VGG-16, VGG-19, and compares thier relative performances. The VGG architecture modified the architecture by replacing large-sized kernel in AlexNet, with multiple 3x3 sized kernels in a repetative manner creating blocks, everytime increasing the number of filters. 

#### Architecture

![VGG16](https://cdn.analyticsvidhya.com/wp-content/uploads/2020/04/VGG-2-850x208.png)

The above image describes the architecture of the VGG16 network. It consista of total 13 convolutional layers, divided into 5 blocks, first having 2 convolution layers and the rest 3 each. Maxpooling layer has been attached to the last convolution layer of each block. There are 64 filters for each convolutional layer in the first block, 128 filters for the 2nd block, 256 filters for each layer in the 3rd block, and 512 filters for each layer for both the 4th and 5th block of the architecture. Maxpooling is used to reduce the dimension, of the image. We start with a image of dimension (224,224,3), which is reduced to (7x7) after the 5the convolutional block. 

The 7x7 feature map is then flattened to obtain a vector which is passed through 3 fully connected layers. The last output layer has 1000 nodes, for the 1000 class classification.

The other variants proposed are obtained by altering the network slightly.

![Variants](https://neurohive.io/wp-content/uploads/2018/11/Capture-564x570.jpg)

In the above comparisons, A is VGG 11, B is VGG 13, D is VGG-16 and E is VGG-19. VGG-19 is seen to have a slightly better performance than the state of the art VGG-16 model.

References:
1. https://arxiv.org/pdf/1409.1556.pdf
2. https://neurohive.io/en/popular-networks/vgg16/
3. geeksforgeeks.org/vgg-16-cnn-model/

