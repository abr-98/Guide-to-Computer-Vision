### Filters:

Filters and Kernals are basically image modifiers which act on a Pixel of Interest based on the Neighbouring Pixels. Please refer to Operations portion to have a clear idea about Neighbourhood. 

![filters](https://www.researchgate.net/profile/Nilesh-Bahadure/publication/286442762/figure/fig10/AS:670370642268178@1536840224859/The-Mechanics-of-Spatial-Filtering.ppm)

As shown in the figure above, the mask is called the kernel or filter. The filter shown is a 3x3 filter. Similarly, we can have 2x2, 5x5 and 7x7 filters, depending upon requirements of the neighbourhood. The (0,0) in the mask is coincides with the pixel of interest (x,y) of the image, f(x,y). Similarly the whole mask or filter just coincides with the pixels of the image, and gives a response according to the filter type. Now, the w(a,b) defines the weight of the filter at that particular index of the filter. The weight of the filter indices are dependent on the type of filter they are and the type of tasks they perform. 

Each filter has a response, which becomes the updated value of the pixel of interest at the center. The response is given by:

**Response= f(x-1,y-1).w(-1,-1) + f(x-1,y).w(-1,0) + f(x-1,y+1).w(-1,1) + f(x,y-1).w(0,-1) + f(x,y).w(0,0) + f(x,y+1).w(0,1) + f(x+1,y-1).w(1,-1) + f(x+1,y).w(1,0) + f(x+1,y+1).w(1,1)**

The filter slides over the entire image, and how the masks slides is controlled by a measure called **Stride**.

Filters are normally used for image smoothing, sharpenining and edge enhancements. Filters can be present in both spatial and frequency domains. We are going to talk about the spatial domain filtering.


