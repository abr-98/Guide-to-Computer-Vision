### Feature Extraction in Deep Learning

We have discussed a lot about traditional feature extractors, similarly, there have been attempts to develop feature extractors, using deep learning as well. One of the extracting models very popularly used is the **Feature Pyramid Network**. The concept of Pyramid networks is widely used in most classification and segmentation problems. 

The Pyramid Networks are based on the idea that if we apply convolutions, in order to extract features, from the same image at different spatial resolutions, each of the resolutions, will provide different feature maps that will focus on different views and fields of the image. Thus, we can obtain a much better and precise feature representation of the image.

Initially, the idea was implemented through the creation of the image pyramid.

![Pyramid](https://miro.medium.com/max/600/1*UAee9W6LRTIYT0ygCFAdmw.png)

As shown in the above figure, the actual image, is upscaled to double the size and downscaled to half the size, in order to create the pyramid. Now, here the catch is downscaling causes a loss in information, so, prior to that a guassian filtering is use, to spread the information. 

The operations of upscaling and downscaling can be performed using opencv in python. But using convolutional layers on so many layers seperately is a very time consuming and costly task, to solve this issue FPN or feature Pyramid Networks were introduced.

![Feature_P_1](https://miro.medium.com/max/1380/1*D_EAjMnlR9v4LqHhEYZJLg.png)

FPN uses the multi-scale feature maps from different layers. It has a two pathway system, a bottom-up pathway and a corresponding top-down pathway. The bottom-up path way, uses a deep convolutional network backbone like, VGG-19 or Resnet. The bottom up pathway provides the rich low resolution feature maps from the image. Every stage in the bottom-up layer processes the image, and reduces the resolution by half before sending it too the next layer, with application of a pooling layer.

The bottom up layer help to extract the best semantic features, while the top down layer, upsamples the feature maps at every stage to get the localized features, that can be found from more high resolution images. Every stage in the top-down limb upsamples the feature map by 2, using nearest distance weighted interpolation method. The upsampling layers in known to create an aliasing effect, so, an extra input from the corresponding layer from the bottom up limb is added after upsampling using a lateral connection. The input from the bottom up limb is passed through a 1x1 convolution, in order to resize the number of channels as, to add we need the two inputs to have same dimension and number of channels. The addition helps to focus on smaller and finer features while processing.

We extract features from all the levels of the top down limb in order to obtain multi scaled features. So, we obtain 4 seperate feature maps, one from each layer, which are flattened and passed into the fully connected layers for classification tasks.

References: 
1. https://arxiv.org/pdf/1612.03144.pdf  
2. https://medium.com/analytics-vidhya/a-beginners-guide-to-computer-vision-part-4-pyramid-3640edeffb00 
3. https://docs.opencv.org/3.4/d4/d1f/tutorial_pyramids.html 
4. https://towardsdatascience.com/review-fpn-feature-pyramid-network-object-detection-262fc7482610 
5. https://jonathan-hui.medium.com/understanding-feature-pyramid-networks-for-object-detection-fpn-45b227b9106c 

An example shown in the file.

Label: 0 -> cat, 1 -> dog

The file structure:\

Train---|\
        |- Cat\
        |- Dog\
Validate|\
        |- Cat\
        |- Dog\
Test----|\
        |- Cat\
        |- Dog

The designed network is a feature pyramid network.



