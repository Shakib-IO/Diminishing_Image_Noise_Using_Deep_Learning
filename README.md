# ***Image De-noising Using Deep Learning***


Denoising an image is a classical problem that researchers are trying to solve for decades. In earlier times, researchers used filters to reduce the noise in the images. They used to work fairly well for images with a reasonable level of noise. However, applying those filters would add a blur to the image. And if the image is too noisy, then the resultant image would be so blurry that most of the critical details in the image are lost.


There has to be a better way to solve this problem. As a result, I have implemented several deep learning architectures that far surpass the traditional denoising filters. In this blog, I will explain my approach step-by-step as a case study, starting from the problem formulation to implementing the state-of-the-art deep learning models, and then finally see the results.

So what we will focused on:
- What is noise in images?
- Source of Data
- Exploratory Data Analysis
- An Overview on Traditional Filters for Image Denoising
- Deep Learning Models for Image Denoising
- Results Comparison


---
- What is noise in images?
  - Image noise is a random variation of brightness or color information in the images captured. It is degradation in image signal caused by external sources. Mathematically, noise in an image can be represented by <br>**A(x,y) = B(x,y) + H(x,y)**<br>
    Where,<br>
    A(x,y)= function of noisy image;<br>
    B(x,y)= function of original image;<br>
    H(x,y)= function of noise;

---

- Paper's Link: <br>
1. REDNet :  https://arxiv.org/pdf/1606.08921.pdf <br>
2. MWCNN : https://arxiv.org/pdf/1805.07071.pdf <br>
3. PRIDNet : https://arxiv.org/pdf/1908.00273.pdf <br>

---
- Source of Data<br>
`For the limitation of GPU, only used SIDD Dataset`
  1. SIDD: https://www.eecs.yorku.ca/~kamel/sidd/dataset.php 
  2. RENOIR: https://adrianbarburesearch.blogspot.com/p/renoir-dataset.html
  3. NIND: https://commons.wikimedia.org/wiki/Natural_Image_Noise_Dataset#Tools

---
- Noisy Images

<img src="https://github.com/Shakib-IO/Diminishing_Image_Noise_Using_Deep_Learning/blob/main/Noisy%20Images/NOISY_SRGB_010.PNG" alt="" width="400" height="350">   <img src="https://github.com/Shakib-IO/Diminishing_Image_Noise_Using_Deep_Learning/blob/main/Noisy%20Images/NOISY__SRGB_010.PNG" alt="" width="400" height="350">

---
- GT Images

<img src="https://github.com/Shakib-IO/Diminishing_Image_Noise_Using_Deep_Learning/blob/main/GT%20images/GT_SRGB_010.PNG" alt="" width="400" height="350">   <img src="https://github.com/Shakib-IO/Diminishing_Image_Noise_Using_Deep_Learning/blob/main/GT%20images/GT__SRGB_010.PNG" alt="" width="400" height="350">

---
-  Feedback on EDA<br>
    - So, analyzing the dataset, we can see that most photos have been clicked on iPhone 7, Samsung S6 and Google Pixel. LG G4 has the least number of photos.<br>And the ISO level for each smartphone’s images are a total of 14 unique ISO level settings used in the dataset. Most of the photos are clicked at a low ISO setting.<br>Shutter speed for each smartphone’s images Most of the photos are clicked at 100 shutter speed, followed by 400 and      800.<br>The higher the shutter speed darker, the image will be, and vice-versa. Brightness level for each smartphone’s images The majority of the photos are clicked in Normal brightness mode.

---
- Fundamental & Traditional Filters: <br>
    - Researchers came up with filters to denoise an image. Most of the filters were specific to the type of noise the image has. There are several types of noises like Gaussian noise, Poisson noise, Speckle noise, Salt and Pepper noise, etc. There are specific filters for each type of noise. Hence, the first step to denoise an image using traditional filters is to identify the type of noise present in the image. After identifying that, we can go ahead and apply the specific filter. To identifying the type of noise, there are certain mathematical formulas to help us guess the type of noise. Or else a domain expert can decide it just by looking at the image. There are also some filters that work on any type of noise.
    - There are tons of filters available for denoising an image.In this datasets I will be discussing the Non-Local Means (NLM) algorithm which is seen to be working very well to denoise an image. Other filter like Median filter (MF), Adaptive Median filter (AMF) and Adaptive Wiener filter (AWF) will be implemented. The filters will be used to remove the additive noises present in the MRI images.
    
---
The Score Table:<br>

| Terms  | Peak Signal Noise Ratio(PSNR)  | Structural similarity index(SSIN) |
| :------------ |:---------------:| -----:|
| Original      | 28.28188495 | 0.6475486 |
| Predicted      | 32.34597064        |   0.80606692 |

---

