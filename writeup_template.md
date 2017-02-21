#**Finding Lane Lines on the Road** 


---

The goals / steps of this project is to make a pipeline that finds lane lines on the road.


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Pipeline

Initially, the program tests on few test images. It gets list of all images present in the **test_images** folder and pass each image to `find_lanes()` function. The output image consists marked lanes and are stored in **test_images_result** folder.

My pipeline for finding lanes in video consisted of 8 steps:
1. The images of video is sent into `process_image()` function
2. Converts image into grayscale.
3. Apply Gaussian blur to reduce noice.
4. Apply Canny edge detection algorithm to convert it to a gradient image.
5. Mask the region of interest area and store it as a separate image.
6. Apply Hough transform to get all lines detected.
7. Filter all lines according to slope and remove unwanted lines.
8. Now draw lines on the original image and return the image to render video.

In order to filter the lines I have created a new method `process_lines()`. Based on slope values, it filters into left and right lines, and discards the horizontal lines.It then finds the average value of both left and right points and store it in an array. Then it is passed into `draw_lines()` function.

In order to draw a single line on the left and right lanes, I modified the `draw_lines()` function by calculating slope value of that averaged points and then calculated top and bottom points based on Y axis. 

>The output videos are saved into notebook as white.mp4,yellow.mp4 and extra.mp4
>The output test images are stored in the test_images_result folder in notebook.


###2. Potential shortcomings


One potential shortcoming would be what would happen when there is a curve on road. It cannot mark the curved lanes. It can only show straight line with changing slopes in each picture.

Another shortcoming could be when the road color is different. Some times road color could be in cement color with lot of rough lines on it. This pipeline cannot dynamically generate the region of interest or change parameters values for Thresholds.

Also, another shortcoming when there is no lane on the road. It faces same problem.

###3. Possible improvements

A possible improvement would be to to identify region of interest dynamically, select gaussian value and threshold value dynamically based on disturbance generated in Hough lines.

Another potential improvement could be to identify curved lanes and angle of curve.