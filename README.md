# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
Make a pipeline that finds lane lines on the road by using a series of image transformations and processing.


[//]: # (Image References)

[image0]: ./writeup_images/0.jpg "Input"
[image1]: ./writeup_images/1.jpg "Grayscale"
[image2]: ./writeup_images/2.jpg "Blur"
[image3]: ./writeup_images/3.jpg "Edges"
[image4]: ./writeup_images/4.jpg "Masked"
[image5]: ./writeup_images/5.jpg "Weighted"
[image6]: ./writeup_images/6.jpg "Result"
[image7]: ./writeup_images/hough.jpg "Hough"

---

### Reflection
### 1. Pipeline
The pipeline takes an input image or video (which are series of images). Then apply a series of image transformations such as grayscale, gaussian blur, Canny transformation, and Hough transformation in order to detect lines. 

The following sequence of images show the lane detection pipeline. Below is an example image with white lanes to the right.
![alt text][image0]

The input image is converted to grayscale.
![alt text][image1]

We then apply Gaussian smoothing to suppress noise and spurious gradients.
![alt text][image2]

Using Canny transformation, we now detect edges in the image.
![alt text][image3]

We are only interested in the edges that correspond to the lane we are currently in, so we restrict the edge detection within a polygon in the center of the image
![alt text][image4]

Then we apply hough transformation to find all edges within the polygon detected by the image above
![alt text][image7]

Lastly, we find the slope of left and right lanes by finding the median of edges on the left and the right side of the image. 
![alt text][image5]

Final Image
![alt text][image6]

### 2. Potential Shortcomings

1. Masked polygon's positions depend on image's frame, so the image depends on the camera's position. If the camera was mounted on the bottom of the vehicle, coordinates of masked polygons would have to be adjusted manually

2. Test images and video are very clean. Night time and weather performance is uncertain with the current algorithm

3. It is not clear how this algorithm would perform if the vehicle in front is blocking the line of sight. Only visible lanes would be the very near lanes, so the vehicle must react quickly.

4. The image and the video output are preprocessed. Based on the equipment on the vehicle, or the model complexity, the lane detection may not perform well in real time.

### 3. Possible Improvements

A possible improvement would be to reduce jitteriness. As of this writing on 6 June, The video output is very jittery. Averaging over a few frames would help reduce jittering. Also, improving the masked polygon boundary to only use detect the lanes would reduce the jitteriness.

Another potential improvement could be to not use a linear equation (i.e., y=mx+b) to interpolate the line. Using a polynomial function for interpolation may improve the accuracy of lane detection when encountering curves. That perhaps requires more complex algorithm for edge detection in image.
