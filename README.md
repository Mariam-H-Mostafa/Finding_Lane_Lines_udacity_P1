# Finding Lane Lines on the Road

The goal of this project is to detect lane lines the car is moving in, the approach is done on two steps:

 1. Create a pipeline to detect lines in series of images.
 2. Extrapolate the lines detected to draw just one line representing the right lane and left lane.
 3. Apply the pipeline created to detect lines in a video stream.

Pipeline Explanation:

First, read the image and extract some useful information like no. of rows and no. of columns using imshape function. Convert the image into gray scale, then smoothing the image using GaussianBlur, then detect the edges using canny function, detect pixels above the high_threshold, and reject pixels below the low_threshold.
Then, determine our region of interest, that we are concerned with the lines inside it. At that point we can run hough transform to find lines from canny edges.

**Image**:

![Image](https://i.ibb.co/B31KvS3/Picture2.png)

After applying grayscale transform:

(https://i.ibb.co/DWWRq3r/Picture3.png)

After applying gaussian:
(https://i.ibb.co/ynCkCfw/Picture4.png)

After applying canny:
(https://i.ibb.co/cb5PBSr/Picture5.png)


After applying detecting region of interest:
(https://i.ibb.co/1XVPQmY/Picture6.png)

After Hough lines transform:
(https://i.ibb.co/pyn9H5x/Picture7.png)

After merging it with original image:
(https://i.ibb.co/k0JwZD2/Picture8.png)
**Adjusting the `draw_lines` function to extrapolate** :

Create the slope of each line, if it is positive so these points related to the line in the right area, if negative so they related to points in the left region.

According to simple 1st degree polynomial, y=mx+b, so I will calculate the intercept of each line. Create a list for each group rm,lm,bR,bL

Use the average of them to create new lines, bases on the above mentioned equation.

Now, we can apply the pipeline created to the video provided

**Reflection**:

Roads with curved lanes or uphill and downhill, couldn’t detected easily using the 1st degree polynomial.

Also in extrapolation part, I think there could be another accurate way than separating based on right and left slopes, especially if the roads are full of curves.

We can use like history to detect next point.
