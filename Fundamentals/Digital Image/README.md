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

