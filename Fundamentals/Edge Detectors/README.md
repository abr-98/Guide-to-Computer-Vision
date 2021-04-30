### Edge Detection 

Edge detection is one of the most significant tasks. The technique is used in image processing for tasks like Pattern Recognition and Feature extraction. 

Now, the idea behind how to detect edges is owing to the fact that the edges have much higher intensity value for the pixels lying on it. So, if we move across an edge, the intensity increases as we approach the edge and then it decreases as we move away from it. So, we use this particular feature foe edge detection. 

The best way of finding or detecting a continous change in pixel values as we move across the image is to focus on the gradient of the pixel values, as we move along the x or the y axis of the image plane. Some of the detectoes use first order derivatives for the detecting the change in gradient while others use second order derivatives for the reason.

Some of the most used filters for Edge Detection are:

1. Prewitt Edge Detector
2. Sobel Edge Detector
3. Laplacian Edge Detector
4. Robert Edge Detector
5. LoG or Marr Hildreth Edge Detector
6. Canny Edge Detector.

We have talked about Sobel and Laplacian in the Filters portion. 

**1. Prewitt Edge Detector:** The prewitt edge detectors are a couple of masks, one for detecting horizontal edges, other for vertical edges, obtained using the first order derivative along the Y and X axes repectively.

![Prewitt](https://miro.medium.com/max/541/1*q4Q2T52GyKi0tiF8fOUS1Q.png)

**2. LoG or Marr Hildreth Edge Detector:** Laplacian operator works on double derivative of the flow of intensity of pixels as we move along the axes of the image plane. So, laplacian operators are very sensitive to sharp changes in intensity of the images. Owing to the above facts, laplacian operators are very sensitive to noise as well. So, we need to eliminate the noise using a noise masking operator. For this case, we choose a Gaussian Kernel. So, first we use the gaussian kernel to remove the noise, then we use the laplacian kernel to detect the edges. Using Function of function we obtain the LoG or Laplacian of Guassian filter, which we convolve with the image. 
It is given by:
![form1](https://i0.wp.com/theailearner.com/wp-content/uploads/2019/05/log1.png?resize=211%2C49&ssl=1)
![form2](https://i2.wp.com/theailearner.com/wp-content/uploads/2019/05/Lapeq.png?w=610&ssl=1)

**3. Canny Edge Detector:** The canny edge detector is the most used edge detector of current times. The Canny edge detector works in four different steps:
1. Noise Removal: Like LoG, Canny Edge detector also uses a guassian filter mask to remove the noise from the image.
2. Gradient Computation: It calculates the gradient or the rate of change of intensity of pixels moving along the axes of the image.
3. Extract edges using Non-max supressions: Canny edge detector slides a kernel of size 3x3 over the image plane after calculating the gradients and tries to locate the local maxima, which are the edges detected
4. Hysteresis thresholding: Canny Edge detectors use a two threshold system, with an upper and a lower threshold, which just define a range of intensity. Its often seen that, noises are still not removed. So, canny detectors allows to set an intensity range within which the actual edge intensities should lie.

Refernces:
1. cse.usf.edu/~r1k/MachineVisionBook/MachineVision.files/MachineVision_Chapter5.pdf
2. https://medium.com/analytics-vidhya/a-beginners-guide-to-computer-vision-part-2-edge-detection-4f10777d5483
3. https://theailearner.com/2019/05/25/laplacian-of-gaussian-log/
4. https://ai.plainenglish.io/a-dive-into-canny-edge-detection-using-opencv-python-76326c2fa19c

