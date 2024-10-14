# SafeBlur: Automated Image Moderation Solution using GCP Native Services

## Overview

SafeBlur is an automated image moderation solution designed to ensure a safe online environment by detecting and blurring inappropriate user-uploaded images. Utilizing Google Cloud Functions, Cloud Storage, the Google Vision API, and GraphicsMagick, SafeBlur efficiently processes images uploaded to Google Cloud Storage.

## Features

- **Automated Moderation**: Automatically detects offensive content such as adult material and violence.
- **Image Processing**: Blurs images that contain inappropriate content to protect users.
- **Cloud-Based**: Fully leverages Google Cloud services for scalability and reliability.

## Architecture

![Architecture Diagram](./architecture.png)

### Components

1. **Google Cloud Functions**: Serves as the core processing unit triggered by image uploads.
2. **Google Vision API**: Analyzes images for potentially inappropriate content.
3. **GraphicsMagick**: Processes images by applying effects like blurring.
4. **Google Cloud Storage**: Stores original and processed images in separate buckets.

## Getting Started

### Prerequisites

- A Google Cloud account
- Google Cloud SDK installed
- Cloud Build API
- Cloud Functions API enabled
- Cloud Logging API enabled
- Cloud vision API enabled

### Installation

1. Create two buckets: one for original images (INPUT_BUCKET_NAME) and another for blurred images (BLURRED_BUCKET_NAME)

2. Create Cloud Run Function with 2 environment variables ready.
   INPUT_BUCKET_NAME : <your-input-bucket-name>
   BLURRED_BUCKET_NAME : <your-blurred-bucket-name>
   Edit the default entrypoint of the function to : blurOffensiveImages
   Write the function in blurOffensiveImages.js, save and deploy.

How It Works :

### How It Works:

1. Image Upload: Users upload images to the specified input bucket.
2. Trigger Function: The Cloud Function is triggered by new image uploads.
3. Content Analysis: The Google Vision API analyzes the image for potentially offensive content, such as adult material or violence.
4. Image Blurring: If inappropriate content is detected, the function downloads the image and applies a blur effect using GraphicsMagick.
5. Upload Blurred Image: The blurred image is then uploaded to the output bucket, replacing the original.

Example : Upload a violent image (a Zombie eating human brain),
![Architecture Diagram](./upload.png)

---

The Vision API classifies the image as inappropriate  
![Architecture Diagram](./logs.png)

---

The blurred image is created and uploaded into the Output Image Bucket(opimg)  
![Architecture Diagram](./blurUpload.png)

---

The blurred Image created and uploaded :  
![Architecture Diagram](./blurredImage.png)

---

### Error Handling

The code includes error handling for:

1. Image analysis failures
2. File download/upload issues
3. Image processing errors

### Benefits

Efficiency: Automates the tedious process of content moderation.  
Safety: Protects users by filtering out inappropriate content.  
Scalability: Built on Google Cloud, the system can handle large volumes of images.

### Conclusion

SafeBlur is a robust and scalable solution that harnesses the power of Google Cloud Platform to create a safer online environment. By effectively detecting and blurring inappropriate content, SafeBlur helps protect users, especially children, from harmful material.

This innovative solution can be seamlessly integrated into various applications and platforms, empowering developers and content creators to maintain a clean and user-friendly experience for their audiences. SafeBlur's contribution to a safer digital landscape is a significant step towards fostering a more positive and inclusive online community.
