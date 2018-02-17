# Implementation of threshold moments

Kourmanalieva Antoine 

## Introduction 

Image segmentation segments a digital image based on a certain characteristic of the pixels is a well-known technique. The goal is to turn a grayscale image into a binary image, classifying each pixel into one of two categories, such as "dark" or "white". The most basic threshold technique is to choose a threshold value and compare each pixel to that value. Starting of this principle, many of thresholding methods have been developed. Among them, there are two main categories :  global thresholding, where a single threshold is used throughout the image to be divided into two classes and local thresholding, where the threshold values are determined locally, pixel by pixel or region by region. Three of four algorithm that will be presented Otsu, K-means and Entropie are part of the global thresholding category and are histogram based-methods. While the fourth algorithm, adaptive threshold is part of the local thresholding category and is based on the used of a kernel that runs through the image.

## Materiel and methods

### Threshold Moments

k-means clustering is a method of vector quantization, it is one of the most popular method for cluster analysis. k-means clustering aims to partition n observations into k clusters in which each observation belongs to the cluster with the nearest mean, serving as a prototype of the cluster. k is set by the observer. 

The method has been adapted to automatic thresholding : each cluster will represent one side of a threshold. Choosing 2 clusters (k=2) will result in a bilevel thresholding. Choosing 3 or more will result in a multilevel thresholding. The mean of each cluster is usually called a "centroid".

Programm summary:

1. Initialization of k-numbers of random centroids.
2. Create k-numbers of cluster by labeling each pixel of the image with its closest centroid.
3. Compute the mean of each cluster to create brand new k-numbers of centroids.
4. Label each pixel with its closest new centroid and confront them to the old labels :
    If the old and new labels are exactly the same, stop the loop.
    Else, new labels supersede old labels then repeat steps 3 and 4.
5. Each pixel take the value of its closest centroid. If k=2, each pixel can become black or white.


 
 ## Results
 
A benchmarking has been used to compare the methods. It uses the performance.now() method returning a DOMHighResTimeStamp, measured in milliseconds, accurate to five thousandths of a millisecond (5 microseconds). 
The results are in millisecond and represent the mean of 100 iterations of the method after 100 iteration to warming it up. It compares the method according to the size of an image (1 "lena" to 10 "lenas") and to two web browsers : Firefox (Quantum 57.0.2 64bits) and Chrome (63.0.3239.84 64bits).

### k-means

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

### Adaptive threshold

<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/benchImgJuju.png)" alt="Image" />
    <center><figcaption>Figure 6 : Benchmark of the Adaptive threshold method with Firefox and Chrome.</figcaption></center>
</figure>

The figure 6 show that the obtained results from benchmarks are very variables, it's very surprising. Indeed, we can observe that the execution times globally increases with the the image size increasing. However, we can also observes that the execution with biggest size images is sometimes faster with small pictures. Another benchmark with increasing size images is proportional did not show any variability in the results. An exponential curve is observed, which has been expected (Figure 7).

<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/benchAdapMe.png)" alt="Image" />
    <center><figcaption>Figure 7 : Benchmark of the Adaptative threshold method with proportional size images and with Firefox and Chrome</figcaption></center>
</figure>

A threshold was made with an 8 bits and 16 bits image(Figure 8).

<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/Adaptive.png)" alt="Image" />
    <center><figcaption>Figure 8 : Examples of the execution of 8bits(left) and 16 bits(rigth) image.</figcaption></center>
</figure>

### Max Entropy

The figure below show the result given by ImageJ’s function Auto-threshold which uses Max entropy method,and the maxEntropy() function implemented in javascript. We can see that we obtain similar results (Figure 9).

![]()

The results of benchmark for maxEntropy() function show two things. 

<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/BenchAlexis.png)" alt="Image" />
    <center><figcaption>Figure 9 : Execution time of maxEntropy() function with ten increasing image sizes (uint8 images)</figcaption></center>
</figure>

### Otsu

The two pictures below show the result given by ImageJ’s[^RUE2017] function Auto-threshold which uses Otsu method,and our otsu() function[^RID1978]. We can see that we obtain quite similar results(Figure 10).


<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/blobsmercia.png)" alt="Image" />
    <center><figcaption>Figure 10: Results of otsu method. on the left: original image, in the middle: output of our function, on the right: output of ImageJ Threshold.</figcaption></center>
</figure>

The result of our benchmark for our function for images uint8 shows us the expected result: the otsu() function is the fastest. the function takes longer as the image grows. We can also see that the differences between the two browsers are firefox and chrome, as we increase the size of the input image, the algorithm takes three more times the execution time.This result was expected for otsu because its algorithm  operates on histograms (which are integer or float arrays of length 256), it's quite fast unlike adaptive threshold for example(Figure 11).


<figure>
    <img src="(https://github.com/rmy17/bioinf-struct/blob/master/projectThreshold/images/BenchOtsuJuju.png)" alt="Image" />
    <center><figcaption>Figure 11: Execution time of the function with ten increasing image sizes (uint8 images).</figcaption></center>
</figure>

## Discussion

All the functions can handle the processing of pictures up to 2024x2024 pixels and maybe higher, and two types : uint8, uint16.

### K-means

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
 
 