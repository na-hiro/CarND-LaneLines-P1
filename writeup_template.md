# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image0]: ./report/ori.jpg "Original"
[image1]: ./report/gray.jpg "Grayscale"
[image2]: ./report/blur.jpg "Blur"
[image3]: ./report/edge.jpg "Edge"
[image4]: ./report/mask.jpg "Mask"
[image5]: ./report/hough.jpg "Hough"
[image6]: ./report/lines.jpg "Lines"

---

### Reflection


### 1. Pipeline Description

My pipeline consisted of 6 steps.

The original image is shown below.:

![alt text][image0]

1. The original image is converted to a grayscale image.

![alt text][image1]

2. Noise is removed by applying a smoothing filter to the grayscale image.  The applied filter is the Gaussian Blur, with kernel size = 5.

![alt text][image2]

3. Edges are detected from noise-removed images by applying canny's edge detection algorithm.

![alt text][image3]

4. By specifying the area where the lane is located, only the edge of the lane is extracted from the edge detection image.

![alt text][image4]

5. Applied Hough Transform to find line segments.

![alt text][image5]

6. Lines are drawn as continuous straight lines

Modified the draw_lines() function in order to draw a single line on the left and right lanes. 
The correction items are described below.
 First, both lines of the lane are classified as a left line and a right line. In addition, based on the lane angle range, a valid line will be selected. The maximum and minimum Y coordinate values are calculated from the selected lane. The X coordinate is calculated from the calculated Y coordinate and the average of the slope. The coordinates of both ends of the calculated left and right line are the coordinates of both ends of the lane. Display the lane by drawing the coordinates of both ends as lines.

![alt text][image6]

### 2. Identify potential shortcomings with your current pipeline

The problems are described below.
For solidWhiteRight.mp4 and solidYellowLeft.mp4, the lane trace was stably confirmed. For challenge.mp4, it was confirmed that there were several problems. The problems are as follows. It was confirmed that the detection became unstable in the curve and shadow areas. 



### 3. Suggest possible improvements to your pipeline

The improvement plans are shown below.
It is presumed that this is due to the fact that the lane is approximated by a linear equation and the parameters related to lane detection are fixed values. Therefore, as an improvement plan, there are mainly two points. 
The first point is to approximate the detection result by a nonlinear line such as a quadratic equation.
The second point is adaptively changing parameters such as threshold according to the lane situation. In order to adaptively update the parameters, more detailed image analysis is required.
