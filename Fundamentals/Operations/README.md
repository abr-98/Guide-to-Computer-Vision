### 1. Neighbourhood of an Image Pixel.

In order to have a fundamental knowledge about operations of image processing we must have the knowledge of neighbourhood of a pixel.

![Neighbourhood](https://www.researchgate.net/profile/Ana-Siravenha/publication/221317837/figure/fig1/AS:305627109838848@1449878589041/N-aN-pixels-neighborhooda-4-neighborhood-b-8-neighborhood-9.png)

The above images show the two types of neighbourhood there exists. The centre pixel is the **Pixel of Interest (x,y)** in both cases. The first image (a) of the above figures shows **N-Four Neighbours**, and the second image (b) of the figures show **N-Eight Neighbours** respectvely. It also shows how they are referred with respect to the pixel of interests as  (x+n,y+n), n being 0 or 1 based on the adjacency of the neighbour from the POI


### 2. Operations On an Image

There are several image transformations which take in an image as a 2D function of (x,y), say input image as, F1(x,y) and produce output image signal as function F2(x,y). Overall these transform operations can be divided into three basic types:

**1. Pointwise Operations:** The output value at a specific pixel is dependent only on the input value at that same pixel. 

**2. Local Operations:** The output value at a specific pixel is dependent on the input values in the neighborhood of that same pixel.

**3. Global Operations:** The output value at a specific coordinate is dependent on all the values in the input image..
