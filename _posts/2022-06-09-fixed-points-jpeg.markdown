---
layout: post
title:  "Fixed points of the JPEG image compression algorithm"
date:   2022-06-09
usemath: true
---

A fixed point of a function $f(x)$ is a value $x$ such that $f(x) = f(f(x))$. Not all functions have fixed points, while some may have infinitely many. I couldn't find much literature on the topic, but I suspected that compression functions, which yield an approximation to the identity function, might display interesting behavior. The JPEG compression algorithm works by applying a Discrete Cosine Transform (DCT) and discarding high-frequency components, which for most photographic images does not yield substantial degredation in image quality. However, when applied to random noise, which has significant high-frequency components, we can see a noticable change in image quality.

![MSE, random noise](/assets/images/noiseJPEG.svg)

I used the `PIL` library to write a function to repeatedly convert an image from raw pixel data to JPEG format and back. I first tested this on 10,000 randomly generated 32x32 pixel arrays representing RGB pixel data, since this would give a reasonable baseline for worst-case performance of the compression algorithm. I first plotted the mean squared error for each of 40 iterations of JPEG compression:

![MSE, random noise](/assets/images/noiseError.svg)

The histogram shows a normally-distributed error curve with low variance, which indicates roughly similar performance on random inputs. 

![Histogram, Noise](/assets/images/noiseHist.svg)

Next, I decided to test a more realistic use-case for JPEG compression: photographic images. I randomly selected 10,000 32x32 images from the CIFAR-100 image database. As expected, the mean squared error values were several orders of magnitude lower than compression of random noise. Despite several outliers with unusually high error, every intitial state converged to a fixed point within 40 iterations.

![MSE, CIFAR100](/assets/images/CIFARerror.svg)

Unlike the tests with random noise, the number of iterations until convergence showed a weak bimodal distribution, with a substantial proportion of images converging on the first iteration, and a second, less pronounced centered around the fifth iteration. MSE appeared to follow a skew normal distribution. 

![Histogram, CIFAR100](/assets/images/CIFARhist.svg)


