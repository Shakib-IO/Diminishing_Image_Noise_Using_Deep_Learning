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
<img src="https://github.com/Shakib-IO/Diminishing_Image_Noise_Using_Deep_Learning/blob/main/Noisy%20Images/NOISY_SRGB_010.PNG" alt="" width="500" height="400">
<img src="https://github.com/Shakib-IO/Diminishing_Image_Noise_Using_Deep_Learning/blob/main/Noisy%20Images/NOISY__SRGB_010.PNG" alt="" width="500" height="400">




