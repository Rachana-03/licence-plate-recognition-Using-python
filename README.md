# licence-plate-recognition-Using-python
This project is created by using concept of Deep learning,python,opencv etc.


OpenCV is an open-sourf ce machine learning library and provides a common infrastructure for computer vision. Whereas Pytesseract is a Tesseract-OCR Engine to read image types and extract the information present in the image.

Gaussian Blur: Here we use a Gaussian kernel to smoothen the image. Gaussian Blur operation, the image is convolved with a Gaussian filter instead of the box filter. The Gaussian filter is a low-pass filter that removes the high-frequency components are reduced.In image processing, a Gaussian blur (also known as Gaussian smoothing) is the result of blurring an image by a Gaussian function . It is a widely used effect in graphics software, typically to reduce image noise
You can perform this operation on an image using the Gaussianblur() method of the imgproc class. Following is the syntax of this method −
GaussianBlur(src, dst, ksize, sigmaX)
This method accepts the following parameters −
    • src − A Mat object representing the source (input image) for this operation.
    • dst − A Mat object representing the destination (output image) for this operation.
    • ksize − A Size object representing the size of the kernel.
    • sigmaX − A variable of the type double representing the Gaussian kernel standard deviation in X direction.

Sobel Operator
    1. The Sobel Operator is a discrete differentiation operator. It computes an approximation of the gradient of an image intensity function. 
    2. The Sobel Operator combines Gaussian smoothing and differentiation. 
Following is the syntax of this method −
Sobel(src, dst, ddepth, dx, dy)
This method accepts the following parameters −
    • src − An object of the class Mat representing the source (input) image.
    • dst − An object of the class Mat representing the destination (output) image.
    • ddepth − An integer variable representing the depth of the image (-1)
    • dx − An integer variable representing the x-derivative. (0 or 1)
    • dy − An integer variable representing the y-derivative. (0 or 1)

Morphological transformations are some simple operations based on the image shape. It is normally performed on binary images. It needs two inputs, one is our original image, second one is called structuring element or kernel which decides the nature of operation.
The basic morphological operations are Erosion, Dilation, Opening, Closing. The different functions provided in OpenCV are:
    • cv2.erode()
    • cv2.dilate()
    • cv2.morphologyEx()
Erosion
The basic idea of erosion is just like soil erosion only, it erodes away the boundaries of foreground object (Always try to keep foreground in white). So what does it do? The kernel slides through the image (as in 2D convolution). A pixel in the original image (either 1 or 0) will be considered 1 only if all the pixels under the kernel is 1, otherwise it is eroded (made to zero).
So what happends is that, all the pixels near boundary will be discarded depending upon the size of kernel. So the thickness or size of the foreground object decreases or simply white region decreases in the image. It is useful for removing small white noises (as we have seen in colorspace chapter), detach two connected objects etc.
syntax :erosion = cv2.erode(img,kernel,iterations = 1)
Dilation
It is just opposite of erosion. Here, a pixel element is ‘1’ if atleast one pixel under the kernel is ‘1’. So it increases the white region in the image or size of foreground object increases. Normally, in cases like noise removal, erosion is followed by dilation. Because, erosion removes white noises, but it also shrinks our object. So we dilate it. Since noise is gone, they won’t come back, but our object area increases. It is also useful in joining broken parts of an object.
dilation = cv2.dilate(img,kernel,iterations = 1)
Morphological Gradient
It is the difference between dilation and erosion of an image.
The result will look like the outline of the object.
gradient = cv2.morphologyEx(img, cv2.MORPH_GRADIENT, kernel)
What are contours? 
Contours can be explained simply as a curve joining all the continuous points (along the boundary), having same color or intensity. The contours are a useful tool for shape analysis and object detection and recognition.
    • For better accuracy, use binary images. So before finding contours, apply threshold or canny edge detection. 
    • Since OpenCV 3.2, findContours() no longer modifies the source image. 
    • In OpenCV, finding contours is like finding white object from black background. So remember, object to be found should be white and background should be black. 
findContours() method of cv2 library to find all boundary points(x,y) of an object in the image

++++++++cv2.findContours(src, contour_retrieval, contours_approximation)++++++++++\
Parameters
You need to pass three parameters to findContours() method.
    1. src: Input Image of n – dimensional array(n = 2,3) but preferred 2-dim binary images for better result. 
    2. contour_retrieval: This is contour retrieval mode. Possible values are :
a) cv2.RETR_TREE
b) cv2.RETR_EXTERNAL
c) cv2.RETR_LIST
d) cv2.RETR_CCOMP etc. 
    3. contours_approximation: This is Contour approximation method. Possible values are :
a) cv2.CHAIN_APPROX_NONE
b) cv2.CHAIN_APPROX_SIMPLE 
Return Value
It returns three values :
a) Input image array
b) Contours
c) Hierarchy
Note:
1) Contours is a Python list of all the contours in the image. Each individual contour is a Numpy array of (x,y) coordinates of boundary points of the object.
2) Hierarchy is the parent-child relationship in contours. It is represented as an array of four values : [Next contour, previous contour, First child contour, Parent contour]

Contours Approximation Method

Above, we see that contours are the boundaries of a shape with the same intensity. It stores the (x, y) coordinates of the boundary of a shape. But does it store all the coordinates? That is specified by this contour approximation method.
If we pass cv2.CHAIN_APPROX_NONE, all the boundary points are captured. But actually, do we need all the points? For eg, if we need find the contour of a straight line. We require just two endpoints of that line. In that case, you can pass cv2.CHAIN_APPROX_SIMPLE. It excludes all excessive points and compresses the contour, thereby saving memory.
