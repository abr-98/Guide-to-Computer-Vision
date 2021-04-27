### Digital Image

Before we start learning about Image Processing, we need to learn about the fundamentals of digital imaging, their structures and operations.

**Digital Image is the presentation of an image in the form it can be stores in a computer.** 

Normally, Image is 2 dimensional spatial signal, which is continous in nature, something as being shown by the below diagram. 

![Image_2D](https://media.springernature.com/lw785/springer-static/image/chp%3A10.1007%2F978-981-10-2537-2_3/MediaObjects/428094_1_En_3_Fig7_HTML.gif)

It is impossible to store such a continous 2D signal so, we adapt a few techniques.

### 1. Spatial Discretization

![Discretization](https://www.researchgate.net/profile/Sean-Wood-2/publication/44126806/figure/fig2/AS:452113244397568@1484803605822/Conceptual-depiction-of-discretization-in-time-and-amplitude-a-source-signal.png)

As shown in the above figure, (a), we hava a continous signal, which we can't store. So, we sample the continous signal at some points as shown in (b), to obtain some discrete velues, such that for a particular (x) we have the value of the function f(x) represented by the curve. (c) gives the signal which can be reconstructed from the sampled signals. But for the reconstruction to be possible the sampling frequency must be >= 2 the bandwidth of the original signal. This is called **Nyquist Sampling Theory**. The method is called discretization. 

We saw the above example on a 1D data, but for storing an image we perform this operation on a 2D spatial data, and obtain discrete values all over the image plane (x,y), which represents the value of the function f(x,y) that represents that particular image signal. The values depict the amplitude of the signal at that point (x,y). The points of sampling all over the plane of the image are known as **Pixel Points**

This whole process is called spatial discretization.

### 2. Controlling Resolution: 

Resolution is the measure of the number of pixel values, more the number of pixel points, more is the resolution. We have discussed in the spatial discretization portion, we sample the continous signal all along the 2D space, Now, if look very closely at (c) figure, we will see, that the signal values between the two sampling points are constants, and so looks a bit blockish.

For 1D signal, we just needed to drop some 1D lines on the signals, to discretize it. For 2D image signals we distribute the image into small grids, at the centre of the grid is the sampling point, and the whole grid represent the pixels.

![Resolution](https://www.scientiamobile.com/wp-content/uploads/2018/12/Pixel-Density.jpg)

As it can be seen in the above diagram, the same image has been discretized in two different manner. In the 1st image pixel density (unit: Pixel per inch) is much lower than the 2nd one. The amplitude recorded at the value of sampling spans over the full representing 2D pixel grid. As a result, the second image captures much more distinct and large number of pixel values than the first image. The first image provides much more of a blocky effect due to the reason we saw in the 1D case, and has a lower resolution and hence a lower clarity.

### 3. Quantization of Pixel Values:

As we have already seen, image to be a constant 2D signal, it ranges over all Natural Numbers including decimal values. If we have to store decimal values, we need a large number of bits to save the amplitude of even one of the sampling points. For example, if the value of the signal is 78.93 at one point, it will take up a high number of bits, So, we use the concept of quantization.

![Quantization](https://www.tutorialspoint.com/digital_communication/images/quantization.jpg)

The above image describes quantization of image signal, as we can see any signal value in the range of (a,b), is replaced by value a or value b depending on quantization policy. Now, in this image the axes represents number from 0-16 in binary. In image cases we create divisions from 0 to 255, total of 256 levels of quantizations, So, if we get a pixel value of 78.93 it is mapped as 78, which can be represented as a 8 bit number. So, for representing any pixel value we need 8 bits. The error generated due to quantization is called **quantization error**. More the number of levels, less is the quantization error, more is the memory required. It has been observed that, the quantization error effect is not significant if we use 256 levels of quantization. So, it has been adapted as standard,and the highest value of any pixel is 255. 

### 4. Channels of an Image

As we have seen in the Quantization portion, the pixel value varies from 0-255, and value represents the intensity of the pixel. If we consider a colour say white, 0-255 each value gives a different intensity of white, 0 being black and 255 being white, so we get a complete shade palette. Again, if we see another colour say red, each value from 0-255 gives a different shade of red. As we know, a every colour is a combination of some primary colours in case of images also, this theory holds. 

![Channel](https://miro.medium.com/max/311/1*uMda2KGCQFb6sZm8Cli7tA.png)

If you see the upper image, the first colour image is created by the super position of the other 3 images in primary colours Red, Blue and Green, pixel by pixel. So, the image is said to have 3 channels: Red, Blue and Green (RGB). These 3 channels are also present in diigital cameras. Grayscale images have only 1 channel, while RGB images of 3 channels. So, for saving an RGB image, we need 24 bits for each pixel, 8 bit per pixel for each channel.




