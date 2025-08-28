## WORKSHOP
# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
### NAME : AVINASH T
### REG NO: 212223230026
Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.
Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.
## Program:

```c
## NAME: AVINASH T
## REG NO: 212223230026
import cv2
import matplotlib.pyplot as plt
import numpy as np
# Load the Face Image
faceImage = cv2.imread('Avinashimage.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```

<img width="1101" height="477" alt="image" src="https://github.com/user-attachments/assets/6bcdb059-6e19-4641-bc67-b242e5cf0f51" />

```c
faceImage.shape
```

<img width="851" height="41" alt="image" src="https://github.com/user-attachments/assets/f62ec5bc-5e9f-433f-9625-90035f7fcb87" />

```c
glassPNG = cv2.imread('glasses.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```

<img width="1085" height="329" alt="image" src="https://github.com/user-attachments/assets/45c58b50-cb94-4c0b-896a-15d1c79f4cec" />

```c

# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(550,250))
print("image Dimension ={}".format(glassPNG.shape))
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```

<img width="1101" height="290" alt="image" src="https://github.com/user-attachments/assets/bbfa037c-23fb-4696-9c3b-99c6ff03c697" />

```c
faceWithGlassesNaive = faceImage.copy()
# Replace the eye region with the sunglass image
faceWithGlassesNaive[640:890,290:840]=glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
```

<img width="1082" height="453" alt="image" src="https://github.com/user-attachments/assets/759836e1-e75a-4ada-ab14-fabf0f0d10d0" />

```c
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)
# Make a copy
faceWithGlassesArithmetic = faceImage.copy()
# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[640:890,290:840]
# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))
# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)
# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```

<img width="1102" height="224" alt="image" src="https://github.com/user-attachments/assets/327e51a5-a9eb-446d-b7d8-73dd475911bb" />

```c
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[640:890,290:840]=eyeRoiFinal
# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

<img width="1096" height="748" alt="image" src="https://github.com/user-attachments/assets/bc92523e-928f-4206-a54c-ee6fb1375e07" />



Feel free to fork, contribute, or customize this project for your creative needs!
