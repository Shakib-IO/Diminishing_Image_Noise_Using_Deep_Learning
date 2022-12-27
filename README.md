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
    

The Score Table:<br>

| Terms  | Peak Signal Noise Ratio(PSNR)  | Structural similarity index(SSIN) |
| :------------ |:---------------:| -----:|
| Original      | 28.28188495 | 0.6475486 |
| Predicted      | 32.34597064        |   0.80606692 |

---

- Deep Learning Models for Image Denoising
  - **AutoEncoder**<br>
      Autoencoders are an unsupervised learning technique in which we leverage neural networks for the task of representation learning. Specifically, we'll design a neural             network architecture such that we impose a bottleneck in the network which forces a compressed knowledge representation of the original input. If the input features were         each independent of one another, this compression and subsequent reconstruction would be a very difficult task. However, if some sort of structure exists in the data (ie.       correlations between input features), this structure can be learned and consequently leveraged when forcing the input through the network's bottleneck.
      
      The Architecture of AutoEncoder
![alt text](https://hackernoon.com/hn-images/1*8ixTe1VHLsmKB3AquWdxpQ.png)

The Score Table:<br>

| Terms  | Peak Signal Noise Ratio(PSNR)  | Structural similarity index(SSIN) |
| :------------ |:---------------:| -----:|
| Original      | 27.2716355 | 0.61189799 |
| Predicted      | 13.6541140        |   0.6257206 |

---


  - **RedNet: Residual Encoder-Decoder Network**<br>
      Indoor semantic segmentation has always been a difficult task in computer vision.An RGB-D residual encoder-decoder architecture, named RedNet, for indoor RGB-D semantic         segmentation. In RedNet, the residual module is applied to both the encoder and decoder as the basic building block, and the skip-connection is used to bypass the spatial       feature between the encoder and decoder. In order to incorporate the depth information of the scene, a fusion structure is constructed, which makes inference on RGB image       and depth image separately, and fuses their features over several layers. In order to efficiently optimize the network's parameters, we propose a pyramid supervision           training scheme, which applies supervised learning over different layers in the decoder, to cope with the problem of gradients vanishing. Experiment results show that the       proposed RedNet(ResNet-50) achieves a state-of-the-art mIoU accuracy of 47.8% on the SUN RGB-D benchmark dataset
      
      The Architecture of RedNetz<br>
<img src = "https://raw.githubusercontent.com/JindongJiang/RedNet/master/figure/overall_structure.png" width="100%" height="100%">


| Terms  | Peak Signal Noise Ratio(PSNR)  | Structural similarity index(SSIN) |
| :------------ |:---------------:| -----:|
| Original      | 26.2306718 | 0.57828607 |
| Predicted      | 16.369216        |   0.511164859 |

---

  - **MWCNN — Multi-level Wavelet CNN**<br>
      This is a wavelet-based deep learning architecture. Its architecture has a striking similarity with a U-Net architecture. The only difference in MWCNN is that, unlike down-sampling and up-sampling in U-Net, here we use DWT (Discrete Wavelet Transform) and IWT (Inverse Wavelet Transform). 
      
**Network Architecture**

Multi-level wavelet-CNN architecture. It consists two parts: the contracting and expanding subnetworks. Each solid box corresponds to a multi-channel feature map. And the number of channels is annotated on the top of the box. The network depth is 24. Moreover, our MWCNN can be further extended to higher level (e.g., ≥ 4) by duplicating the configuration of the 3rd level subnetwork.

<img src = "https://raw.githubusercontent.com/lpj0/MWCNN/master/images/Architecture.png">

<br>



[Github Link](https://github.com/lpj0/MWCNN)

[Paper Link](https://arxiv.org/abs/1805.07071)



| Terms  | Peak Signal Noise Ratio(PSNR)  | Structural similarity index(SSIN) |
| :------------ |:---------------:| -----:|
| Original      | 25.785195 | 0.59497514 |
| Predicted      | 28.908399 |   0.78549874 |

---


  - **PRIDNet — Pyramid Real Image Denoising Network**<br>
      While deep Convolutional Neural Networks (CNNs) have shown extraordinary capability of modelling specific noise and denoising, they still perform poorly on real-world noisy images. The main reason is that the real-world noise is more sophisticated and diverse. To tackle the issue of blind denoising, in this paper, we propose a novel pyramid real image denoising network (PRIDNet), which contains three stages. First, the noise estimation stage uses channel attention mechanism to recalibrate the channel importance of input noise. Second, at the multi-scale denoising stage, pyramid pooling is utilized to extract multi-scale features. Third, the stage of feature fusion adopts a kernel selecting operation to adaptively fuse multi-scale features. Experiments on two datasets of real noisy photographs demonstrate that our approach can achieve competitive performance in comparison with state-of-the-art denoisers in terms of both quantitative measure and visual perception quality.
      
**Network Architecture**

[Github Link](https://github.com/491506870/PRIDNet)<br>
[Paper Link](https://arxiv.org/abs/1908.00273?context=cs.CV)


| Terms  | Peak Signal Noise Ratio(PSNR)  | Structural similarity index(SSIN) |
| :------------ |:---------------:| -----:|
| Original      | 27.89533182 | 0.6145745 |
| Predicted      | 28.997406 |   0.71679110 |

---



