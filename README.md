[//]:# (README file)
Image Resizing method (Nearest, Bilinear, and Bicubic) Comparison
==
Image scaling or resizing is extreamly useful tool. A good resizing method allows the user to modify the size of the image while retain the detail the user desires. The more common methods are: nearest-neighbor, bilinear, and bicubic. They are different in computation complexity, timing, and final image quality. This notebook will put the three methods into study and compare each other to determine which method is better under certain circumstance.
# Methods
##### Nearest-neighbor
The nearest-neighbor method is the most simple method of the three. It replaces every pixels with the nearest pixel in the output. It is the fastest method, so it is usually the go to method if timing is crucial. In some cases "nearest" does not have to be the mathematical nearest. In upsampling, OpenCV repeats the same pixel value up to the next sample pixel instead the true nearest pixel value.
##### Bilinear
The bilinear method takes the nearest 4 pixels, and replaces it with the weighted average of the 4 pixels. This method is great for continuous-tone images, but lose the contrast in the sharp edges. It is OpenCv use this method as default.
##### Bicubic
The bicubic method is the most complex of the three resizing methods. Simular to bilinear, it uses the weighted average to determine the pixel value, but unlike the bilinear method which uses the surounding 4 pixels, bicubic method uses 16 surrounding pixels (4 by 4) to determine the pixel value. The resized image using this methos usually are smoother and have fewer inerpolaiotn artifacts.

# Comparison 
### Scaling Up
The image up scaled by the nearest-neighbor method is too blocky to be identify what is written. The image up scaled by the bilinera method is more readable than the nearest-neighbor, but is still glossy. The image up scaled by the bicubic method is the most legible of the three methods.
![ ](img/plate_rm.png)
### Scaling Down
While making the image smaller, bilinear and bicubic method retained some detail from the orignal image, while nearest-neighbor method will lost some small detail. In this example, the image, lena has be resized to 1/10 of its original size. For better visualization, each image has resized back to its original size using nearest-neighbor method. The eyes of lena is no longer visible in nearest-neighbor method while bilinear and bicubic retain the detail of the eyes.
![ ](img/lena_rm.png)
# Performance
Each scaling methods is being applied to a image dataset form Urban Object Detection wihch contains 106920 jpeg images with mostly dimension of 1280 by 960. The magnitude of scaling is 10x both in height and width. The nearest-neighbor is expected to be the fastest. The bicubic method takes almost double the amount of time, and the bilinear method takes more than double of the time. A further experiment with less image imputs but with differentt magnitude of scaling (from 2x to 10x). The experiment shows that the bilinear method only out performs bicubic method when the magitude of scaling is below 4x. However, while down scaling the image, bilinear constantly out performs bicubic.
![ ](img/perform_us.png)
![ ](img/perform_ds.png)
# Conclusion
For up scaling an image, bicubic will always produce the best images. For down scaling an image, bilinear is a more effective method.
# License
The contents of this repository are covered under the [MIT](LICENSE) License.
# Reference
* Wikipedia. Image scaling. Retrieved on Augest 1, 2019, from https://en.wikipedia.org/wiki/Image_scaling

* OpenCV. Geometric Image Transformations. Retrieved on Augest 1, 2019, from https://docs.opencv.org/2.4/modules/imgproc/doc/geometric_transformations.html

* License Plate: Cropped and retrieved on Augest 1, 2019, from https://miro.medium.com/max/700/1*EYFejGUjvjPcc4PZTwoufw.jpeg

* Lenna: Wikipedia. Lenna. Retrieved Augest 2, 2019, from: https://en.wikipedia.org/wiki/Lenna

* A. Dominguez-Sanchez, M. Cazorla, and S. Orts-Escolano. (2018). Urban Object Detection dataset. Retrieved Augest 2, 2019, from: http://www.rovit.ua.es/dataset/traffic
