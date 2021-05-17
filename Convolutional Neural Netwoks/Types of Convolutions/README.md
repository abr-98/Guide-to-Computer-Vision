### Types of Convolutions

As we have already seen, convolution layers are the chief and most important functional layers in the Convolutional Neural Networks. There are a number of different types of convolutional layers, with varying funtionalities. 

Based on dimensionality of applications, the convolutional layers, are divided into 2 types:

**1. 2-D Convolutional layers:** These filters work on 2D input images and extract the required feature map. The size of the feature maps to be extracted is given by:

!{Normal](https://miro.medium.com/max/435/1*1okwhewf5KCtIPaFib4XaA.gif)

Feature Map Size= ((Image Size - Filter size + 2* Padding) / Stride) + 1

The functionalities are performed on 2D units of the Images, termed as Pixels. 

We can preserve the size of output feature image same as the input image, using the padding parameter, padding ="same", and keeping the stride=1. 

We can also reduce the size of the ouput feature image compared to the input image, using the padding="valid" and stride=2. This is called **Strided Convolutions**, and is used in place of Pooling layers, to reduce the number of parameters and the size of the feature maps.

**2. 3-D Convolutional layers:** These filters work on 3D input volumes and extract the required feature map. The size of the feature maps to be extracted is given by:

The functionalities are performed on 3D units of the Images, termed as Voxels.

Now, convolutions have been modified to obtain several versions from the normal versions, as discussed previously.

### Dilated Convolutions (Atrous Convolutions)

![Dilated](https://miro.medium.com/max/435/1*SVkgHoFoiMZkjy54zM_SUw.gif)

Dilated convolutions were created, to obtain a larger size receptive field and at the same time, restricting the number of parameters. For example, in the above diagram, the kernel filter has 9 parameters, as of 3x3 kernel, but it's receptive field is same as a 5x5 kernel. It helps to obtain a broader field of vision. The above one is a 3x3 kernel, with a **dilation rate** of 2. The dilation rate is the parameter that controls how big is the kernel. For dilation rate n , n-1 zero rows and columns are inserted alternatively, after a wieght in a kernel.

In dilated convolutions, also, similar to normal convolutionsm we can preserve the size of the output feature maps using padding= dilation rate. In several cases, dilated convolutions have been used to replace pooling layers, by using them with stride=2.  

### Transposed Convolutions 

In cases like segmentation, we need to upsample from the final output feature maps. In such cases, we have used upsampling techniques like bilinear interpolation methods. But in order to upsample from so small feature maps,upsampling results in aliasing effects, and also causes loss in localized information. To deal with such problems, a learned convolution has been proposed. The Transposed convolutions or Deconvolutions, return the upsample image from a feature map. 

To achieve this transposed convolutions use a designed padding pattern and a normal convolutional kernel as shown here.

![Transpose](https://miro.medium.com/max/435/1*Lpn4nag_KRMfGkx1k6bV-g.gif)

