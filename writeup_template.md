#**Finding Lane Lines on the Road** 

##Overview

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on my work in a written report


[//]: # (Image References)

[image1]: ./test_images/image1.png "1"
[image2]: ./test_images/image2.png "2"
[image3]: ./test_images/image3.png "3"
[image4]: ./test_images/image4.png "4"
[image5]: ./test_images/image5.png "5"
---

### Reflection

##1. Pipeline Description. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps. 

1. Convert the images to grayscale
![alt text][image1]

2. Apply Gaussian Blur with kernel size 5. This filter effectively remove image noise that can cause false edge detection.
![alt text][image2]

3. Detect edges with Candy transform. It finds the intensity gradient of the image by applying a pair of convolution masks in x and y directions, and finding the gradient strength and direction. Then a non-maximum suppression is used to remove pixels that are not considered to be part of an edge. Finally, using two thresholds: lower to remove points, upper to accept points, and also accept all points in the range if they are connected to points above upper threshold (A low to high ratio of 1:2 or 1:3 is recommended).
![alt text][image3]

4. Use a tight trapezium region of interest to limit the detection. This greatly avoids false detection and allows stronger, more flexible tuning in Hough transform.
![alt text][image4]

5. Use Hough transform to detect line. Basically it transforms the lines in original image to points in polar coordinate, and counts the numbers of sin/cosin curves going through each point. rho can be 1/2, while threshold, min_line_length and max_line_gap affects the performance in removing short, unconnected lines.
![alt text][image5]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function. The slopes of lines detected by Hough transform are looped through, checking if they are negative or positive to know if they should belong to left or right lanes. Furthermore, I apply a filter in slope range (20, 70) deg to remove unnecessary horizontal detected lines which are noise. This greatly makes my line detection robust.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

##2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


##3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
