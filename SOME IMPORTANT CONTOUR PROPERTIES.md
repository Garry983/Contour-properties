# **SOME IMPORTANT CONTOUR PROPERTIES**

In this article, we'll see some of the important properties of Contour.

Here, we will cover some advanced Contour Properties like aspect ratio, extent, convex hull, and solidity.

**1. Aspect Ratio**

The definition of Aspect Ratio is given as 

aspect ratio = image width / image height ,i.e. it's simply the ratio of the image width to the image height.

Following is the code snippet for finding the aspect ratio in Python

`x,y,w,h = cv.boundingRect(cnt)`
`aspect_ratio = float(w)/h`



Various examples of the different values of aspect ratios are shown in the figure below:

![image-20210704133107591](C:\Users\garim\AppData\Roaming\Typora\typora-user-images\image-20210704133107591.png)

**2. Extent**

The definition of Extent is given as:

*extent = shape area / bounding box area* i.e., it is simply defined as the ratio of actual shape area and the area of the bounding box, where the bounding box area is given as follows:

*bounding box area = bounding box width x bounding box height*

Extent is always <1, as the shape area (in pixels) cannot be greater than that of the bounding box area.

`area = cv.contourArea(cnt)`
`x,y,w,h = cv.boundingRect(cnt)`
`rect_area = w*h`
`extent = float(area)/rect_area`

**3. Solidity**

Solidity is defined as the  ratio of contour area to its convex hull area, i.e.:

*solidity = contour area / convex hull area*

Python Code for finding Solidity:

`area = cv.contourArea(cnt)`
`hull = cv.convexHull(cnt)`
`hull_area = cv.contourArea(hull)`
`solidity = float(area)/hull_area`

The value of solidity cannot be greater than 1, as the number of pixels inside a shape cannot outnumber the number of pixels in the convex hull, because by definition, the convex hull is the smallest possible set of pixels enclosing the shape.

**4**. **Equivalent Diameter**

Equivalent Diameter is the diameter of the circle whose area is same as the contour area.

EquivalentDiameter=√(4×ContourArea/π)

Following is the code for finding the Equivalent Diameter using Python:

`area = cv.contourArea(cnt)`
`equi_diameter = np.sqrt(4*area/np.pi)`

**5. Orientation**

Orientation is the angle at which object is directed.

Using the following line of code in Python, the orientation angle, Major and the Minor axes can be found out:

`(x,y),(MA,ma),angle = cv.fitEllipse(cnt)`

**6. Mask and Pixel Points**

In order to find all the pixel points having an object, we use non-zero masks in a gray-scale image.

Following is the Python code for doing so:

`mask = np.zeros(imgray.shape,np.uint8)`
`cv.drawContours(mask,[cnt],0,255,-1)`
`pixelpoints = cv.findNonZero(mask)`

**7. Maximum Value, Minimum Value and their locations**

We can use the `cv.minMaxLoc`to find the image locations with maximum and minimum values on a masked image, i.e.,

`min_val, max_val, min_loc, max_loc = cv.minMaxLoc(imgray,mask = mask)`

 **8. Mean Color or Mean Intensity**

We can also find the average color of an object, or the average intensity of the object in grayscale mode. We again use the same mask to do it.

`mean_val = cv.mean(im,mask = mask)`

**9. Extreme Points**

We can also find the extreme points from an image i.e. topmost, bottommost, rightmost and leftmost points of the object.

`leftmost = tuple(cnt[cnt[:,:,0].argmin()][0])`
`rightmost = tuple(cnt[cnt[:,:,0].argmax()][0])`
`topmost = tuple(cnt[cnt[:,:,1].argmin()][0])`
`bottommost = tuple(cnt[cnt[:,:,1].argmax()][0])`

The following image shows the extreme points located:

![image-20210704143101619](C:\Users\garim\AppData\Roaming\Typora\typora-user-images\image-20210704143101619.png)

