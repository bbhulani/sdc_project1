# **Finding Lane Lines on the Road** 
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
My pipeline consists of 5 stages:
* Greyscaling: converts image to a grey scale
* Gaussian blur: supresses noise and gradient spurs
* Canny edge detection: detects the edges of objects on the image
* Region of interest selection: Filters out edges that are outside of the driving lane
* Hough transform: Identifies line segments in an image within the region of interest 

The output of the hough transform gives 2 co-ordinates for each of the line segments detected within in an image

The draw_lines function then: 
* Filters out line segments with slopes that are outside the range of the lane line slope (done by experimentation)
* Computes the average x1,y1,x2,y2 coordinates of all the line segments
* Computes the average slope for right lane and left lanes of all line segments
* Computes the intecept b in the line equation y = mx + b
* The line to be drawn assumes fixed Y coordinates for startY and endY positions. 
* Using the calculated intercept b, startY and endY, the starting X coordinates are calculated
* The final line is created with the startX, startY, endX, endY coordinates

Finally the lane lines are drawn on the original image with the weighted image function

![solidWhiteCurve][./test_images_output/solidWhiteCurve.jpg]
![solidWhiteRight][./test_images_output/solidWhiteRight.jpg]
![solidYellowCurve][./test_images_output/solidYellowCurve.jpg]
![solidYellowCurve2][./test_images_output/solidYellowCurve2.jpg]
![solidYellowLeft][./test_images_output/solidYellowLeft.jpg]
![whiteCarLaneSwitch][./test_images_output/whiteCarLaneSwitch.jpg]

### 2. Identify potential shortcomings with your current pipeline


* when the lanes are curved like in the challenge video the algorithm doesnt work well since its assuming straight lines and not curved lines
* plotting lanes based on fixed starting and ending Y coordinates is not a dynamic solution. 


### 3. Suggest possible improvements to your pipeline

* Dynamically detectiong the vairance of the slope and use that to filter out the line segments in draw_lines
* Ideal the algorithm should identify the starting and ending Y coordinates of the drawn line
* draw_lines function should be able to draw curved lines and not just straight lines
* Drawn lines coult be a bit longer and be consistent for all frames of the video
