
# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]:./OutFiles/a.jpg "Grayscale"

[image2]:./OutFiles/b.png "Canny"

[image3]:./OutFiles/c.png "Lines"


---

### Reflection



## 1. Describe your pipeline.

The first step in my pipeline was to convert the images into grayscale.![alt text][image2] Next, I implemented a Gaussian blur function to reduce the image noise. This step was followed by the implementation of the Canny operator to identify the edges of the images.![alt text][image3] The final step was to use the canny images to identify a region of interest delimited by a polygon where lines will be drawn ![alt text][video] . 

### Lane Separations

In order to draw a single line on the left and right lanes, we must unabiguously identify left lanes from right lanes. This is achieved by implemented a function on segmented lines and recognizing that slopes from left lines segment will be negative and slope from right line segment will be positive. 
The code below is a snippet showing how the slopes were obtained.
    
    ymax = img.shape[0]
    ymin = 0
    for line in lines:
        for x1,y1,x2,y2 in line:
            slope = (y2 - y1)/(x2 - x1)
            intercept = y2 - slope*x2
            if slope < 0 and slope > -math.inf:
                neg_slopes.append(slope)
                neg_intercepts.append(intercept)
           
            if slope > 0 and slope < math.inf:
                pos_slopes.append(slope)
                pos_intercepts.append(intercept)
               
            ymin = min(y1, y2)    
            
    neg_slope = np.mean(neg_slopes)
    neg_intercept = np.mean(neg_intercepts)
    pos_slope = np.mean(pos_slopes) 
    pos_intercept = np.mean(pos_intercepts)
    
 ![alt text][image1]
 
 ### Video
 Three videos were also provided on which I run my pipeline:

* a video with solid white lane lines. Here is a [link to my video result](./test_videos_output/solidWhiteRight.mp4)
* a video with solid yellow lane line on the left and dotted white lane line on right. Here is a link to that video. [link to my video result](./test_videos_output/solidYellowLeft.mp4)
* a challenge video where the road is curved. Here is a [link to my video result](./test_videos_output/challenge.mp4)

### 2. Identify potential shortcomings with your current pipeline
One potential shortcoming is that the code does not workk well for curved lanes as observed in the challenge video. 


### 3. Suggest possible improvements to your pipeline
A possible improvement would be to do a linear fit and extrapolate the direction of the lanes using the fit parameters.




```python

```
