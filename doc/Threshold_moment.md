# Implementation of threshold moments

Kourmanalieva Antoine 

## Introduction 

The image thresholding is mainly used in image analysis and is the most simple way for image segmentation.
It replaces one by one the pixels of an image using a fixed threshold value. Thus, if a pixel with a value greater than the threshold , it will take the value 255 (white), and if its value is lower (for example 100), it will take the value 0 (black).
It is called bilevel thresholding.


This method has been established by WEN-HSIANG TSAI. Here is proposed two implementations of this method in JavaScript, with one using the paradigm of functional programming. The implementation has been done using the Java code of ImageJ of the function moment() in the file AutoThresholder.java. This work has been performed in the context of the time project which stands for Tiny Image Processing in ECMAScript. It can be found on the Github crazybiocomputing. The Material and methods part will describe the moment() function of ImageJ and the Benchmark procedure. The result part will be about the comparison of the proposed implementation with the ImageJ implementation.

## Materiel and methods

### Threshold Moments



 
 ## Results
 
A benchmarking has been used to compare the methods. It uses the performance.now() method returning a DOMHighResTimeStamp, measured in milliseconds, accurate to five thousandths of a millisecond (5 microseconds). 
The results are in millisecond and represent the mean of 100 iterations of the method after 100 iteration to warming it up. It compares the method according to the size of an image (1 "lena" to 10 "lenas") and to two web browsers : Firefox (Quantum 57.0.2 64bits) and Chrome (63.0.3239.84 64bits).

### Threshold Moments

<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/KmeansImage1.png)" alt="Image" />
    <center><figcaption>Figure 1 : Benchmark with Firefox and Chrome(F = Firefox, C = Chrome).</figcaption></center>
</figure>

 The two implemented methods are faster on Firefox than on Chrome. The result are also less fluctuating on Firefox(Figure 1). 

<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/KmeansImage2.png)" alt="Image" />
    <center><figcaption>Figure 2 : Comparison between two implementation with and without histogram.</figcaption></center>
</figure>

The second method implemented is faster than the first (10 times faster on a 512*512 pixels image to 50 times faster on a image with 10x more pixels)(Figure 2). 


<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/KmeansImage3.png)" alt="Image" />
    <center><figcaption>Figure 3 : Benchmark to compare the two K values K=2 and K=3 using Firefox.</figcaption></center>
</figure>

The number of loop turn is only correlated to the k-number and not to the image size(Figure 3). 


<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/KmeansImage4.png)" alt="Image" />
    <center><figcaption>Figure 4 : Ratio of time between the execution of algorithm and the creation od raster using Firefox.</figcaption></center>
</figure>

The loading of the Raster in the method takes around 75% of the time of the method(Figure 4).

Bilevel thresholding and multilevel thresholding can be done with k-means clustering. The left image is the original, then it is a bilevel thresholding, then 3 clusters k-means (so 2 thresholds, 3 shades of grey) and finally 9 clusters k-means(Figure 5). 

<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/ExempleKmeans.png)" alt="Image" />
    <center><figcaption>Figure 5 : Examples of differents executions</figcaption></center>
</figure>



## Discussion

All the functions can handle the processing of pictures up to 2024x2024 pixels and maybe higher, and two types : uint8, uint16.

### Threshold Moments

Two implementations have been designed. The first one, as proposed in the program summary, following a direct description of the k-means clustering, has to read through each pixel of the image multiples times, to label them and to compare new and old label to each other. It is getting slower the bigger the image is.

The second method has be designed to improve the speed of the program. This implementation takes advantage of the histogram of the image and only has to read through 256 values at maxima for a 8-bit image - 65535 for a 16-bit image - when computing centroids or labelling each pixel with a cluster. A initialization step has been added to compute the histogram of the image.

## Conclusion

All the scripts works correctly and for those that can be compared to ImageJ functions, the results are identical. As planned, javascript in a web browser is slower than java compiled code in ImageJ. However these versions in javascript will allow to potentially make a web interface to use these with an Internet grader.

## References

[^BRA2007]: Bradley D, Roth G. Adaptive thresholding using integral image. Journal of Graphics Tools. Volume 12, Issue 2.  pp. 13-21. 2007. NRC 48816.

[^GLAS1993]: Glasbey CA.An analysis of histogram-based thresholding algorithms.CVGIP: Graphical Models and Image Processing.1993 Nov;55:532-537.

[^KAP1985]: Kapur JN, Sahoo PK, Wong ACK.A New Method for Gray-Level Picture Thresholding Using the Entropy of the Histogram.Graphical Models and Image Processing.1985 Mar;29(3):273-285.

[^OTS1979]: Otsu N.A threshold selection method from gray-level histograms.IEEE Transactions on systems, man and cybernetics.1979 Jan;9:62-66.

[^RID1978]: Ridler TW, Calvard S.Picture thresholding using an iterative selection method.IEEE Transactions on Systems, Man and Cybernetics.1978 Aug ;8:630-632.

[^RUE2017]: Rueden, Curtis T., et al. "ImageJ2: ImageJ for the next generation of scientific image data." BMC bioinformatics 18.1 (2017): 529.
 
 
