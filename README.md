# Histogram-Based Image Enhancement Using OpenCV

---

# Ex. No: 03  
# Histogram Equalization Using OpenCV (Grayscale & Color Images)

**Name :** PRASIDHA A  
**Reg. No :** 212224230204  
**Slot No :** T2-J6

---

## About the Project

This project demonstrates histogram equalization techniques using OpenCV in Python for both grayscale and color images.

Histogram equalization is an image processing technique used to improve image contrast by redistributing pixel intensity values across the histogram range. It enhances image visibility, brightness distribution, and feature clarity.

The experiment performs histogram equalization on:

- Grayscale images using direct histogram equalization
- Color images using HSV color space enhancement

The HSV-based enhancement preserves image color information while improving brightness and contrast through equalization of the Value (V) channel.

---

## Aim

To write a Python program using OpenCV to perform histogram equalization on both grayscale and color images to enhance image contrast and brightness.

The program performs the following operations:

- Read and display a grayscale image
- Plot histogram of the grayscale image
- Apply histogram equalization on grayscale image
- Read and display a color image
- Plot histogram of B, G, R channels
- Convert image to HSV color space
- Apply histogram equalization on the Value (V) channel
- Convert the enhanced image back to BGR format
- Display original and enhanced images with histograms

---

## Software Used

- Anaconda – Python 3.7
- Jupyter Notebook / VS Code
- OpenCV (cv2)
- NumPy
- Matplotlib

---

## Required Libraries

```bash
pip install opencv-python numpy matplotlib
```

---

## Input Image

Place the following image inside the project folder or inside the `images/` folder.

| Image Name | Purpose |
|------------|----------|
| `parrot.jpg` | Histogram Equalization on Grayscale and Color Images |

---

## Project Structure

```bash
Histogram-Based-Image-Enhancement-Using-OpenCV/
│
├── images/
│   └── parrot.jpg
│
├── output/
│   ├── grayscale_original.png
│   ├── grayscale_histogram.png
│   ├── grayscale_equalized.png
│   ├── grayscale_equalized_histogram.png
│   ├── color_original.png
│   ├── color_histogram.png
│   ├── enhanced_color.png
│   └── enhanced_histogram.png
│
├── histogram_equalization.py
├── histogram_equalization.ipynb
└── README.md
```

---

# Algorithm

### Step 1
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2
Read the image `parrot.jpg` in grayscale format.

### Step 3
Display the grayscale image and plot its histogram.

### Step 4
Apply histogram equalization using `cv2.equalizeHist()` to enhance contrast.

### Step 5
Display original grayscale image, its histogram, enhanced image, and its histogram using a 2 × 2 grid.

### Step 6
Read the same image in color format.

### Step 7
Split the image into B, G, R channels and plot their histograms.

### Step 8
Convert the image from BGR to HSV color space.

### Step 9
Apply histogram equalization on the V (Value) channel.

### Step 10
Merge the channels and convert the image back to BGR format.

### Step 11
Display original color image, histogram, enhanced image, and enhanced histogram using a 2 × 2 grid.

---

# Program

