# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[image1]: ./test_images/solidWhiteCurve.jpg "Grayscale"

[image2]: ./test_images_output/solidWhiteCurve.jpg "Grayscale"

[image3]: ./test_images_output/lineSolidWhiteCurve.jpg "Grayscale"

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
  3. apply Canny Edge Detection with low_threshold = 50, high_threshold = 150
  4. define the mask poygon for choosing Region of Interest
  5. Run Hough Transform on edge detected image and add the lines to the image via draw_lines()

In order to draw a single line on the left and right lanes, I modify the draw_lines() function by looping through
  the individual line segemnts and:
  1. determine the slope of each line segment (which determines if the segment belongs on the left or right) and
  2. save the cooordinates for the segments with the lowest and highest x-values
Once all segemnts have been processed, I draw the lines by calling cv2.line to join the low and high coordinates

Several examples follow.

input image example: 

![alt text][image1]

output image example (lane segments): 

![alt text][image2]

output image example (lane lines): 

![alt text][image3]


### 2. Potential shortcomings with your current setup

The challenge video output suggests several problems:
  - shadows create an issue
  - sharp curves can create issues
  - lane obstructions can create issues
  - lines detected as part of objects such as bridges create issues
  - random noise creates non-sensical lane lines

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to parameterize some of the functionality:
  - when trying to determine polygon vertices
  - sharp curves can create issues
  - lane obstructions can create issues
  - lines detected as part of objects such as bridges create issues
  - random noise creates non-sensical lane lines

A possible improvement would be to parameterize some of the functionality:
  -when trying to determine polygon vertices
Also see if the horizon can be determined for figuring Region of Interest
