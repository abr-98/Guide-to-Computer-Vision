### Noise in image processing:

Before startiing to learn about Noise Filtering in image processing, we must take a look at the noises that exist in images and what noise actually is. 

Suppose I(x,y) denotes the intensity of the pixel (x,y) in an image.The Intensity is made of two components: value of the image signal F(x,y) at the pixel concerned and the value of noise at the pixel N(x,y). 

##### I(x,y) = F(x,y) + N(x,y)

Noise is a random variation of brightness or colour information in images. It obsecures the desired value of the image signal function and thus the information.

There are two types of noise models: 

1. Additive noise 
2. Multiplicative noise.

Other than this there are basic 4 types of noise which are very common in images.

**1. Gaussian Noise:** The probability Density Function of this type of noise follows the Normal distribution or guassian distribution with mean *nu* and standard deviaton *sigma*

**2. Salt and Pepper Noise:** This type of noise has two values for each pixel: 0(black->pepper) and 255(white->salt) for 8-bit images.  They cause sharp and sudden disturbance in the image signal.

**3. Poisson's Noise:** The probability Density Function of this type of noise follows the Poisson distribution 

**4. Speckle Noise:** It exists naturally and can be created by randomly multiplying random pixel values with different pixels of an image.

### Image Denoising:

There are several ways to remove noise from images, some of them are spatial domain methods, and some of them are in the frequency domain, which need to be deployed after conducting a Fast Fourier Treansform, to convert the spatial domain into frequency domain. Some Noises best suite some specific denoising methods. 

Some basic techniques of Image Denoising are:

1. Mean filter, Weighted Averaging filters
2. Median Filter
3. Gaussian Filter
4. Weiner Filter.

We discussed first three while discussing Filters. Now we move to Weiner Filter.

##### Weiner Filter.

This filter tries to minimiza the mean squared error (MSE) between the noisy image and the original image signal.

The equation of Weiner filter obtained while reducing MSE error is -

![Weiner](https://iq.opengenus.org/content/images/2019/07/Untitled-Diagram--14-.png)

Where,

||H(x, y)||^2 = H(x, y)H*(x, y);
H(x, y) = degradation function;
H*(x, y) = complex conjugate of degradation function;
Sn(x, y) = ||N(x, y)||^2 i.e. Power spectrum of Noise;
Sf(x, y) = ||F(x, y)||^2 i.e. Power spectrum of undegraded(original) image;

References:
1. https://medium.com/image-vision/noise-in-digital-image-processing-55357c9fab71#:~:text=There%20are%20three%20types%20of,value)%20all%20over%20the%20image.
2. https://medium.com/image-vision/noise-filtering-in-digital-image-processing-d12b5266847c
3. https://pub.towardsai.net/image-de-noising-using-deep-learning-1a8334c81f06
4. https://towardsdatascience.com/introduction-to-image-denoising-3e269f176483
5. https://iq.opengenus.org/image-denoising-and-image-processing-techniques/
6. https://www.ijcaonline.org/volume9/number4/pxc3871846.pdf





