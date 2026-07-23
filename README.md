# Deep-Learning-Semantic-Segmentation-
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



## References
* **FloodNet Dataset:** Rahnemoonfar, M., Chowdhury, T., Sarkar, A., Varshney, D., Yari, M., & Murphy, R. R. (2021). *FloodNet: A High Resolution Aerial Imagery Dataset for Post Flood Scene Understanding*. IEEE Access. [Dataset on GitHub](https://github.com/BinaLab/FloodNet-Supervised_v1.0)
* **U-Net Architecture:** Ronneberger, O., Fischer, P., & Brox, T. (2015). *U-Net: Convolutional Networks for Biomedical Image Segmentation*. Medical Image Computing and Computer-Assisted Intervention (MICCAI).
* **U-Net PyTorch Implementation:** Buda, M., Saha, A., & Mazurowski, M. A. (2019). *Association of genomic subtypes of lower-grade gliomas with shape features automatically extracted by a deep learning algorithm*. Computers in Biology and Medicine. [PyTorch Hub](https://pytorch.org/hub/mateuszbuda_brain-segmentation-pytorch_unet/)
* **PSP-Net Architecture:** Zhao, H., Shi, J., Qi, X., Wang, X., & Jia, J. (2016). *Pyramid Scene Parsing Network*. IEEE Conference on Computer Vision and Pattern Recognition (CVPR).
* **PSP-Net Implementation:** Yakubovskiy, P. (2020). *Segmentation Models PyTorch*. [GitHub Repository](https://github.com/qubvel/segmentation_models.pytorch)
