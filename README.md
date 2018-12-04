# **Finding Lane Lines on the Road** 

## Writeup


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. 

1. Mask the image to the region of interest using a polygon.
2. Remove everythin besides the white and yellow regions in the image
3. Then I convert the image to grayscale
4. Apply gaussian blur to remove image noise
5. Apply the canny filter to the image (low: 50, high: 150 - 1:3)
6. Detect lines using hough transformation (1 Pixel, 1 Radiant, 25 Thresh, 50 min line length and 150 max line gap)


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by computing the slope m for every detected line. If the slope m is positive, it has to be the right lane, otherwise the left (in the code, left and right is named inverted - I forgot that y-axis is pointing down in image space :) ). Afterwards, I check every line if m is in a plausible magnitude for a lane line (between 0.5 and 1). Than I take the average of m for the final left an right slope. I also compute b for both lanes. Having the complete line equations, I compute the intersection with the horizontal top and button side of the roi polygon and mark the points as end and beginning of the final lane lines.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be a false detection if the lane marking disappears or a wrong image region is detected as lane marking. At them moment, this would dramatically affect the final lane marking.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to track the right and left lane over time. Another potential improvement could be to add a low-pass filter to make the approach more robust against outlier.