```python

# Histogram Equalization Using OpenCV

# Import required libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt

# PART 1 : GRAYSCALE HISTOGRAM EQUALIZATION

# Read the image in grayscale format
img_gray = cv2.imread('parrot.jpg', cv2.IMREAD_GRAYSCALE)

# Display grayscale image
plt.figure(figsize=(5,5))
plt.imshow(img_gray, cmap='gray')
plt.title("Original Grayscale Image")
plt.axis('off')
plt.show()

# Plot histogram of grayscale image
plt.figure(figsize=(6,4))
plt.hist(img_gray.ravel(), bins=256, range=[0,256])
plt.title("Histogram of Original Grayscale Image")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")
plt.show()

# Perform histogram equalization
equalized_img = cv2.equalizeHist(img_gray)

# Display images and histograms using 2x2 layout
plt.figure(figsize=(12,10))

# Original Grayscale Image
plt.subplot(2,2,1)
plt.imshow(img_gray, cmap='gray')
plt.title("Original Grayscale Image")
plt.axis('off')

# Histogram of Original Image
plt.subplot(2,2,2)
plt.hist(img_gray.ravel(), bins=256, range=[0,256])
plt.title("Histogram of Original Image")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")

# Equalized Image
plt.subplot(2,2,3)
plt.imshow(equalized_img, cmap='gray')
plt.title("Enhanced Equalized Image")
plt.axis('off')

# Histogram of Equalized Image
plt.subplot(2,2,4)
plt.hist(equalized_img.ravel(), bins=256, range=[0,256])
plt.title("Histogram of Enhanced Image")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")

plt.tight_layout()
plt.show()

# PART 2 : COLOR IMAGE HISTOGRAM EQUALIZATION

# Read the color image
img_color = cv2.imread('parrot.jpg')

# Convert BGR to RGB for display
img_rgb = cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB)

# Plot histogram of B, G, R channels
colors = ('b', 'g', 'r')

plt.figure(figsize=(6,4))

for i, color in enumerate(colors):
    hist = cv2.calcHist([img_color], [i], None, [256], [0,256])
    plt.plot(hist, color=color)

plt.title("Histogram of Original Color Image")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")
plt.show()

# Convert image from BGR to HSV
hsv = cv2.cvtColor(img_color, cv2.COLOR_BGR2HSV)

# Split HSV channels
h, s, v = cv2.split(hsv)

# Apply histogram equalization on V channel
v_equalized = cv2.equalizeHist(v)

# Merge HSV channels
hsv_equalized = cv2.merge((h, s, v_equalized))

# Convert HSV image back to BGR
enhanced_bgr = cv2.cvtColor(hsv_equalized, cv2.COLOR_HSV2BGR)

# Convert BGR to RGB for display
enhanced_rgb = cv2.cvtColor(enhanced_bgr, cv2.COLOR_BGR2RGB)

# Display original and enhanced images with histograms
plt.figure(figsize=(12,10))

# Original Color Image
plt.subplot(2,2,1)
plt.imshow(img_rgb)
plt.title("Original Color Image")
plt.axis('off')

# Histogram of Original Image
plt.subplot(2,2,2)

for i, color in enumerate(colors):
    hist = cv2.calcHist([img_color], [i], None, [256], [0,256])
    plt.plot(hist, color=color)

plt.title("Histogram of Original Image")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")

# Enhanced Color Image
plt.subplot(2,2,3)
plt.imshow(enhanced_rgb)
plt.title("Enhanced Color Image")
plt.axis('off')

# Histogram of Enhanced Image
plt.subplot(2,2,4)

for i, color in enumerate(colors):
    hist = cv2.calcHist([enhanced_bgr], [i], None, [256], [0,256])
    plt.plot(hist, color=color)

plt.title("Histogram of Enhanced Image")
plt.xlabel("Pixel Intensity")
plt.ylabel("Frequency")

plt.tight_layout()
plt.show()
```

---

# Experimental Outputs

---

## 1. Original Grayscale Image


<p align="center">
<img width="537" height="378" alt="image" src="https://github.com/user-attachments/assets/6d351694-995a-4698-97e5-82fee834e41a" />
</p>

---

## 2. Histogram of Original Grayscale Image


<p align="center">
<img width="773" height="496" alt="image" src="https://github.com/user-attachments/assets/86b805ad-d4bf-4a6c-98a1-974e2386635d" />
</p>

---

## 3. Equalized Grayscale Image


<p align="center">
<img width="967" height="392" alt="image" src="https://github.com/user-attachments/assets/32ca635f-5587-4d86-ba1f-49bb3880412a" />
</p>

---

## 4. Histogram of Equalized Grayscale Image


<p align="center">
<img width="660" height="463" alt="image" src="https://github.com/user-attachments/assets/b40fd4ec-b7f5-4f55-997b-216f8cbc0c77" />
</p>

---

## 5. Original Color Image


<p align="center">
<img width="877" height="657" alt="image" src="https://github.com/user-attachments/assets/a2d27bcb-fd19-4200-95e3-f02562b9b814" />
</p>

---

## 6. Histogram of Original Color Image


<p align="center">
<img width="779" height="590" alt="image" src="https://github.com/user-attachments/assets/4f60be93-32f5-466e-b281-44b8da793c9f" />
</p>

---

## 7. Enhanced Color Image


<p align="center">
<img width="763" height="586" alt="image" src="https://github.com/user-attachments/assets/c65554bb-cc5f-4ea2-8c0f-139a5706c68b" />
</p>

---

## 8. Histogram of Enhanced Color Image


<p align="center">
<img width="862" height="668" alt="image" src="https://github.com/user-attachments/assets/775a4728-375d-4862-8fcf-2e2596f1e67a" />
</p>

---

# Output

## Grayscale Histogram Equalization

- Original grayscale image is displayed
- Histogram of original grayscale image is plotted
- Enhanced image after histogram equalization is displayed
- Histogram of enhanced grayscale image shows improved contrast

---

## Color Image Histogram Equalization

- Original color image is displayed
- Histogram of B, G, R channels is plotted
- Enhanced image after HSV-based equalization is displayed
- Histogram of enhanced image shows better intensity distribution

---

# Result

Thus, histogram equalization is successfully performed on both grayscale and color images using OpenCV. The contrast and brightness of the images are significantly improved, enhancing visual quality and feature visibility.

---

# Learning Outcomes

By completing this experiment, we learn:

- Histogram equalization techniques
- Contrast enhancement methods
- HSV color space transformations
- Histogram plotting using Matplotlib
- Grayscale and color image enhancement
- OpenCV image processing fundamentals

---

# Developed By

| Name | Register Number |
|------|----------------|
| PRASIDHA A | 212224230204 |

