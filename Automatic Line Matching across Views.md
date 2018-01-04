# Automatic Line Matching across Views
_by Cordelia Schmid and Andrew Zisserman from Department of Engineering Science, University of Oxford in 1999_

## short range motion
This is the image motion that arises in image sequences where simple nearest neighbour tracking would almost work. 

## long range motion
This is the image motionthatarises between views from a stereo rig, where the baseline is signiﬁcant(compared to the distance to the scene).

## Line detector
**Canny edge detector**

## F-guided matching
_inspired by epipolar constraint. __F__ is the fundamental matrix_.
_assuming F is known_
Corresponding image points **x** and **x'** satisfy the epipolar constraint **x'^T * F * x = 0**
The epipolar line corresponding to **x** is **Fx**.
The epipolar line corresponding to **x'** is **F^T * x'**.
suppose two image lines **l** and **l'**, a point **x** on **l** corresponds to the point **x'** which is the intersection of **l'** and the epipolar line of **x**.
For each segment in one image, a matching score is computed for all segments of the second image.
The epipolar geometry can also be used to reduce the search space.

## H-correlation score
