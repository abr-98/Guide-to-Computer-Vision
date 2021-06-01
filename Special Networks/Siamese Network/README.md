### Siamese Network

The idea of siamese network was first proposed by Lev V. Utkin in the paper titled "An explanation method for Siamese neural networks". The Main focus of the Siamese Network was to deal with classifications where there is a shortage of data, or a severe imbalance, like face detection or signature detection mechanisms. It is impossible to obtain large number of data.

The SNN basically works on an autoencoder based idea. It passes two images through two similar networks, i.e, same architecture, and weights so two corresponding feature maps are obtained. Then the similarity between the obtained feature maps is checked. If they difference is less, the objects are similar and vice versa.

#### Architecture

![Arch](https://miro.medium.com/max/770/1*I7a9aVN2poHUtiHSq2q44Q.png)

The above image gives the architecture. So, we have two models but they are same in weights and structure. It can be said that they are instances of the same model. On being passed two images, it returns 1 if they are similar, else returns 0. Siamese networks convert the classification problem into a similarity problem, and learns from semantic similarity, as the features are obtained from same semantic embeddings. 

#### Losses

The model is trained o minimize the distance between samples of the same class and increasing the inter-class distance. The most used losses are: 

1. **Contrastive loss:**  In Contrastive loss, pairs of images are taken. For same class pairs, distance is less between them. For different pairs, distance is more. This loss is used to learn embeddings in which two similar points have a low Euclidean distance and two dissimilar points have a large Euclidean distance. It is given by:


**L = Y * D^2 + (1-Y) * max(margin — D, 0)^2**

D is the distance between image features. ‘margin’ is a parameter that helps us pushing different classes apart.

1. **Triplet loss:**  The model takes three inputs- anchor, positive, and negative. The anchor is a reference input. Positive input belongs to the same class as anchor input. Negative input belongs to a random class other than the anchor class. The idea behind the Triplet Loss function is that we minimize the distance between the anchor and the positive sample and simultaneously also maximize the distance between the anchor and the negative sample. It is given by:

**Loss L= max(d(a,n) — d(a,p), 0)**

where d is the distance metrics, a is the reference, p is the positive example and n is the negative. So, in order to maximize this we need to have d(a,p) < 0 and d(a,n) to have a positive high value. 

References:

1. https://arxiv.org/pdf/1911.07702.pdf

Application:

https://ai.plainenglish.io/an-approach-towards-building-a-gui-based-and-voice-controlled-security-lock-mechanism-based-on-f06b47d0426e
