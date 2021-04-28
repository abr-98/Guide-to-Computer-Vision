## Pointwise operations

For the application of these operaors, we will consider each amplitude value of a pixel as X. The operations are pointwise, so the transformations are pixelwise. The transformation can be denoted as 

##### Y=T(X)

where X is the original pixel value and Y is the new pixel value after transformation for the same pixel.

### 1. Inversion

This operator converts the image into its  negative or inverse image, as shown in the image_negative.ipynb file. The transformation formulates as below:

**Y= (max_pixel_value-1) - X**

It is a completely linear transformation.

### 2. Image Thresholding

The operator make all the pixel values above a particular threshold equal to the maximum value and all the pixel values below a particular threshold equal to the minimum value. Its working has been shown un the image_threshold_and_stretching.ipynb file

### 3. Context-Stretching:

It is an image enhancement technique. There are several types of Context stretching operations:

##### MinMax Context Stretching:

It is achieved by the equation: 

**P_new(i,j)= ( (P_old(i,j) - min(P_old) ) / ( max(P_old) - min(P_old))* 255**

where P_old is the given image, and max(P_old) depicts the highest pixel value.

##### Percentile Stretching



