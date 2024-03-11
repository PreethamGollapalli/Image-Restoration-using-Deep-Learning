# ***Image Restoration Using Deep Learning***


Restoring an image is a classical problem that researchers are trying to solve for decades. In earlier times, researchers used filters to reduce the noise in the images. They used to work fairly well for images with a reasonable level of noise. However, applying those filters would add a blur to the image. And if the image is too noisy, then the resultant image would be so blurry that most of the critical details in the image are lost.


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
1. MWCNN : https://arxiv.org/pdf/1805.07071.pdf <br>
2. PRIDNet : https://arxiv.org/pdf/1908.00273.pdf <br>

---
- Source of Data<br>
`For the limitation of GPU, only used SIDD Dataset`

  1. SIDD: https://www.eecs.yorku.ca/~kamel/sidd/dataset.php 
  2. NIND: https://commons.wikimedia.org/wiki/Natural_Image_Noise_Dataset#Tools

---
-  Feedback on EDA<br>
    - So, analyzing the dataset, we can see that most photos have been clicked on iPhone 7, Samsung S6 and Google Pixel. LG G4 has the least number of photos.<br>And the ISO level for each smartphone’s images are a total of 14 unique ISO level settings used in the dataset. Most of the photos are clicked at a low ISO setting.<br>Shutter speed for each smartphone’s images Most of the photos are clicked at 100 shutter speed, followed by 400 and      800.<br>The higher the shutter speed darker, the image will be, and vice-versa. Brightness level for each smartphone’s images The majority of the photos are clicked in Normal brightness mode.

---

  - **MWCNN — Multi-level Wavelet CNN**<br>
      This is a wavelet-based deep learning architecture. Its architecture has a striking similarity with a U-Net architecture. The only difference in MWCNN is that, unlike down-sampling and up-sampling in U-Net, here we use DWT (Discrete Wavelet Transform) and IWT (Inverse Wavelet Transform). 
      
**Network Architecture**

Multi-level wavelet-CNN architecture. It consists two parts: the contracting and expanding subnetworks. Each solid box corresponds to a multi-channel feature map. And the number of channels is annotated on the top of the box. The network depth is 24. Moreover, our MWCNN can be further extended to higher level (e.g., ≥ 4) by duplicating the configuration of the 3rd level subnetwork.

[Paper Link](https://arxiv.org/abs/1805.07071)


| Terms  | Peak Signal Noise Ratio(PSNR)  | Structural similarity index(SSIN) |
| :------------ |:---------------:| -----:|
| Original      | 25.785195 | 0.59497514 |
| Predicted      | 28.908399 |   0.78549874 |

---


  - **PRIDNet — Pyramid Real Image Denoising Network**<br>
      While deep Convolutional Neural Networks (CNNs) have shown extraordinary capability of modelling specific noise and denoising, they still perform poorly on real-world noisy images. The main reason is that the real-world noise is more sophisticated and diverse. To tackle the issue of blind denoising, in this paper, we propose a novel pyramid real image denoising network (PRIDNet), which contains three stages. First, the noise estimation stage uses channel attention mechanism to recalibrate the channel importance of input noise. Second, at the multi-scale denoising stage, pyramid pooling is utilized to extract multi-scale features. Third, the stage of feature fusion adopts a kernel selecting operation to adaptively fuse multi-scale features. Experiments on two datasets of real noisy photographs demonstrate that our approach can achieve competitive performance in comparison with state-of-the-art denoisers in terms of both quantitative measure and visual perception quality.
      
**Network Architecture**

[Paper Link](https://arxiv.org/abs/1908.00273?context=cs.CV)


| Terms  | Peak Signal Noise Ratio(PSNR)  | Structural similarity index(SSIN) |
| :------------ |:---------------:| -----:|
| Original      | 27.89533182 | 0.6145745 |
| Predicted      | 28.997406 |   0.71679110 |

---



