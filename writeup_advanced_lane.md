# Advanced Lane Finding Project

[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

[//]: # (Image References)
[camera_cal1]: ./writeup_images/camera_cal1.png
[camera_cal2]: ./writeup_images/camera_cal2.png
[camera_cal3]: ./writeup_images/camera_cal3.png
[camera_cal4]: ./writeup_images/camera_cal4.png
[camera_cal5]: ./writeup_images/camera_cal5.png
[undis1]: ./writeup_images/undis1.png
[undis2]: ./writeup_images/undis2.png
[undis3]: ./writeup_images/undis3.png
[undis4]: ./writeup_images/undis4.png
[undis5]: ./writeup_images/undis5.png
[undis6]: ./writeup_images/undis6.png
[undis7]: ./writeup_images/undis7.png
[undis8]: ./writeup_images/undis8.png
[bird1]: ./writeup_images/bird1.png
[bird2]: ./writeup_images/bird2.png
[bird3]: ./writeup_images/bird3.png
[bird4]: ./writeup_images/bird4.png
[bird5]: ./writeup_images/bird5.png
[bird6]: ./writeup_images/bird6.png
[bird7]: ./writeup_images/bird7.png
[bird8]: ./writeup_images/bird8.png
[color1]: ./writeup_images/color1.png
[color2]: ./writeup_images/color2.png
[color3]: ./writeup_images/color3.png
[color4]: ./writeup_images/color4.png
[color5]: ./writeup_images/color5.png
[color6]: ./writeup_images/color6.png
[color7]: ./writeup_images/color7.png
[color8]: ./writeup_images/color8.png
[comb1]: ./writeup_images/comb1.png
[comb2]: ./writeup_images/comb2.png
[comb3]: ./writeup_images/comb3.png
[comb4]: ./writeup_images/comb4.png
[comb5]: ./writeup_images/comb5.png
[comb6]: ./writeup_images/comb6.png
[comb7]: ./writeup_images/comb7.png
[comb8]: ./writeup_images/comb8.png
[curve1]: ./writeup_images/curve1.png
[curve2]: ./writeup_images/curve2.png
[curve3]: ./writeup_images/curve3.png
[curve4]: ./writeup_images/curve4.png
[curve5]: ./writeup_images/curve5.png
[curve6]: ./writeup_images/curve6.png
[curve7]: ./writeup_images/curve7.png
[curve8]: ./writeup_images/curve8.png
[grad1]: ./writeup_images/grad1.png
[grad2]: ./writeup_images/grad2.png
[grad3]: ./writeup_images/grad3.png
[grad4]: ./writeup_images/grad4.png
[grad5]: ./writeup_images/grad5.png
[grad6]: ./writeup_images/grad6.png
[grad7]: ./writeup_images/grad7.png
[grad8]: ./writeup_images/grad8.png
[histo1]: ./writeup_images/histo1.png
[histo2]: ./writeup_images/histo2.png
[histo3]: ./writeup_images/histo3.png
[histo4]: ./writeup_images/histo4.png
[histo5]: ./writeup_images/histo5.png
[histo6]: ./writeup_images/histo6.png
[histo7]: ./writeup_images/histo7.png
[histo8]: ./writeup_images/histo8.png
[lane1]: ./writeup_images/lane1.png
[lane2]: ./writeup_images/lane2.png
[lane3]: ./writeup_images/lane3.png
[lane4]: ./writeup_images/lane4.png
[lane5]: ./writeup_images/lane5.png
[lane6]: ./writeup_images/lane6.png
[lane7]: ./writeup_images/lane7.png
[lane8]: ./writeup_images/lane8.png
[pipe1]: ./writeup_images/pipe1.png
[pipe2]: ./writeup_images/pipe2.png
[pipe3]: ./writeup_images/pipe3.png
[pipe4]: ./writeup_images/pipe4.png


Overview
---
This write-up was written as a partial fulfillment of the requirements for the Nano degree of "Self-driving car engineer" at the Udacity. The goals of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

The project instructions and starter code can be found in [here](https://github.com/udacity/CarND-Behavioral-Cloning-P3).
The project environment can be created with [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md).

Rubric Points
---
This write-up explains the points in rubric by providing the description in each step and links to other supporting documents and the images to demonstrate how the code works with examples.

### Writeup/Readme
#### 1. Provide a writeup/README that includes all the rubric points and how you addressed each one.
The files are submitted in the directory containing this write-up.
The files are
* `advanced-lane-finding.ipynb` : a jupyter notebook which contains all the required codes.
* `advanced-lane-finding.html` : a html file exported by the jupyter notebook containing all the execution results.
* `./writeup_images/*` : all the images and video showing the result
* `writeup_advanced_lane.md` : this write-up file

### Camera Calibration
#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `object_points` is just a replicated array of coordinates, and `objpoint` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `corners` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.

I then used the output `object_points` and `image_points` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result:

![alt text][camera_cal1]
![alt text][camera_cal2]
![alt text][camera_cal3]
![alt text][camera_cal4]
![alt text][camera_cal5]


### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

I apply `cv2.undistort()` with camera calibration parameters obtained in the previous section to all the test images which are shown in the following.

![alt text][undis1]
![alt text][undis2]
![alt text][undis3]
![alt text][undis4]
![alt text][undis5]
![alt text][undis6]
![alt text][undis7]
![alt text][undis8]


#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

I used a combination of color and gradient thresholds to generate a binary image (thresholding steps at 3rd cell through 5th cell in `advanced-lane-finding.ipynb`).  Here are my output results for this step.

![alt text][comb1]
![alt text][comb2]
![alt text][comb3]
![alt text][comb4]
![alt text][comb5]
![alt text][comb6]
![alt text][comb7]
![alt text][comb8]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

The code for my perspective transform includes a class called `birdsview`, which appears in 6th cell in the file `advanced-lane-finding.ipynb` The `transform()` function in `birdsview` class takes as inputs an image (`image`) and inverse on/off flag. The source(`before`) and destination (`after`) points are required at the class construction call.  I chose the hardcode the source and destination points in the following manner: (`offset` variable is used to trim destination points.)

```
before = np.array([[253, 697],[585,456],[700, 456],[1061,690]], np.int32)
off = 60
offset = np.array([[off, 0],[off, 0],[-off, 0],[-off, 0]], np.int32)
after = np.array([[253, 697], [253, 0], [1061, 0], [1061, 690]] + offset , np.int32)
```

This resulted in the following source and destination points:

| Source        | Destination   |
|:-------------:|:-------------:|
| 253, 697      | 313, 697      |
| 585, 456      | 313, 0        |
| 700, 456      | 1001, 0       |
| 1061, 690     | 1001, 690     |

I verified that my perspective transform was working as expected by drawing the `before` and `after` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.

![alt text][bird1]
![alt text][bird2]
![alt text][bird3]
![alt text][bird4]
![alt text][bird5]
![alt text][bird6]
![alt text][bird7]
![alt text][bird8]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

First of all, to detect the lane start points, I take the frequency of one in each column which is well described in histogram depicted in the following. The peaks in the histogram indicates the lane starting points.

![alt text][histo1]
![alt text][histo2]
![alt text][histo3]
![alt text][histo4]
![alt text][histo5]
![alt text][histo6]
![alt text][histo7]
![alt text][histo8]

Then I fitted my lane lines with a 2nd order polynomial. This is a fairly exquisite technique which is not amply explained in the web material. I should have understood the code by myself. I took the codes from the material and wrapped them in a function. The identified lane-line pixels and 2nd order polynomial fitting results are shown in the below.

![alt text][curve1]
![alt text][curve2]
![alt text][curve3]
![alt text][curve4]
![alt text][curve5]
![alt text][curve6]
![alt text][curve7]
![alt text][curve8]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

I did this in 9th cell in `advanced-lane-line.ipynb`. The curvature-measuring formula is explained in [Interactive Mathematics](https://www.intmath.com/applications-differentiation/8-radius-curvature.php) and this is
$$([1+((dy)/(dx))^2]^(3//2))/(|(d^2y)/(dx^2)|)$$
at any point <em>x</em> for the curve <span class="intmath"><i>y</i> = <i>f</i>(<i>x</i>)</span>
The measured left and right line curvatures are shown in the following figures as well as the offset in meters from the center point.

![alt text][lane1]
![alt text][lane2]
![alt text][lane3]
![alt text][lane4]
![alt text][lane5]
![alt text][lane6]
![alt text][lane7]
![alt text][lane8]

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

I implemented this step in 11th cell in `advanced-lane-finding.ipynb` in the clss `Line`.  Here are my results on all the test images:

![alt text][pipe1]
![alt text][pipe2]
![alt text][pipe3]
![alt text][pipe4]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./writeup_images/project_video_result.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

All the necessary techniques are well described in the web materials. So any problems / issues were not seriously encountered during the project.
Following the suggestion in the rubric, I accumulated and averaged many times (12 times in a code) the lane line detection result to signal the robust detection and used that to inform the *a priori* search for the position of the lines in subsequent frames of video. Since then, accumulated lane line coefficients were averaged to get the current values to draw the current lines. Three functions `update_fit()`, `get_best_fit()`, and `get_bestx()` in the class `Line` implements it.
```python
    def update_fit(self, left_fitx, right_fitx, left_fit, right_fit):
        self.bestx_left_buffer.append(left_fitx)
        self.bestx_right_buffer.append(right_fitx)
        self.best_fit_left_buffer.append(left_fit)
        self.best_fit_right_buffer.append(right_fit)
        if len(self.bestx_left_buffer) >= 12:
            del self.bestx_left_buffer[0]
            del self.bestx_right_buffer[0]
            del self.best_fit_left_buffer[0]
            del self.best_fit_right_buffer[0]
            self.detected == True

    def get_best_fit(self):
        ave_left = np.average(self.best_fit_left_buffer, axis=0)
        ave_right = np.average(self.best_fit_right_buffer, axis=0)
        return ave_left, ave_right
    
    def get_bestx(self):
        ave_left = np.average(self.bestx_left_buffer, axis=0)
        ave_right = np.average(self.bestx_right_buffer, axis=0)
        return ave_left, ave_right
```

This has two impacts on the overall performance.
 1. This improves speed and provides a more robust method for rejecting outliers.
 2. This smoothes the lane detection over frames to avoid jitter.

Nonetheless, it was not possible to pass the challenge and harder video test.

