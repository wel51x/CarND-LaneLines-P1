# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

I created three pipelines, with much common functionality
  1. finding_lanes_segments_pipeline creates iamge files containing line segments for each image in test_images
  2. draw_lane_lines improves on the above by drawing singe lines on the left and right side of the lanes
  3. process_challenge_lane_image changed the vertices for the mask polygon since the video dimensions are larger.
 
Each pipeline has five steps as follows:
  1. convert the images to grayscale
  2. apply Gaussian smoothing
  3. apply Canny with low_threshold = 50, high_threshold = 150
  4. define the mask poygon
  5. Run Hough on edge detected image and add the lines to the image

In order to draw a single line on the left and right lanes, I modify the draw_lines() function by looping through
  the individual line segemnts and:
  1. determine the slope of each line segment (which determines if the segment belongs on the left or right) and
  2. save the cooordinates for the segments with the lowest and highest x-values
Once all segemnts have been processed, I draw the lines by calling cv2.line to join the low and high coordinates

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
