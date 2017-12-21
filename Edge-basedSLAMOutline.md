## Direct Monocular Odometry Using Points and Lines
---------------------------
### advantages of the egde-based method
1. line is common in man-made environment.
2. Edges are more robust to lighting changes and preserve more information compared to single points.
3. In the mapping part, edge is used to speed up and increase stereo matching accuracy.
4. The detection of edges is less sensitive to lighting changes by nature.

### line-based and feature-based method
the line-based method is a kind of direct method which directly operates on the raw pixel intensity by minimizing photometric error without feature extraction.
feature based methods rely on feature point extraction and matching to create sparse 3D map used for pose estimation by minimizing reprojection geometric error.
Reprojection geometric error of keypoints is typically more robust to image noise and large geometric distortions and movement. 
Direct method on the other hand, exploits much more image information and can create dense or semi-dense maps. 

### core idea of this paper 
the author maintain a depth map for the keyframe then in the tracking part, the camera pose is recovered by minimizing both the photometric error and geometric error to the matched edge in a probabilistic framework.

### camera pose estimation
#### feature based VO
The camera pose is estimated by solving the PnP (Perspective N-Point Projection) problem to minimize geometric error which is more robust to image noise and has a large convergence basin.
#### Direct VO
It optimizes the geometry directly on the image intensities without any feature extraction so it can work in some textureless environments with few keypoints. 
The core idea is to maintain a semi-dense map for keyframes then minimize the photometric error which is a highly non-convex function thus it requires good initial guess for the optimization
#### Edge based VO
This method is a frame to keyframe monocular VO. We maintain a semi-depth map for the high gradient pixels in the keyframe. Then for each incoming new frame, there are three steps. 
1. detect line segments and match them with the keyframe’s edges. 
2. camera pose tracking. We minimize a combination of pixel photometric error and geometric reprojection error if the pixel belongs to an edge. 
3. we update the depth map through variable baseline stereo. Edges are used to speed up the stereo search for those edge pixels and also improve reconstruction through an efﬁcient 3D line regularization.
------------------
###Tracking
* the depth map of the reference frame is assumed to be fixed.
* The current image I is aligned by minimization of the photometric residual r(ξ) and line re-projection geometric error g(ξ) corresponding to two observation model: photometric intensity observation and edge position observations
$$r_i = $$
