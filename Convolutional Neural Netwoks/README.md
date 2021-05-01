## Convlutional Neural Networks

There have been many approaches to solve Computer Vision problems. The most popular approach is the application of deep learning architecture that is the use of Convolutional Neural Networks.

### Basic Idea

Most of the fundamental operations in this field are dependent on the answer to a simple question “HOW SIMILAR ARE THE IMAGES?”. Say, for example, object detection or classification, an image set is given to a computer using which the computer has to label or detect a new image. This task seems pretty easy for humans because we can see. The computer answers this question by comparing how much the pattern of one image matches the other image pattern. By pattern, we mean the pattern in the array structure of the two images. 

![CNN1](https://miro.medium.com/max/700/0*alvTaRr1j-IOnKGG)

Here we can see that the X is rotated and as a result its array substructure changes. It becomes hard for the computer to get a 100% match, so it just compares and checks small patterns to decide if the two images match.

![CNN2](https://miro.medium.com/max/700/0*UJ-jwmPEKbVIFUZQ)

We can see the patterns in the boxes match each other. So the computer can also judge these similarities and based on these it decides the answer to the basic question. These patterns are extracted by the computer as features of an image. Later, the computer tries to find these features in a new image it receives. If the same features are found in the new images it is classified as the target class else not, or if a part of the new image carries similar features as experienced in the training set, it is detected as an object. 

### Convolution

Convolution is a mathematical operation on two functions (f and g) that produces a third function expressing how the shape of one is modified by others. A second function g(t) is passed over a function f(t). The product of the two functions at a point t is found and the values are integrated to devise the third function. It is given by:

![formula]
