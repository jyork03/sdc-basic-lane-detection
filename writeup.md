# **Finding Lane Lines on the Road** 


**Below describes details of a program that finds lane lines on the road**


[//]: # (Image References)

[gray]: ./test_images_output/gray_0.jpg "Grayscale"
[blur_gray]: ./test_images_output/blur_gray_0.jpg "Gaussian Blur Grayscale"
[edges]: ./test_images_output/canny_edges_0.jpg "Canny Edge Detection"
[masked_edges]: ./test_images_output/masked_edges_0.jpg "Masked Canny Edges"
[hough_lines]: ./test_images_output/hough_lines_0.jpg "Averaged & Extrapolated Hough Lines"
[final]: ./test_images_output/final_0.jpg "Overlayed On Original"

---

## Reflection

### 1. How It Works

My pipeline consisted of 6 steps:

1. Convert the image to grascale

 ![alt text][gray]

2. Apply a Gaussian blur to reduce noise in the image data

 ![alt text][blur_gray]

3. Apply Canny Edge Detection to identify the boundaries of objects in the image.  This works by finding steep color gradients.

 ![alt text][edges]

4. Mask out a trapezoidal shape as our region of interest

 ![alt text][masked_edges]

5. Apply a Hough Transformation to find lane lines, then average and extrapolate them into one left and right lane line
 using `draw_lines()`.
 
  ![alt text][hough_lines]
 
 * The `cv2.HoughLinesP()` method returns an array of lines, described in terms of `[x1, y1, x2, y2]`.
 * We start by iterating through each line to calculate the slope `(y2-y1)/(x2-x1)`.
 * If the slope falls between  -0.5 and 0.5, we immediately throw it out, since it's probably not the lane line we're detecting.
 * If the slope is positive and both points are on the right half of the image, we save the slope and the points in numpy arrays for the "right lane".
 * If the slope is negative and both points are on the left half of the image, we save the slope and points in numpy arrays for the "left lane."
 * After iteration we average out the `left_slopes` and `right_slopes` arrays and then the `left_x`, `left_y`, `right_x`, `right_y` arrays to find our intercept points.
 * Now we're ready to solve the line for x using the slope, intercept point, and a chosen y-coordinate value for the starting and ending  point of the left and right lines.
     * The point-slope equation `(int(((slope * -ix) + iy - y)/-slope), int(y))` returns
 a tuple that represents the desired point.
  * Then we draw our lines, using the four starting and ending left and right points

6. Overlay the averaged and extrapolated Hough lines onto the original image

 ![alt text][final]




### 2. Current Shortcomings


One potential shortcoming would be what would happen when the pipeline fails to detect a line.  In the current implementation,
I've opted to not display the line in such a scenario, which causes a flickering effect.

Another shortcoming could be night-driving conditions, since it is completely untested.

Other shortcoming could be poor lane markings that do not have high enough gradients to pass detection, debris
on the road, or cars merging in front of us that could throw off our detection pipeline.


### 3. Possible Improvements

A possible improvement would be to store previously detected line start/end points, and if the program fails to
detect a line, fall back to the most recent, previously found line positions in hopes that it will successfully find more soon.  I left an implementation of this strategy commented out in the `draw_lines()` method.

Other potential improvement could be to throw out more outliers, or spend more time fine-tuning the parameters to produce less noise in a sustainable way.
