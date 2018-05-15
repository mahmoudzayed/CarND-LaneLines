# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 8 steps:

1) I filtered the image color to just see yello and white.
2) I converted the images to grayscale.
3) I ran Gaussian smoothing on the image with size 5x5 matrix. this step can be skiped beacuse its included in the next step.
4) I used canny to get the edges in the image.
5) I masked an area of interest in the image to focus on the road.
6) I used hough transform to just pick a certain edges(lines) with specific properties to be carried forward into the analysis
7) I draw the lines into the an empty image. lines became two lines with the modification mentioned below.
8) I used a weight function to merge the line image into the orginal image to highlight the Road lanes.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
I add 3 steps before drawing the lines:

1) I filtered any line with extreme slop so to avoid noises and unrealistic lines.
2) I divided the lines into left and right groups.
3) I calculated the best fit line to the points for the left group lines and right group lines. I used linear regression to calculate the 
    best fit.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

There are several shortcoming that would results in failure of dediction of the lines or insufficient results.

1) You need to tune lots of parameters to reach the best performance.
2) parameter are static which can't adapt to changes in the enviroment.
3) I can't identify curved Lane lines
4) I can't see other lanes existing in the same road which cause limited decision which can be take upon this given data.
5) If there are a car infont of me, i will not predict the lane lines perfectly


### 3. Suggest possible improvements to your pipeline

There are several imporvemnt that can be add:

1) we can avoid using masked areas amd make our algorithm more general to analysis the whole image and analysis all the shapes in it and determine lane lines.
2) we can find best fit of the lines using a spline or a curve instead of straight line.