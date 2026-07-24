# Deep-Learning-Semantic-Segmentation
Semantic segmentation of flood scenes from UAV imagery (FloodNet dataset) comparing U-Net and PSP-Net architectures

## Introduction
Our goal with this project is to perform semantic segmentation on drone imagery from natural disaster zones. We classify the imagery into 10 categories to specifically identify flooded infrastructure. Our motivation is to improve disaster response efforts to help rescue workers quickly locate flooded houses and streets. 

## Dataset
We utilized the [FloodNet Dataset](https://github.com/BinaLab/FloodNet-Supervised_v1.0/blob/main/README.md) (Rahnemoonfar et al., 2021), which consists of 2,343 high-resolution images (~1.5 cm/pixel) captured during Hurricane Harvey in Texas and Louisiana in 2017. The imagery is annotated with 10 distinct classes: Background, Flooded and Non-Flooded Buildings, Flooded and Non-Flooded Roads, Water, Trees, Vehicles, Pools, and Grass.

## Network Architectures
We compared two classic semantic segmentation models in this project. Both models were optimized using a custom **Hybrid Focal-Dice Loss** function to handle severe class imbalances.

**1. U-Net**
* **Architecture:** A symmetric encoder-decoder network with skip connections, which helps to mitigate information loss and recover fine-grained spatial details (like the sharp edges of flooded buildings).
* **Implementation:** We loaded a standard U-Net architecture directly via [PyTorch Hub](https://pytorch.org/hub/mateuszbuda_brain-segmentation-pytorch_unet/) (repository by Mateusz Buda).
* **Original Paper:** Ronneberger et al., 2015.

**2. PSP-Net**
* **Architecture:** A Pyramid Scene Parsing Network utilizing a massive `ResNet101` backbone as the feature encoder. This structure is highly effective at capturing global image context.
* **Implementation:** We initialized the model using the popular [Segmentation Models PyTorch (smp)](https://github.com/qubvel/segmentation_models.pytorch) library.
* **Original Paper:** Zhao et al., 2016.

## Methodology
We fed 1,445 training images into both the U-Net (trained entirely from scratch) and the PSP-Net models. Both models were trained using the AdamW optimizer to decouple weight decay and prevent over-regularization, while being optimized against a custom Hybrid Focal-Dice Loss function to effectively handle class imbalances. During the data loading process, all images and masks were resized to 512x512 pixels. To increase the volume and diversity of our training data, we augmented the images using random horizontal and vertical flips. The pixel values were then normalized to a standard range to ensure faster and more efficient training. The final model performance was subsequently evaluated on a dedicated test set of 448 images, where we assessed the predictions based on Mean IoU (mIoU), Mean Dice Score, and Overall Pixel Accuracy.

Loss Curve during Training U-Net
<img width="690" height="423" alt="image" src="https://github.com/user-attachments/assets/de6136e9-2c79-4034-bee7-ac7fc0e31de9" />

Loss Curve during Training PSP-Net
<img width="685" height="418" alt="image" src="https://github.com/user-attachments/assets/b8b71a0e-4475-4020-8e9d-feb69d4dfb15" />

## Result

Overall, the PSP-Net clearly outperformed the U-Net architecture. PSP-Net achieved a Mean IoU of 0.6132 and a Dice Score of 0.7463, while U-Net reached a Mean IoU of 0.4629 and a Dice Score of 0.5494.

Visual Result:

Legend:

<img width="186" height="193" alt="image" src="https://github.com/user-attachments/assets/348cc9bf-ecc2-4e1a-b822-e2ab72f4e635" />


U-Net Picture 9109:

<img width="750" height="300" alt="image" src="https://github.com/user-attachments/assets/6ec0e15b-f6fd-42e6-8e98-d62e95086c39" />

U-Net Picture 6831:

<img width="800" height="280" alt="image" src="https://github.com/user-attachments/assets/e0968da8-b0f1-46be-acfd-297f088e9172" />


PSP-Net Picture 7583:

<img width="729" height="267" alt="Bildschirmfoto 2026-07-24 um 09 02 16" src="https://github.com/user-attachments/assets/6992a15e-6841-4d21-b63e-231764c13001" />

PSP-Net Picture 7813:

<img width="729" height="267" alt="image" src="https://github.com/user-attachments/assets/70357cbe-dcc7-48ef-87f7-348ef31ce7b4" />






## References
* **FloodNet Dataset:** Rahnemoonfar, M., Chowdhury, T., Sarkar, A., Varshney, D., Yari, M., & Murphy, R. R. (2021). *FloodNet: A High Resolution Aerial Imagery Dataset for Post Flood Scene Understanding*. IEEE Access. [Dataset on GitHub](https://github.com/BinaLab/FloodNet-Supervised_v1.0)
* **U-Net Architecture:** Ronneberger, O., Fischer, P., & Brox, T. (2015). *U-Net: Convolutional Networks for Biomedical Image Segmentation*. Medical Image Computing and Computer-Assisted Intervention (MICCAI).
* **U-Net PyTorch Implementation:** Buda, M., Saha, A., & Mazurowski, M. A. (2019). *Association of genomic subtypes of lower-grade gliomas with shape features automatically extracted by a deep learning algorithm*. Computers in Biology and Medicine. [PyTorch Hub](https://pytorch.org/hub/mateuszbuda_brain-segmentation-pytorch_unet/)
* **PSP-Net Architecture:** Zhao, H., Shi, J., Qi, X., Wang, X., & Jia, J. (2016). *Pyramid Scene Parsing Network*. IEEE Conference on Computer Vision and Pattern Recognition (CVPR).
* **PSP-Net Implementation:** Yakubovskiy, P. (2020). *Segmentation Models PyTorch*. [GitHub Repository](https://github.com/qubvel/segmentation_models.pytorch)
