### U-Net

The idea of U-Net was developed from the idea of Fully Connected Network's skip connection. The idea was mainly to make the upsampling limb stronger. The authors proposed a symmetric model structure.

![Unt_arch](https://www.jeremyjordan.me/content/images/2018/05/Screen-Shot-2018-05-20-at-1.46.43-PM.png)

The above image shows the proposed architecture. There exists two symmetric limbs in these archiecture. The encoder limb or the contracting path extracts the finer features and captures important global information, while the expanding path or the decoder limb upsamples the the feature map and enables precize localizations. 

The encoder limb consists of blocks of 2 3x3 convolutions followed by a maxpool layer. THere are 4 such blocks. The decoder limb consists of blocks of 2 3x3 convolutions and a up-convolution to upsample the feature map on 2x scale. There are 4 such blocks. Just before passing the feature maps upsampled from the last layer of the decoder limb through the convolutional layers in the next limb blocks, they are concatenated with the features maps from the same level before downsampling in the contraction path.  This helps to give the localization information from contraction path to expansion path. Finally, a 1x1 convolution is used to produce the prediction.The encoder and the decoder blocks are connected using a bottleneck block having 3 convolutional layers

Initially, the model used zero padding for the convolutional layers so, the input image size did not match with the output size. To deal with it, the authors proposed an overlap tile strategy involving a mirroring technique and some upsampling and downsampling. Later, it was modified to have padding for the convolutional layers and the input and output resolutions became equal.

![over](https://miro.medium.com/max/1114/1*GNB3UkI-hErQwvL-jDLU7A.png)

The authors also, introduced the idea of data augmentation in order to train the models, as the segmentation data creation takes lots of time and the datasets are not that vast.

### Variants: Resnet + Unet

Soon after the success of the Unet architecture, "The Importance of Skip Connections in Biomedical Image Segmentation" proposed to change the basic convolutional blocks with residual blocks. The paper proposed three types of blocks: A basic block, A simple block, and A bottleneck block. The three blocks make up the redesigned U-Net architecture. The paper says that the short skip connections among the blocks themselves allow for faster convergence when training and allow for deeper models to be trained.

![New](https://vitalab.github.io/article/images/resunet/sc01.png)

References:
1. https://arxiv.org/pdf/1505.04597.pdf
2. https://arxiv.org/pdf/1608.04117.pdf
3. https://towardsdatascience.com/understanding-semantic-segmentation-with-unet-6be4f42d4b47
4. https://towardsdatascience.com/review-u-net-biomedical-image-segmentation-d02bf06ca760
