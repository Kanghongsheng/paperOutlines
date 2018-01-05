# Robust Line Matching Based on Ray-Point-Ray Structure Descriptor
_by Kai Li, Jian Yao, Xiaohu Lu of Wuhan University in 2014_

## Keywords
two-view line matching method; Ray-Point-Ray structures; SIFT-like descriptor 

## difficulties
1. instability of endpoints of line segments; 
2. the lost of connectivity of line segments.

## line matching method
At the place of the junctions, a Ray-Point-Ray (RPR) structure is formed, consisting of a junction point and two rays (line segments) connected to the point
RPRs are described with a robust SIFT-like descriptor.

## Partial Line-Connectivity Recovery
Problem:Line segments extracted by EDLines and LSD line segment detectors are often separated with each other.
Resolution: reﬁning them by partially recovering their connectivity through exploiting the gradient map of the original image.
Steps:
1. two circles centered at its two endpoints with the same radius, _d_.
2. Other line segments fall inside these two circles are neighbors.
3. for a searched neighbor line segment, if the orientation difference between _l1_ and _l2_ is less than a given threshold _alpha_, merge the two line segments to a long one.
4. adjust the endpoints of the mew line segment to maximize its Gradient Magnitudes(GM).
5. If the GM of the merged line segment is greater than 80% of the sum of that of _l1_ and _l2_, we accept it and use it to replace _l1_ and _l2_ for further steps.
6. If the direction diﬀerence between l1 and l2 is above α, we intersect them and generate a junction.
7. If the distance between the junction and the endpoint of l1 is less than d, we accept the junction and extend l1 to the junction.

## Line matching

### RPR construction

#### The principle of forming RPRs from connected line segments:
any two line segments which connect with a common joint point but are not in the same line can be used to form a RPR.

### RPR Descriptor
using the directions of both rays as dominant directions of the point and generate orientation histograms.
1. dominant direction selection
2. The description region is split into 4 subregions along the height, generate 4 rectangles with the same size.
3. In each subregion, an orientation histogram containing 8 bins is constructed
4. For each pixel in the rectangle, its gradient magnitude is weighted and added to corresponding entry of certain histogram according to its gradient orientation.

### Global Image Scale Change Estimation
1. Gaussian pyramids for original reference and query images.
2. the pyramids have 4 octaves with 4 layers in each octave.
3. the original reference image is to match all images in the pyramid built for the query image with their RPRs. 
4. The pair of images producing the most putative RPR matches is regarded to be in the same scale 

### RPR Match Propagation
To achieve a stable and precise fundamental matrix, we ﬁrst use RANSAC to estimate an initial fundamental matrix and reﬁne it by the Normalized 8-point Method and Levenberg-Marquardts optimization in order.
The RPR match propagation is achieved by progressively increasing the threshold for the distance of an accepted point match according to the fundamental matrix.
three pairs of points in each RPR match: one pair of junctions and two pairs of endpoints of the two pairs of rays.
the match based criteria:
1. the distance of their descriptors should be less than a given threshold
2. the DFM of the test endpoint pair should be less than a pre-deﬁned threshold

#### RPR match Filtering
by exploiting the topological consistency between RPR matches and their neighbor point matches.
the topological consistency is performed by evaluate the RPRs locating in the same quadrants.

### Single Line Segment Matching
#### Steps
1. group single line segments based on matched RPRs
2. match them in corresponding groups

### advantages of this description
1. efficiency and keep its distinctiveness.
2. avoid the possible shift of the point along the ray.
