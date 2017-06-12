# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image_step_0]: ./image_for_writeup/0.png "Original"
[image_step_1]: ./image_for_writeup/1.png "Grayscale"
[image_step_2]: ./image_for_writeup/2.png "Blur"
[image_step_3]: ./image_for_writeup/3.png "Edge"
[image_step_4]: ./image_for_writeup/4.png "Masked"
[image_step_5]: ./image_for_writeup/5.png "Line detection"
[image_step_6]: ./image_for_writeup/6.png "Final"
 	
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

I describe my pipeline in steps:

This is the original image:

![alt text][image_step_0]

- Step 1: To gray scale

![alt text][image_step_1]

- Step 2: Gaussian blur

![alt text][image_step_2]

- Step 3: Edge detection

![alt text][image_step_3]

- Step 4: Image region mask

![alt text][image_step_4]

- Step 5: Line detection

![alt text][image_step_5]

- Step 6: Combine line with original image

![alt text][image_step_6]


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:

1. Split the line points into left points and right points by looking at the points' x coordinate value
2. Do linear regression on each point group to get the slope and intercept
3. Draw the line using the slope and intercept

### 2. Identify potential shortcomings with your current pipeline

Short comings:

1. I separate the line points by looking at the points' x value, but the threshold is hardcoded. If we change the mount position of the camera, the threshold needs to be adjusted.
2. The region of interest is also hardcoded. It will break easily if we change the camera mount position, or just drive into a road with different visual characteristics (e.g., much wider or narrower road)
3. I use a standard linear regression algorithm which is easily affected by outliers. The regression is not stable against outliers caused by visual noises.


### 3. Suggest possible improvements to your pipeline

Possible improvements:
1. Auto adjust the region of interest to clearly separate the road and other visual parts.
2. Use more robust regression (rlm(), or other iteration-based algorithm) to reduce the impact of visual noises so the line slope and intercept could be more stable.