# Solar Panel Defect Detection Using Deep Learning

## Overview

This project focuses on detecting defective solar panels in a solar array using semantic segmentation of overhead infrared (IR) images captured using drones.

The objective is to segment solar-panel regions and identify different defect categories while addressing the class-imbalance challenges present in the dataset.

## Defect Classes

The segmentation task considers the following classes:

- **LHS — Light Hot Spot**
- **DHS — Dark Hot Spot**
- **BP — ByPass Diode**
- **Normal — No Defect**

## Project Workflow

The project follows the following workflow:

1. Image and annotation preparation
2. Data preprocessing
3. Data augmentation
4. Annotation and mask correction
5. Semantic segmentation model training
6. Model experimentation with different loss functions
7. Validation and inference
8. Analysis of segmentation errors and model limitations

## Data Preprocessing

The preprocessing stage addressed issues related to the available training data and segmentation masks.

### Data Augmentation

To increase the available training data, augmentation techniques were applied, including:

- Rotation up to 15°
- Horizontal flipping
- Vertical flipping
- Shearing

### Mask Preprocessing

The annotation masks contained unexpected pixel values outside the expected class range.

The preprocessing workflow investigated the pixel-value distribution and identified incorrect class-value assignments. The masks were then corrected so that the pixel values represented the intended segmentation classes.

Details of the annotation and preprocessing procedure are provided in the corresponding project folders.

## Semantic Segmentation Models

Multiple deep learning model configurations were investigated.

The project includes experiments using:

- **PSPNet**
- **U-Net**

The experiments included both fine-tuned/pretrained models and different loss-function configurations.

## Loss Functions

Different loss configurations were investigated to address the strong class imbalance in the segmentation task.

The documented experiments include:

- Standard categorical cross-entropy (CCE)
- Weighted categorical cross-entropy
- Weighted focal loss

Higher loss weights were investigated for less frequently occurring defect classes so that the models would be less biased toward the dominant classes.

## Model Experiments

The training and results documentation contains multiple model experiments.

These experiments investigated:

- Fine-tuned PSPNet with default CCE
- Pretrained PSPNet with weighted CCE
- Pretrained PSPNet with weighted focal loss
- Pretrained U-Net with weighted CCE
- Different class-weight configurations

The experiments showed that the dominant Normal class could cause the model to predict the majority class excessively, making segmentation of less frequent defect classes difficult.

## Results and Observations

The project includes qualitative validation and inference results for the investigated models.

A major observation was the difficulty of segmenting rare defect classes when using a single model because of the imbalance between normal panels and defective-panel classes.

The documented experiments therefore explored class-weighted loss functions and a combination-of-models approach.

One proposed approach was to:

1. Develop a model to separate solar panels from the surrounding ground/background.
2. Use a second model to classify the segmented solar panels as defective or non-defective.

The detailed predictions, observations, and model-specific results are available in the `Training and results` folder.

## Project Structure

```text
solar-panel-defect-detection/
│
├── Annotations/
│   └── Annotation information and related documentation
│
├── Final_Notebook/
│   └── Finalized notebooks and model experiments
│
├── Preprocessing/
│   └── Data preprocessing and augmentation
│
├── Training and results/
│   └── Model experiments, predictions and observations
│
└── README.md
