# **Finding Lane Lines on the Road** 

## Writeup 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report
<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />


[//]: # (Image References)

[image1]: ./test_images_output/solidYellowLeft.jpg "Solid Yellow Left"

---

### Reflection

### 1. Description of the pipeline

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied Gaussian Blur to it. The Canny-Filter searches for Gradients in the grayscale and marks them. The mask function selects the area in front of the car. Then, the Hough function searches straight lines in the area. Those lines get sorted into right and left lanes by the modified draw_lines() function. The search criteria is the angle of the line, whether it matches the expected interval. The lists for right and left contain the arguments of a straight line m and b. The mean of these are used in order to calculate the straight beams. 
<img src="/test_images_output/gray_blur.png" width="480" alt="gray_blur" />
<img src="/test_images_output/edges.png" width="480" alt="edges" />
<img src="/test_images_output/masked.png" width="480" alt="masked" />


### 2. Potential shortcomings


* The main issue is to build a contrast-filter that works consistently. Other cars in the masked area as well as bad contrast confuse the filter. Rain, snow, other cars, tight corners, or a bad contrast between the pavement and the marking need further sophistication. 
* The lanes are assumed to be straight, as seen in the challenge, sharp corners need an improved algorithm. 
* The perspective dynamically changes the lengths of both the lines and the gaps, so the detection parameters are always a compromise between the individual marker in front of the car and the "shorter" line in the distance. 


### 3. Possible improvements

* Usually, road markings are pretty continous, so a moving average over one second or even better a Kalman Filter would be very interesting to stabilize the markings. 
* Since this particular algorithm is purpose-build for the examples with light traffic in sunshine, further tuning of the parameters is necessary. 
* In the longer run either changing the color from gray to a range where the pavement/marking color range is enhanced may be more beneficial. 
* Another potential improvement could be to detect the other lanes. Programming an algorithm, which detects the contrast between road and grass on the side, would enable masking for the complete road. Then, an advanced feature detection may be able to see the other lanes, and once the other cars are detected, they could be excluded from the lane algorithm. 


