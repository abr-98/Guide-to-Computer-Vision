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






