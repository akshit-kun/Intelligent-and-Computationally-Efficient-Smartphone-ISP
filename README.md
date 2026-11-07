# Hybrid Smartphone ISP

A smartphone Image Signal Processing (ISP) project that converts RAW
camera data into a finished RGB image. It combines traditional image
processing with a compact deep-learning model to improve image quality
while keeping the model small and fast.

## Project Overview

A phone camera sensor records only one colour (red, green, or blue) at
each pixel. The RAW image can contain noise, colour problems, brightness
issues, and white-balance errors.

This project uses a **hybrid approach**:

-   **Traditional image processing** handles steps such as white
    balance, colour correction, gamma correction, and tone adjustment.
-   **A compact INT8 U-Net model** helps remove noise and rebuild
    missing colour information.
-   The final system combines both methods to balance image quality and
    processing speed.

## Main Features

-   RAW-to-RGB image processing.
-   Classical ISP, direct deep-learning ISP, and hybrid ISP comparison.
-   White-balance correction using camera information when available.
-   Noise reduction and image restoration.
-   Compact INT8 U-Net model for faster processing.
-   Image quality comparison using PSNR, SSIM, LPIPS, and ΔE2000.
-   Browser-based demo.

## System Pipeline

1.  Read the input image.
2.  Prepare the RAW data and Bayer colour channels.
3.  Estimate noise and image brightness.
4.  Correct white balance.
5.  Prepare the image for the neural network.
6.  Restore the image using the compact U-Net.
7.  Apply colour correction and gamma correction.
8.  Produce the final RGB image.

## Demo

**Live application:**\
https://akshit-kun.github.io/Intelligent-and-Computationally-Efficient-Smartphone-ISP/

Open the link, choose a sample or upload a supported image, and click
**Process**. You can compare the Classical ISP, Hybrid ISP, and
Reference outputs.

The browser version runs the INT8 model using ONNX Runtime Web. Image
processing is performed in the browser, so uploaded images are not sent
to a server.

## Run Locally

### 1. Download the repository

``` bash
git clone https://github.com/akshit-kun/Intelligent-and-Computationally-Efficient-Smartphone-ISP.git
cd hybrid-smartphone-isp
```

You can also open the GitHub repository, select **Code → Download ZIP**,
and extract the files.

### 2. Install the required packages

``` bash
pip install -r requirements.txt
```

### 3. Start the application

``` bash
python app.py
```

Then open the local address shown in the terminal. The local application
uses Gradio.

## Model Information

The project includes different model sizes:

  Model               Parameters
  ----------------- ------------
  Reference model      4,022,444
  Compact model          947,036
  Tiny model             145,396

The compact INT8 model is used in the deployed hybrid system.

## Dataset

The models were trained and tested using the SIDD-CC dataset. It
contains real noisy and clean image pairs from five smartphones:

-   Google Pixel
-   iPhone 7
-   Samsung Galaxy S6 Edge
-   Motorola Nexus 6
-   LG G4

The report describes 204 training image pairs, 26 validation image
pairs, and 928 test blocks.

## Main Results

The main benchmark compares the Classical ISP, Deep Learning ISP, and
proposed Hybrid ISP.

  Method                PSNR (dB) ↑   SSIM ↑   LPIPS ↓   ΔE2000 ↓   Time per tile
  ------------------- ------------- -------- --------- ---------- ---------------
  Classical ISP               33.38   0.8668    0.2666       3.94           39 ms
  Deep Learning ISP           35.03   0.9059    0.1749       3.66          218 ms
  Hybrid ISP                  35.23   0.9126    0.1286       3.61         15 ms\*

\*The 15 ms figure is for the hybrid network only, not the complete
image-processing pipeline.

## Limitations

-   White-balance estimation is a major source of error.
-   The dataset contains only 10 real scenes.
-   Speed was measured on a laptop CPU, not on a smartphone.
-   Very noisy images may need multiple frames to recover more detail.
-   The model output may change small image details and should not be
    treated as forensic evidence.

## Team

**Team Name:** Soul Society --- Team 17

**Team Members:** - Akshitraj C - Akil Pranav G - Alok Murali - Aryan
Rajeev Gowda

## Repository

https://github.com/akshit-kun/Intelligent-and-Computationally-Efficient-Smartphone-ISP

## References

-   SIDD: A High-Quality Denoising Dataset for Smartphone Cameras.
-   U-Net: Convolutional Networks for Biomedical Image Segmentation.
-   Simple Baselines for Image Restoration.
-   Bilateral Filtering for Gray and Color Images.
-   Guided Image Filtering.
-   The CIEDE2000 Color-Difference Formula.

------------------------------------------------------------------------

**Note:** This README describes the project and its reported results.
Refer to the repository for the latest source code and setup details.
