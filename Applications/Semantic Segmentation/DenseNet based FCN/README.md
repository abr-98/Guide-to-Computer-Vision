### FC Dense-Nets

The Montreal Institute for Learning Algorithms, Ecole Polytechnique de Montreal, Imagia Inc., and Computer Vision Center persued another modification to the U-net architecture and proposed DenseNets to replace the basic convolutional blocks of the Unet.

The authors focused on the facts that the DenseNets have skip connections, which will help the model to learn better features and also the model works on a multi-scale space, i.e, it learns from multiple scaled images at the same time, which helps it to extract richer feature.

![Densenet](https://miro.medium.com/max/770/1*rmHdoPjGUjRek6ozH7altw.png)

The dense blocks are useful as they carry low level features from previous layers directly alongside higher level features from more recent layers, allowing for highly efficient feature reuse.

![Arch](https://miro.medium.com/max/716/1*5Bqcgzl6JDXrScL1RXd6Ag.png)

The above shows the Architecture of the proposed densenet based Unet architecture.

![Layers](https://miro.medium.com/max/1970/1*1Pj56mTHPNha8Pg58fWJEQ.png)

The above give the details of the layers used in the architecture. 

The model architecture uses a skip connection over the DenseNet modules in the encoder limb, to have better gradient flow, but it is not present in the decoder limb, as it becomes "Memory Demanding". The concatenation of feature maps between the encoder and the decoder limb remains as it was in the original Unet architecture, for the model to learn the local information better.

References:

1. https://arxiv.org/pdf/1611.09326.pdf
2. https://arxiv.org/pdf/1608.06993.pdf
3. https://towardsdatascience.com/review-fc-densenet-one-hundred-layer-tiramisu-semantic-segmentation-22ee3be434d5
4. https://towardsdatascience.com/review-densenet-image-classification-b6631a8ef803




