## Pointwise operations

For the application of these operaors, we will consider each amplitude value of a pixel as X. The operations are pointwise, so the transformations are pixelwise. The transformation can be denoted as 

##### Y=T(X)

where X is the original pixel value and Y is the new pixel value after transformation for the same pixel.

### 1. Inversion

Thise operator converts the image into its  negative or inverse image, as shown in the image_negative.ipynb file. The transformation formulates as below:

**Y= (max_pixel_value-1) - X**

It is a completely linear transformation.


