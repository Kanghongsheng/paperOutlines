
#Robust Stereo Visual Odometry through a Probabilistic Combination of Points and Line Segments
---------
## feature detector
Point Features: ORB detector
Line Segment Feature: Line Segment Detector(LSD)

##Problem Statement
### point projection error:
### line projection error:
a vector formed by the euclidean distances
from the projected endpoints of the line segments in the ﬁrst frame and the line detected in the second frame.
### Optimization
iterative minimization of the Maximum Likelihood Estimator(MLE). 
through iterative Gauss-Newton optimization on the manifold tangent space.
### Outlier Rejection
