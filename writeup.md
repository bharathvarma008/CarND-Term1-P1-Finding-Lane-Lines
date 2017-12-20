# **Finding Lane Lines on the Road** 

## Writeup Template

---

[//]: # (Image References)

[image1]: ./pipeline.png "Image Pipeline"

---

### Reflection

The pipeline that this implementation(P1.ipynb) follows is broadly built in 5 steps. The steps involve fine tuning the parameters for Gaussian Blur, Canny Edge Detection, Region Identification and Hough Transformations over the images. The parameters are chosen in such a way, that these can be approximately applicable to all the test images given by finding/drawing optimal Lane lines.

Once these preliminaries were performed, the resulting image was masked to a bounding isosceles trapezoid that contains the lanes. This ended up being proportional to the image size, as the position of the camera in the car relative to the lanes is reasonably invariant. Doing it this way availed using the same routine for the two test videos.

The issue here is to get a balance in terms of the minimum line length, where if it is too small there is road noise, if it is too large then the broken road segments are harder to detect. Similarly with the kernel size for the Gaussian blur, if it is too low then road noise contributes excessively, but if it is too large then features can be missed more easily.

In order to draw a single line on the left and right lanes, I've used averaging function. The `average_lines()` function is used in separating line segments by their slope ((y2-y1)/(x2-x1)) to decide which segments are part of the left line vs. the right line.  Then, the average position of each of the lines are found and extrapolated to the top and bottom of the lane.

![Pipeline][image1]


### Potential Shortcomings and Possible Improvements with the current pipeline


One potential shortcoming would be what would happen when the lanes disappear or lane getting erased(on the road), the vehicle might not be able to find out the path in which it has to move forward(atleast with this kindof setup). Also, The averaging function has to be tweaked/improved a little more to identify lanes in videos which are not taken in a single orientation, which i believe is the reason for the pipeline not being able to detect lanes in the challenge.mp4 video properly. 

Another shortcoming could be that the lanes might not be well detected when the light conditions vary because of the camera/climate. This has to be taken into consideration to improve the performance of this pipeline.


## Video Streaming!! 

`SolidWhiteRight.mp4`

<video controls src="../test_videos/SolidWhiteRight.mp4" />


After Applying the pipeling over the video, 

<video controls src="../test_videos_output/SolidWhiteRight.mp4" />




