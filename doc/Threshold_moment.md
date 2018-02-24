# Implementation of threshold moments

Kourmanalieva Antoine 

## Introduction 

The image thresholding is mainly used in image analysis and is the most simple way for image segmentation.
It replaces one by one the pixels of an image using a fixed threshold value. Thus, if a pixel with a value greater than the threshold , it will take the value 255 (white), and if its value is lower (for example 100), it will take the value 0 (black).
It is called bilevel thresholding.
The Moments Thresholding method has been established by WEN-HSIANG TSAI [^TSA1985]. The implementation has been done using the Java code of ImageJ of the function moments() in the file AutoThresholder.java. This work has been performed in the context of the TIME project which stands for Tiny Image Processing in ECMAScript. The Material and methods part will describe the moment() function of ImageJ and the Benchmark procedure. The result part will be about the comparison of the proposed implementation with the ImageJ implementation.

## Materiel and methods

Tsai's method attempts to preserve the moments of the original image in the thresholded result. 
A new approach to automatic threshold selection using the moment-preserving principle. The threshold values are computed to preserve the moments of an input picture in the output picture. Experimental results show that the approach can be employed to threshold a given picture into meaningful gray-level classes. The approach is described for global thresholding, but can be used for local thresholding.
We will use boats image available on the time project and the ImageJ image samples in order to perform the Moments threshold.

#IMAGE BATEAUX

Two implementations will be used, functionnal and non functionnal javascript code. We will compare the time of processing by using benchmark on different sizes of image. We will also compare two Web Browsers : Firefox(version 57.0.4 (64bits)) and Chrome (version 64.0.3282.119 (64bits)). 
This benchmark will have a warm-up phase corresponding to 100 iterations of the function, followed by the application of the threshold on the different image sizes that are (in pixels): 360 * 288, 720 * 576, 1480 * 1152, 2960 * 2304, 3600 * 2880, 7200 * 5760. There will be 1000 executions of the Moment script by image size, we will record the time before and after the execution of the function. And we will calculate at the end of every 1000 iterations made on each image size, the average obtained from the execution time. It uses the performance.now() which mesure time in milliseconds.
 
 ## Results
 

<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/KmeansImage1.png)" alt="Image" />
    <center><figcaption>Figure 1 : Benchmark with Firefox and Chrome(F = Firefox, C = Chrome).</figcaption></center>
</figure>





## Discussion

All the functions can handle the processing of pictures up to 2024x2024 pixels and maybe higher, and two types : uint8, uint16.



Two implementations have been designed. The first one, as proposed in the program summary, following a direct description of the k-means clustering, has to read through each pixel of the image multiples times, to label them and to compare new and old label to each other. It is getting slower the bigger the image is.

The second method has be designed to improve the speed of the program. This implementation takes advantage of the histogram of the image and only has to read through 256 values at maxima for a 8-bit image - 65535 for a 16-bit image - when computing centroids or labelling each pixel with a cluster. A initialization step has been added to compute the histogram of the image.

## Conclusion

All the scripts works correctly and for those that can be compared to ImageJ functions, the results are identical. As planned, javascript in a web browser is slower than java compiled code in ImageJ. However these versions in javascript will allow to potentially make a web interface to use these with an Internet grader.

## References


[^GLAS1993]: Glasbey CA.An analysis of histogram-based thresholding algorithms.CVGIP: Graphical Models and Image Processing.1993 Nov;55:532-537.

[^RUE2017]: Rueden, Curtis T., et al. "ImageJ2: ImageJ for the next generation of scientific image data." BMC bioinformatics 18.1 (2017): 529.

[^TSA1985]: Tsai, W (1985), "Moment-preserving thresholding: a new approach", Computer Vision, Graphics, and Image Processing 29: 377-393
 
 
