# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[trapezoid]: ./trapezoid.png "Grayscale"
[slope]: ./slope.png "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I use gaussian blur to eliminate noise. After gaussian operation, I use Canny to detect edge and use hough transform to find lines from trapezoid in image.
![alt text][trapezoid]

In order to draw a single line on the left and right landes, I separate lines by slope to left side and right side. To avoid wrong direction line segment, I set a minimum threshold for slope. Because we already know lane line must extend to the center of image, the slope of lane line must be greater than from corner to the center. After separate and filter line segments, we use numpy.polyfit to find a line through all segments in left and right group. The left line and right line are drawing by these 2 group's weight and bias.
![alt text][slope]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there is too many noise in lane. In optional challenge, this method could not handle well because shadow on the lane and reflection inside the car.
Another shortcoming could be curve. The current lane line is drawing by "line" function, but the curve could not satisfy "line".


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to kalman filter to correct new line with previous. This method avoid the noise in some frame. We can get great direction in most frames.
Another one is using curve function to draw lane line.
