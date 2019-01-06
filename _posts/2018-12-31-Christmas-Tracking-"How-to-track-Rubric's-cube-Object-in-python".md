![Alt Stack](https://i.imgur.com/nffQgQw.jpg "Computer Vision")
## Object tracking is one of the most important components in numerous applications of computer vision and machine learning.

A month ago I am thinking about what to write in December and I decided that the best thing to close this year is the last thing I learned. So this is Computer Vision. 

### Object Tracking is like you are spying or following an object or person or car to know the the location of the object and how this object is moving, its speed, where is it going and etc.

**But before we start to talk about the theory and the implementation. I want to tell that after you read this blog, We are going to make like this video.**  
<a href="https://www.youtube.com/watch?v=8Bk_I_H8GlQ" target="_blank"><img src="https://i.imgur.com/6LNfYaH.png" alt="computer vision and machine learning" width="580" height="350" border="20" /></a>

First, there is steps or stages to track an object:
1. **Background:** is the image or the frame that have all the background without the object that we want to track.
for example if we want to track the car or wastebasket in street, We have to take a picture for the street without car or Wastebasket.  
![Alt Stack](https://i.imgur.com/cBlGhJq.png "background without our object")

2. **Current frame:** is the image or the frame that have the background and our object  
![Alt Stack](https://i.imgur.com/GjCQiho.png "background with our object")


3. **Mathematical subtraction:** sub(Background, Frame)  
For example if we have 2 images like the prev and we do mathematical subtraction on both, The result will be the object. 
**Notice we subtracted pixels:** 
    * If the two pixels are same, the result is 0 which give us black pixel
    * If the two pixels aren't same, we can't say the result is 1 which is white and it can be another value. But it is not necessary to be white.

4. **Filter:** The mathematical subtraction from previous step applies here threshold filter to get the difference between the two images. 
For example we make a condition to make all pixels that less than 100 equals zero and all pixels greater than or equal to 100 equals to 255. Here's we can see our object  
![Alt Stack](https://i.imgur.com/7WvXxjZ.png "Our object after subtraction")
 
5. **Masking &&:** Between the result of our mathematical subtraction and the current frame which have the object. 
**Do you remember:** 
    * 0 && any value => 0 
    * 255 && any value!=0 => any value!=0 

    Here's we get only the object from the frame with its color.

6. **Blob detection:** A Blob is a group of connected pixels in the frame that share some common property .like the dark connected regions that around the object. The goal of blob detection is to identify and mark these regions.
Blob detection is scanning the image from filtering stage until there is change in color (Called edge) which is the white around the object. Then draw around the object to compute containing box or containing rectangle  (X1, X2, Y1, Y2) which means the height and width. Then we can get the center of container box  
![Alt Stack](https://i.imgur.com/okoqgC6.png "Our object after blob detection")


## **This is the concept around object detection and now lets detect the green color of our rubric's cube and track its moves in the frame**


First we import our necessary packages. We’ll be using deque , a list-like data structure that allows us to draw the tail or contrail of the rubric.

```python
import cv2
import imutils
import numpy as np
from collections import deque
from imutils.video import VideoStream
import argparse
import time
```

To access webcam, we use --buffer which is the maximum size of our deque to maintain a list of the previous (x, y)-coordinates of the object that we are tracking. So the default is the value of our buffer.
This deque  allows us to assembly points and track it so the deque draw the tail or contrail of the rubric.


```python
ap = argparse.ArgumentParser()
ap.add_argument("-b", "--buffer", type=int, default=50)
args = vars(ap.parse_args())

```

We have to define the lower and upper boundaries of the color green in the HSV color to detect the green boundaries in our frame. 
```python
greenLower = (29, 86, 6)
greenUpper = (64, 255, 255)
```

Then initialize the list of tracked points using the supplied maximum buffer size which defaults to 50
```python
pts = deque(maxlen=args["buffer"])

```

To warm up and access the camera stream
```python
vs = VideoStream(src=0).start()
time.sleep(2.0)
```

Then we resize the frame to have a width of 700px. Then blur the frame to reduce high frequency noise and allow us to focus on the rubric inside the frame such. Finally, we convert the frame  to the HSV color space.
```python
frame = imutils.resize(frame, width=700)
blurred = cv2.GaussianBlur(frame, (11, 11), 0)
hsv = cv2.cvtColor(blurred, cv2.COLOR_BGR2HSV)

```

Then we construct a mask for the color "green", then perform a series of dilations and erosions to remove any small blobs left in the mask so we can get and detect the actual localization of the green rubric in the frame

```python
mask = cv2.inRange(hsv, greenLower, greenUpper)
mask = cv2.erode(mask, None, iterations=2)
mask = cv2.dilate(mask, None, iterations=2)

```

Then we can find the center of the rubric by computing the contours of the object(s) in the mask.
Also we initialize the center of the rubric (x, y) coordinates to be None 

```python
cnts = cv2.findContours(mask.copy(), cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_SIMPLE)	
cnts = imutils.grab_contours(cnts)
center = None
```

Then we have to make a check to ensure at least one contour was found in the mask. So we find the largest contour in the cnts list, Compute the minimum enclosing circle of the blob and then compute the center (x, y) coordinates (the centroids)

```python
if len(cnts) > 0:
	c = max(cnts, key=cv2.contourArea)
	((x, y), radius) = cv2.minEnclosingCircle(c)
	M = cv2.moments(c)
	center = (int(M["m10"] / M["m00"]), int(M["m01"] / M["m00"]))

```

Then we make a another check to ensure that the radius of the minimum enclosing circle is sufficiently large. So we then draw Contours surrounding the rubric. Then update our new points.

```python
	if radius > 10:
	    cv2.drawContours(frame, [c], -1, (0, 255, 0), 2)

	pts.appendleft(center)

```

Finally, We have to to draw the tail or contrail of the rubric. 
We start looping over the set of tracked points. If either the current point or the previous point is None that means the rubric was not successfully detected in that given frame, then we ignore the current index and continue looping over the set of tracked points.
```python
    for i in range(1, len(pts)):
        if pts[i - 1] is None or pts[i] is None:
            continue
```


Else if both points are valid, that means the rubric was successfully detected in that given frame so we compute the thickness of the contrail and then draw it on the frame.
```python	
        thickness = int(np.sqrt(args["buffer"] / float(i + 1)) * 4.5)
        cv2.line(frame, pts[i - 1], pts[i], (0, 255, 250), thickness)

```

Finally, display and show the frame to our screen, detecting any key presses and break if you entered q

```python
    cv2.imshow("Rubik's cube tracking", frame)
    key = cv2.waitKey(1) & 0xFF

    if key == ord("q"):
        break
```

Last thing to code is to release the camera

```python
vs.release()
cv2.destroyAllWindows()
```


### Last thing to say, Happy new year and thank you for reading :))
[Here](https://github.com/mohamedkhaledyousef/Crash-courses/tree/master/Computer%20vision/Rubik's%20cube%20tracking) is the repo, You can find the source code in python.


