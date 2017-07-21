# **Finding Lane Lines on the Road**

## Writeup Template

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline converts an RGB image into the HSL color space, masks anything that is not bright white or yellow, then converts the image to greyscale, adds a gaussian blur, and then uses Canny edge detection.  The image is cleared except a region of interest the lanes are known to be in.  I cluster line segments from the probabilisitic Hough algorithm into right and left and take their weighted average, where the line length is the weight. The result is averaged with the last 50 lanes to smooth tracking and that is overlaid on the frame.


### 2. Identify potential shortcomings with your current pipeline

My pipeline is sensitive to light changes. Filtering by color is very difficult and would easily fail under different lighting conditions.

Abrupt changes cause jittery lines or missing lines, which are filled in by a running average.  This is an approximation and could be inaccurate in rapidly changing situations


### 3. Suggest possible improvements to your pipeline

Better lane lines could be found by considering the distance between the lanes and the theoretical intersection of the lines when deciding which features are actually lanes and which are noise.  

The color thresholds could be based on values derived from the roadway instead of constants to deal with changing lighting conditions.

The masking area could be improved by dynamically updating with the horizon, intersection of the lanes, and curvature of the lanes so that it is not accidentally masked by a static map.

In short, it would be better to replace the constants I used with dynamic values
