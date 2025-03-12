# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

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

## PROGRAM & OUTPUT:

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
faceImage = cv2.imread('Pic.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```

![Screenshot 2025-03-12 190224](https://github.com/user-attachments/assets/6f5b6d23-4830-421f-977c-685f29db1cf8)

```
faceImage.shape
```

![Screenshot 2025-03-12 190316](https://github.com/user-attachments/assets/7f4ee424-b337-4a91-8f17-be5fbefae403)

```
glassPNG = cv2.imread('sunglass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```


![Screenshot 2025-03-12 190409](https://github.com/user-attachments/assets/bdef0f98-3bcc-4614-9c1b-172cf84311d8)

```
glassPNG = cv2.resize(glassPNG,(170,80))
print("image Dimension ={}".format(glassPNG.shape))
```


![Screenshot 2025-03-12 190459](https://github.com/user-attachments/assets/67d265b8-23c1-4099-a3f7-7f3bf8a83d8f)


```
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
```
```
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```

![Screenshot 2025-03-12 190615](https://github.com/user-attachments/assets/0d3d935d-df9e-4a5b-b51f-9dccfaa130ca)


```
faceWithGlassesNaive = faceImage.copy()

faceWithGlassesNaive[150:230, 125:295]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```

![Screenshot 2025-03-12 190659](https://github.com/user-attachments/assets/7bc93578-f88c-4282-bda0-66571869f54c)

```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

glassMask = np.uint8(glassMask/255)

faceWithGlassesArithmetic = faceImage.copy()

eyeROI= faceWithGlassesArithmetic[150:230, 125:295]

maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

maskedGlass = cv2.multiply(glassBGR,glassMask)

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```



![Screenshot 2025-03-12 190738](https://github.com/user-attachments/assets/61652485-3954-4414-a1fa-1743113c1e95)


```
faceWithGlassesArithmetic[150:230, 125:295]=eyeRoiFinal

plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```

![Screenshot 2025-03-12 190839](https://github.com/user-attachments/assets/93bfaad2-a576-4200-9b30-0bf3d70f1309)


