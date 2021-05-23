### Histogram of Gradients (HOG)

Histogram of Gradients or HOG is one of the most used traditional feature descriptors, for the object detection tasks. 

#### Gradients: 
Gradients are the rate of change of pixel values. Now, image is a 2D function f(x,y). So, to find the rate of change of pixel values, we need to calculate the derivative for f(x,y), so we will need to calculate the partial derivative of the function, wrt x and y. The derivative can be calculated using laplacian.

∇f(x,y)= \[gx   gy] = \[∂f/∂x  ∂f/∂y] = \[f(x+1,y)−f(x−1,y)  f(x,y+1)−f(x,y−1)]

where,

![loc](https://lilianweng.github.io/lil-log/assets/images/image-gradient-vector-pixel-location.png)

It is given as the above as image is a discrete function on saving on a digital device.

Magnitude of the gradient = Sqrt ( gx^2 + gy^2)
Direction of the gradient = arctan ( gy / gx )

Now, in the original scenerio, it is much easier to use the given kernels in order to calculate the gradients. 1st filter can be convoluted to get ∂f/∂x and 2nd to get ∂f/∂y.

![grad](https://learnopencv.com/wp-content/uploads/2016/11/gradient-kernels.jpg)

They can also be calculated using standard filters like Sobel and Prewitt filters. These filters can also be used to find gradients. 

![HOG](https://learnopencv.com/wp-content/uploads/2016/12/hog-cell-gradients.png)

The gradients are a very good indicator of boundaries and  sharp edges. The magnitude of gradient sparks if we cross a boundary. Otherwise, gradients removes the parts where the gradient is almost constant.

#### HOG

In order to create HOG, we take the entire image, and correspondingly the matrix of magnitude of gradients and the matrix of gradient directions. Next we divide the image into several 8x8 pixel cells In each cell, the magnitude values of these 64 cells are binned and cumulatively added into 9 buckets of unsigned direction.

For better robustness, if the direction of the gradient vector of a pixel lays between two buckets, its magnitude does not all go into the closer one but proportionally split between two. For example, if a pixel’s gradient vector has magnitude 8 and degree 15, it is between two buckets for degree 0 and 20 and we would assign 2 to bucket 0 and 6 to bucket 20.

![dist](https://lilianweng.github.io/lil-log/assets/images/HOG-histogram-creation.png)

Using the above method HOG is found.

Next, we create 2x2 window of such 8x8 pixel cells. So, each window contains 4 such 8x8 pixel cells. We have previously seen, from 8x8 pixel cells, we create 9x1 Histogram vector. So, from the 2x2 window we can concatenate the 4 9x1 vector, to create a 36x1 vector. This is done in order to normalize. Normally, if we use thw values without normalization, it would be very effective to light, which we do not want. Normalizing a larger vector of 36x1 proves to be more robust than a normalizing a 9x1 vector, so we adapt the sliding window.

Now, initially, the method was performed for human detection, so the authors focused on the image patches of size 64 x 128, and then conducted the whole experiment. 

So, considering the size of the patch, we calculate how many 16x16 blocks can be there. If there are m patches horizontally and n patches vertically, for the final vector we send the concatenated vector of size 36x1 from all the windows. The total size resulting to: (m x n x 36 , 1).

This vector we send to predictive algorithms like SVM, for object detection. 

Now, this method can be applied to any patch of aspect ratio 1:2 like 100 x 200, 105 x 210 and so on, which can be resized to 64 x 128. As far as the size 8x8 cell goes, it is due to the initial problem setting. The authors found that for a image of dimension 64 x 128, 8x8 size cells was based suited for detecting features like faces, etc.


References:

1. http://lear.inrialpes.fr/people/triggs/pubs/Dalal-cvpr05.pdf
2. https://learnopencv.com/histogram-of-oriented-gradients/
3. https://lilianweng.github.io/lil-log/2017/10/29/object-recognition-for-dummies-part-1.html



