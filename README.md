
## Bird's Eye view generation and Mapping through end-to-end deep learning.
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1gToGQ3_H7z4yEzM8Om0-zRdk9lGfQ50-?usp=sharing)

First of all, this project wouldn't had been possible without [Maciek Dziubiński](https://medium.com/@ponadto).

The repository works on building a model that takes in input the front camera image and generates the top-down view as well as simultaneous map generation (Can be thought of 2D SLAM). 

### Tesla's autopilot results:
<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/tesla.JPG?token=AKHLNLDG5IC3JBR3GLIA6LC64JYQ6" alt="drawing" width="150"/>


### Our results (In CARLA Simulator):
<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/ours.JPG?token=AKHLNLDMLLZC73V3BV25E6C64JYVO" alt="drawing" width="200"/>

## Training:

3 Models were trained:
 - U-Net
 - Autoencoder
 - Deeper Autoencoder

Model was trained using following losses:
 - SSIM
 - Dice Loss
 - Cross Entropy Loss


<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/train.JPG?token=AKHLNLCQSHVNQDCMV6XENQS64J6EY" alt="drawing"/>

<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/loss.JPG?token=AKHLNLGEPITHLWZKZLDSCZK64J644" alt="drawing"/>

### Front view images:

<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/Front.JPG?token=AKHLNLEAL25HAITHK7PDW4K64JYZG" alt="drawing"/>

### Predicted Bird's eye view:

<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/predicted.JPG?token=AKHLNLAZJRUH5RMGZYDV47K64JY5I" alt="drawing"/>

### Ground Truth:

<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/ground_truth.JPG?token=AKHLNLHUFWKVM735DNALYDS64JY7Y" alt="drawing"/>

### Testing on real world data (Comma10k dataset):

The model was trained on a simulator, but I was able to obtain good results after finetuning the model and some further image processing. See how the car is correctly localized to the right and th road curve is correctly detected.  

<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/comma10k.JPG" alt="drawing"/>


### Map Generation (In Progress) :

This is based on image stitching using map coordinate metadata. I noticed that SIFT/SURF, etc based image feature extractors and matchers do not work in this case since the images produced are very symmetrical and sparse in colors, therefore, no good/unique features can be extracted from these images to perform stitching based on pixels.

Hence, we use location coordintes based stitching. Images are simply overlapped along with correct rotation. 

<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/mapping.JPG?token=AKHLNLC2SGA5OFRCORWHRBS64J3HM" alt="drawing" width="400"/>

## Dataset:

### Dataset can be found [here.](https://drive.google.com/file/d/1x0JdeA2Mo_QvYIJDHMfempoy2R675gMi/view?usp=sharing)
 

<img src="https://raw.githubusercontent.com/MankaranSingh/Auto-Birds-Eye/master/images/DataSample.JPG?token=AKHLNLBGMGSIP375Y3HW2LK64JZEC" alt="drawing" width="500"/>

Although, the dataset contains images from **five** camera:
 
 - Front
 - Top
 - Left
 - Right
 - Rear

**Note:** For training the model, **only front images** were used to predict the **half top-down image.**

## Try this out on Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1gToGQ3_H7z4yEzM8Om0-zRdk9lGfQ50-?usp=sharing)

## References:

[https://mono.software/2018/03/14/Image-stitching/](https://mono.software/2018/03/14/Image-stitching/)

[https://medium.com/asap-report/from-semantic-segmentation-to-semantic-birds-eye-view-in-the-carla-simulator-1e636741af3f](https://medium.com/asap-report/from-semantic-segmentation-to-semantic-birds-eye-view-in-the-carla-simulator-1e636741af3f)
