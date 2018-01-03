# Wide-Baseline Stereo Matching with Line Segments
_by Herbert Bay, Vittorio Ferrari of ETH Zuerich_

## Contribution
This paper propose a novel matcher for straight line segments, based on their appearance and their topological layout.

## Features
This matcher can work in a completely **uncalibrated** setting.

## Algorithm
This approach exploits the appearance similarity of pairs of line segments, and the topological relations between all line segments. 
If region matches are available, they are automatically integrated in the topological conﬁguration, and exploited in combination.

### Steps
1. **viewpoint-invariant region matcher**.(Optional) 
This is applied in order to get a set of initial region matches. 
2. **Line segments detector**
3. **Color histogram based matching**. in order to get initial candidate matches.  
The line segments in both views are compared based on the **histograms of the neighboring color proﬁles**
4. **topological ﬁlter**. 
remove wrong candidate matches.
5. **Mpre matches**. 
found by iteratively reintroducing unmatched line segments which respect the topological structure of the current set of matches 
6. **epipolar geometry**.  
estimated after an intermediate step of coplanar grouping using homographies.

### Line descriptor
HSV(the Hue channel, Saturation and Value) images.
use two color histograms _h_ of _pesai^R_ and _pesai^L_ as descriptor of a line segment.
each bin _h_m_ contains the number of pixels of _pesai_ having a certain color _m_.

### match strategy
1. segment of I2 is compared to all segments in the I2
2. if the dissimilarity is below 0.25, then this pair is considered as a candidate match.
3. only the 3 with the lowest dissimilarity are kept

### Topological ﬁlter
1. use pair and triplet topology to filter the mismatch.
2. for every feature we compute a violation score which counts the number of violated constraints for all unordered triplets/pairs including it.

### disadvantages
The average computation time for the matcher was 8 seconds on a modest workstation (Pentium 4 at 1.6GHz, line detection not included). 

## Epipolar geometry estimation
_assuming the scene contains at least two planes_
The idea of this method is to group **coplanar** segments using homographies.
estimate the fundamental matrix from these point matches using **RANSAC**.

## confusion
1. how to eliminate the influence of the line caused by sunlight?

## idea
1. when matching, we are not going to compare segment A in the image I1 to all the segments in the image I2. 
we are supposed to match the special features first. then the common features.
