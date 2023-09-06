# Lane-Path_Detection
In the project the combined (gradian/sobel/hsl/hsv) methods to create a better understanding on the roads and their lanes


# Advanced Lane Finding Project

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.



### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.
This step is really easy
for find and draw corners

    1. cv2.findChessboardCorners
    2. cv2.calibrateCamera
for undistort

    1. cv2.undistort
The camera calibration for my code is in `Calibrate_Camera.ipynb`. [here](Calibrate Camera.ipynb "Calibrate Example")


### Pipeline (single images)


#### 1. Provide an example of a distortion-corrected image.
![alt text][image1]

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

In this step, I've called three different functions the first is `abs_sobel_thresh(img)`  , `mag_thresh(img)` and `dir_threshold(img)`. These three function are combine in

```python
combine_sobel_hls_threshold(img)
```
I could add CLAHE (Contrast Limited Adaptive Histogram Equalization), but not enought time ...


#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

Here too really easy in my function `warp(img)` I called :

1. cv2.getPerspectiveTransform => to get the Matrix
2. cv2.warpPerspective

But!! Before we use these functions we need to two things the Source and the Destination

```python
src = np.float32(
    [[(img_size[0] / 2) - 55, img_size[1] / 2 + 100],
    [((img_size[0] / 6) - 10), img_size[1]],
    [(img_size[0] * 5 / 6) + 60, img_size[1]],
    [(img_size[0] / 2 + 55), img_size[1] / 2 + 100]])
dst = np.float32(
    [[(img_size[0] / 4), 0],
    [(img_size[0] / 4), img_size[1]],
    [(img_size[0] * 3 / 4), img_size[1]],
    [(img_size[0] * 3 / 4), 0]])
```


| Source        | Destination   | 
|:-------------:|:-------------:| 
| 585, 460      | 320, 0        | 
| 203, 720      | 320, 720      |
| 1127, 720     | 960, 720      |
| 695, 460      | 960, 0        |




#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

`find_lane_pixels(binary_warped, nwindows=9, margin=100, minpix=20)`

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

`mesure_curve(left_fit_cr, right_fit_cr, ploty)`

quick example

```python
left_fitx = left_fit[0]*ploty**2 + left_fit[1]*ploty + left_fit[2]
right_fitx = right_fit[0]*ploty**2 + right_fit[1]*ploty + right_fit[2]
```


#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.



---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Video is in the output_videos

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?


1. In the project the combined (gradian/sobel/hsl/hsv) methods and it was difficult to undestand them. Now it ok :D
2. Find the good threshold is a challenge
3. My fitting are not quite good ! Help

### Vamsi K
