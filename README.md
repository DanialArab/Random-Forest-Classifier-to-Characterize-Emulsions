# Characterization of Emulsion Flow in Porous Media: Machine Learning Approach (Arab et al., 2022)

<a href="https://www.sciencedirect.com/science/article/abs/pii/S0920410522007045?via%3Dihub/" target="_blank" rel="noopener">link to the article</a>

In this work, we designed microfluidic experiments to investigate the effect of various chemicals to emulsify heavy oil in water. This repository is focused on the machine learning pipeline, where we used random forest classifier to perform pixel level microfluidic image segmentation. These results allow us to precisely calculate oil recovery and quantify the effect of various chemicals on emulsion droplet size distributions. Ground truths were generated using an annotation platform, apeer.com (Fig. 1b). As shown in Fig. 1c, oil, water, and glass were labelled as white, black, and gray, respectively.

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/A%20close-up%20view%20of%20microfluidic%20chip%20images.PNG)
Fig. 1: A close-up view of microfluidic chip images: a) the raw image captured during the experiment, b) the corresponding annotated image used to generate ground
truth, c) ground truth used as training dataset to train Random Forest classifier (Ground truths were generated using an annotation platform, apeer.com)

The training dataset containing a feature bank along with the ground truth masks were used to train the Random Forest classifier, which was then used to
segment the images not being used to train the model. The feature bank was framed using original pixel values, Gabor kernels (OpenCV (Open-Source Computer Vision Library) documentation on Gabor kernels), various edge detection kernels (Canny, Roberts, Sobel, Scharr, and Prewitt), Gaussian, Median, and Variance kernels (they are depicted in Fig. 2). Formulating the Random Forest classifier with the features bank allows us to precisely segment each pixel, which in turn was used to quantify the effect of various chemicals on oil recovery. All the scripts were generated in Python using OpenCV. 

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/filters.PNG)

Fig. 2: Various filters used to generate a feature bank: a) original (raw) image, b) Canny edge, c) Variance, d) Gabor, e) Gaussian (sigma=3), f) Gaussian (sigma=7), g) Median (sigma=3), h) Sobel

To quantify the size of oil clusters created due to various chemicals, each separated oil cluster is labeled through a different color, whose equivalent diameter was calculated through the regionprops module from the scikit-image library (Fig. 3 and 4).

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/Machine%20Learning%20results.PNG)

Fig. 3: Microfluidic images of ASP chemical injection: a)  the raw image captured during the experiment, b) the mask generated from the ML, c) the labelled image outputed from the ML results used for further cluster geometry and size analysis 

The continuous untouched oil, left behind after the water breakthrough is stripped due to the effect of ASP injection, which in turn widens the finger. This is also observed, to a smaller extent, in AS injection. This is insignificant when the injection solution is only polymer (for further details please refer to the link to the full article on top). These images were used to calculate the probability density function of oil clusters (Fig. 4d). The size distribution datasets were fitted to the Gamma distribution function (Fig. 4d): the average diameter of emulsion droplets in ASP flood is around 9 µm. These results are comparable with the droplet size analysis of the batch mixing experiments. The probability density function of oil clusters’ diameter at the end of the experiments, i.e., at the end of high velocity extended water flooding, is also included in Fig. 4d (see the dashed lines). As shown, the distributions of oil clusters at the end of AS and P floods are comparable to those observed at the end of the high velocity extended water floods. On the other hand, there is a significant reduction in the number of oil clusters due to the extended water injection following the ASP flood. As discussed, in this case, the chemical formulation efficiently emulsifies the oil in place with small sizes (around 9 µm on average), which can be pushed through the pore throats. This is the main reason behind the 6 % OOIP incremental oil recovery observed in the extended water flood following the ASP flood. 

![](https://raw.githubusercontent.com/DanialArab/images/main/my_papers/emulsion%20droplet.PNG)
Fig. 4: a, b, and c are the labelled images corresponding to the various stages of the ASP flood, d) probability density
function of the emulsion droplets labelled in a, b, and c (the probability density function of the emulsion droplets left at the end of the high-velocity water floods are also included in Fig. 3d, the corresponding labelled images are not shown).

