# Pix2Pix Paired Rain Synthesis 🌧️

## Overview

This project implements a **Pix2Pix Conditional Generative Adversarial Network (cGAN)** using PyTorch to generate synthetic rainy images from clean images.

The model learns the mapping between paired clean and rainy images. It uses a **U-Net Generator** to synthesize rain effects and a **conditional PatchGAN Discriminator** to distinguish generated rainy images from real rainy images while preserving the original scene structure.

## Features

- Paired clean and rainy image dataset.
- Image preprocessing and synchronized horizontal flipping.
- U-Net-based Generator with skip connections.
- Conditional PatchGAN Discriminator.
- Adversarial loss and L1 reconstruction loss.
- GPU training using PyTorch.
- Validation visualization and synthetic image export.

## Model Architecture

### Generator — U-Net

The Generator takes a clean RGB image as input and produces a synthetic rainy RGB image. Its encoder-decoder structure and skip connections help preserve scene details.

### Discriminator — Conditional PatchGAN

The Discriminator receives the clean image alongside either the real or generated rainy image. It predicts the authenticity of local image patches.

## Dataset

The dataset contains paired clean and rainy images organized into two folders:

```text
dataset/
├── gt/       # Clean images
└── rainy/    # Corresponding rainy images
```

- **Total paired images:** 1,201
- **Training pairs:** 1,080
- **Validation pairs:** 121
- **Input image size:** 256 × 256 pixels
- **Image channels:** RGB

Images are resized to 256 × 256, normalized to the range `[-1, 1]`, and randomly flipped horizontally during training. The same flip is applied to both images in a pair to preserve alignment.

## Training Configuration

| Parameter | Value |
|---|---|
| Framework | PyTorch |
| Image size | 256 × 256 |
| Batch size | 4 |
| Epochs | 50 |
| Optimizer | Adam |
| Learning rate | 0.0002 |
| Adam betas | (0.5, 0.999) |
| Adversarial loss | BCEWithLogitsLoss |
| Reconstruction loss | L1 Loss |
| L1 loss weight | 100 |

The Generator is trained to produce realistic rainy images while maintaining similarity to the paired ground-truth rainy images. The Discriminator learns to distinguish real rainy images from generated ones, conditioned on the corresponding clean images.

## Results

After 50 training epochs, the model generated **121 synthetic rainy validation images**.

The generated outputs demonstrate the learned clean-to-rainy image transformation while retaining important scene structures.

The project also produces a three-panel validation visualization:

**Clean Image → Generated Rain → Real Rain**


## Technologies Used

- Python
- PyTorch
- Torchvision
- NumPy
- Matplotlib
- Google Colab

