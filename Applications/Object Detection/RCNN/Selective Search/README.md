### Selective Search

Before we move into the details of selective search, we have to look at another algorithm **Felzenszwalb’s Algorithm**, which is a image segmentation algorithm, on which the selective algorithm is built.


#### Felzenszwalb’s Algorithm based Image Segmentation 

In case of image classification here is only one object, but for object detection and image segmentation we have more than one objects in an image. For multiple object detection we need to identify the regions that potentially contains an object. To solve this, a graph based segmenting method was proposed in order to mark and segment the similar portions of the image. 

We use a undirected graph G=(V,E) to represent an input image. One vertex vi ∈ V represents one pixel. One edge e=(vi,vj) ∈ E connects two vertices vi and vj. Its associated weight w(vi,vj) measures the dissimilarity between vi and vj. The dissimilarity can be quantified in dimensions like color, location, intensity, etc. The higher the weight, the less similar two pixels are. A segmentation solution S is a partition of V into multiple connected components, {C}. Intuitively similar pixels should belong to the same components while dissimilar ones are assigned to different components.

The graphs are created based on Nearest Neighbour policy. Each pixel is a point in the feature space (x, y, r, g, b), in which (x, y) is the pixel location and (r, g, b) is the color values in RGB. The weight is the Euclidean distance between two pixels’ feature vectors. 

We need to know 2 distance metrics to create the graph.

1. Internal distance: Int(C)=max(w(e)), where e ∈ MST(C,E) MST is the minimum spanning tree of the components. A component C can still remain connected even when we have removed all the edges with weights < Int(C).

2. Difference between two components: Dif(C1,C2) = min ( w(vi,vj)). Dif(C1,C2) = ∞ if there is no edge in-between.

3. Minimum internal difference: MInt(C1,C2)= min (Int(C1)+τ(C1), Int(C2)+τ(C2) ), where τ(C)=k/|C| helps make sure we have a meaningful threshold for the difference between components. With a higher k, it is more likely to result in larger components.

If the weights of two vertices belonging two different components C1,C2 is less than MInt(C1,C2), we merge the two components. 

Algorithm:

1. Edges are sorted by weight in ascending order, labeled as e1,e2,…,em.
2. Initially, each pixel stays in its own component, so we start with n components
3. Repeat for k=1,…,m:
4.    The segmentation snapshot at the step k is denoted as Sk.
5.    We take the k-th edge in the order, ek=(vi,vj).
6.    If vi and vj belong to the same component, do nothing and thus Sk=Sk−1.
7.    If vi and vj belong to two different components C1 and C2 as in the segmentation Sk−1, we want to                 merge them into one if w(vi,vj) ≤ MInt(C1,C2); otherwise do nothing.


![Image_ex](https://lilianweng.github.io/lil-log/assets/images/image-segmentation-indoor.png)

#### Selective Search Algorithm:

Selective Search algorithm is used to generate target regions which can contain the objects in the image. It initially uses the Felzenszwalb’s Algorithm based Image Segmentation for producing the similar regions.

1. At the initialization stage, apply Felzenszwalb and Huttenlocher’s graph-based image segmentation algorithm to create regions to start with.

2. Use a greedy algorithm to iteratively group regions together:
->First the similarities between all neighbouring regions are calculated.
->The two most similar regions are grouped together, and new similarities are calculated between the resulting region and its neighbours.

3. The process of grouping the most similar regions (Step 2) is repeated until the whole image becomes a single region.

The selective searches the proposed basic properties of images as similarity metrics between two regions ri and rj, like,

1. Colour
2. Texture
3. Size
4. Shape

By tuning the threshold k in Felzenszwalb and Huttenlocher’s algorithm, changing the color space and picking different combinations of similarity metrics, we can produce a diverse set of Selective Search strategies.


References:

1. http://cs.brown.edu/people/pfelzens/papers/seg-ijcv.pdf
2. http://www.huppelen.nl/publications/selectiveSearchDraft.pdf
3. https://www.pyimagesearch.com/2020/06/29/opencv-selective-search-for-object-detection/
4. https://lilianweng.github.io/lil-log/2017/10/29/object-recognition-for-dummies-part-1.html
