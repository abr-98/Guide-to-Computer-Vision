## Pointwise operations

For the application of these operaors, we will consider each amplitude value of a pixel as X. The operations are pointwise, so the transformations are pixelwise. The transformation can be denoted as 

##### Y=T(X)

where X is the original pixel value and Y is the new pixel value after transformation for the same pixel.

### 1. Inversion

This operator converts the image into its  negative or inverse image, as shown in the image_transformation_1.ipynb file. The transformation formulates as below:

**Y= (max_pixel_value-1) - X**

It is a completely linear transformation.

### 2. Image Thresholding

The operator make all the pixel values above a particular threshold equal to the maximum value and all the pixel values below a particular threshold equal to the minimum value. Its working has been shown in the image_transformation_2.ipynb file

### 3. Context-Stretching:

It is an image enhancement technique. There are several types of Context stretching operations:

##### MinMax Context Stretching:

It is achieved by the equation: 

**P_new(i,j)= ( (P_old(i,j) - min(P_old) ) / ( max(P_old) - min(P_old))* 255**

where P_old is the given image, and max(P_old) depicts the highest pixel value.

##### Percentile Stretching

### 4. Grayscale slicing:

The operator make all the pixel values above a particular threshold equal to the maximum value and all other pixel values remain intact. Its working has been shown in the image_transformation_3.ipynb file

### 5. Logarithmic Stretching:

This enhancement technique is used a lot in FFTs. It is given by:

**Y= C.log(1+x)**, where C is a constant

### 6. Power-law transform:

This enhancement technique is given by:

**Y= C.(X+*lambda*)^*gamma***

Here gamma is the exponential parameter, that gives a number of variants based on its value. C is the constant.

### 7. Histogram Equalization:

It is a simple technique to improve the contrast of an image and enhance it. It is often seen that, in images pixel values get confined in a particular range, for example, for bright images, the pixel  values are mostly confined to higher value region. This results in a low contrast image.

![Equalization](https://repository-images.githubusercontent.com/196091044/195dce80-a2b1-11e9-8028-f8688944258f)

Histogram equilization spreads the pixel values over the range as shown in the above diagram, increasing the image contrast, by creating an equal probable distribution for all the pixel values to occur. The process can be achieved using opencv, easily as shown in the fourth module file. 




