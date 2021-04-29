### Filters:

Filters and Kernals are basically image modifiers which act on a Pixel of Interest based on the Neighbouring Pixels. Please refer to Operations portion to have a clear idea about Neighbourhood. 

![filters](https://www.researchgate.net/profile/Nilesh-Bahadure/publication/286442762/figure/fig10/AS:670370642268178@1536840224859/The-Mechanics-of-Spatial-Filtering.ppm)

As shown in the figure above, the mask is called the kernel or filter. The filter shown is a 3x3 filter. Similarly, we can have 2x2, 5x5 and 7x7 filters, depending upon requirements of the neighbourhood. The (0,0) in the mask is coincides with the pixel of interest (x,y) of the image, f(x,y). Similarly the whole mask or filter just coincides with the pixels of the image, and gives a response according to the filter type. Now, the w(a,b) defines the weight of the filter at that particular index of the filter. The weight of the filter indices are dependent on the type of filter they are and the type of tasks they perform. 

Each filter has a response, which becomes the updated value of the pixel of interest at the center. The response is given by:

**Response= f(x-1,y-1).w(-1,-1) + f(x-1,y).w(-1,0) + f(x-1,y+1).w(-1,1) + f(x,y-1).w(0,-1) + f(x,y).w(0,0) + f(x,y+1).w(0,1) + f(x+1,y-1).w(1,-1) + f(x+1,y).w(1,0) + f(x+1,y+1).w(1,1)**

The filter slides over the entire image, and how the masks slides is controlled by a measure called **Stride**.

Filters are normally used for image smoothing, sharpenining and edge enhancements. Filters can be present in both spatial and frequency domains. We are going to talk about the spatial domain filtering.

### 1. Smoothening or Blurring Filters:

They smoothen out or blur the image upto some extent to reduce Noise. There are Linear and Non-Linear Smoothening operators. 

##### Smoothening Linear Filters:

**Mean Blur Kernel:** The response of this filter is just the mean value of the pixels in the neighbourhood of the pixel of interest, covered by the kernel.

![Mean](https://miro.medium.com/max/187/1*wJfPULU0I_OnskXTkWjqkA.gif)

**Weighted Average Kernel:** The response of this kernel is similar to the Mean Blur kernel except the fact that this kernel takes the wieghted average of the neighbours. 

![Weighted](https://miro.medium.com/max/432/1*rnHldrVN7DAqGX6fe_2IGQ.png)

**Guassian Average Kernel:** Gaussian kernel is also another weighted mean blur kernel, whose weights follow the bell shaped curve Gaussian distribution. 

![Gaussian](https://miro.medium.com/max/526/1*CHbVU4ykR7yWS3nd2ayrwg.png)

The kernel distributions and weights can be varied using the mean ad the standard deviation according to requirements as shown in the implementations.

##### Smoothening Non Linear Filters:

The non-linear filters mostly consists of three types of filters, the MIN, MAX and the MEDIAN filters, which are used for smootheining. Accordingly, as their name suggests, the filters return the Maximum, Minimum and Median values of the pixel values covered by the filters over the image.




