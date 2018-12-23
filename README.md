# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### Reflection


### 1. Pipeline description

I tried to keep the script as flexible as possible, so it could be easily reused for future projects with different image sizes and content. Therefore, all relevant parameters are defined outside of the pipeline function.

My pipeline consisted of the following major steps:

1. Convert the image to grascale, reduce noise and detect edges with Canny
1. Focus on the most likely area for lane markers and identify lines with Hough transform
1. Optional: Plot all lines in a gray scale image (see first image below)
1. Separate left and right lines using a K-means algorithm, a likely slope range as well as separation by the center of the focus area
1. Optional: Plot all relevant left and right lines in the original image (see second image below)
1. Use linear regression on all points of the left and right lines to determine the left and right lane markers
1. Optional: Plot lane markers in the original image (see thrid image below). This is also the output of the pipeline.

![First image](https://github.com/CyberAMS/CarND-LaneLines-P1/blob/master/output_16_1.png "First image")
![Second image](https://github.com/CyberAMS/CarND-LaneLines-P1/blob/master/output_16_3.png "Second image")
![Third image](https://github.com/CyberAMS/CarND-LaneLines-P1/blob/master/output_16_4.png "Third image")


### 2. Potential shortcomings with this pipeline

The pipeline works well for images in which the road has clear lane markers and the road surface itself has a homogeneous color. In the case of varying road surfaces and influences from other objects like driving from sunny conditions into shade, the pipeline picks up edges and lines that are also in the driving direction, but no lane markers.

Another shotcoming of this pipeline is that it requires that you drive pretty much in the middle of a lane. In case you leave the lane, the algorithm wouldn't detect the correct lane markers and there is no way for the vehicle to know how to get back into the necessary position in the lane.


### 3. Possible improvements to this pipeline

My current pipeline does not consider past images as I tried to keep the video processing function unchanged. Leveraging the fact that the vehicle cannot change its position relative to the lane too quickly, one could assume that the lane markers of the next video frame image should be very similar to the previous one. This would allow to overcome short periods of what the current pipeline experiences as unclear lane markers.

This pipeline could be used with several mask areas in which you look for lane markers. Besides the position in the middle lane, these mask areas would consider being out to the left or right and look for lane markers considering this perspective. This would allow to find lane markers when being outside of the center position in a lane, e.g. during lane change maneuvers. A logic would be required to determine the most likely perspective to pick the correct interpretation of lane markers.
