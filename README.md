# Image-Manipulation-Detection
## SpoofSense.ai task

** The given task is to detect image manipulation in the given set of images which contains authentic(unforged) and forged(copy-moved, spliced) images. **

### Data Exploration and Preparation:

There are two folders: traindev and test. Each of them contains 3 classes of images: authentic, copy-moved and spliced. copy-moved and spliced has two folders: images and masks. Masks are the segments of the images which highlights the forged region.

Types of image extensions:
1. .jpg
2. .png
3. .tif

The image and its corresponding masks are having the same file names.

** Observations: **
- The dataset has equal balance of copy-moved, spliced and authentic images (1494 images)
- Multiple dimensions of images: (256,384,3), (384, 256, 3), (600, 800, 3), etc. 
- More number of images are having the shape: (256, 384, 3)
- Masks are also same. The masks are all grayscale/binary. Few of them are 3D and 2D. All the masks are converted to 2D.
- In traindev data, specifically in copy-moved and spliced: Two images(1 copy-moved, 1 spliced) and their masks are having opposite dimensions. (copy-moved: c_1318 and spliced: s_0692)
- In test data, in copy-moved: One image and its mask is having opposite dimensions. (copy-moved: c_0041)
- Rotating these images fixed the mismatched dimensions.

### Feature Extraction:

- The approach used here is to sample the forged image around the forged region by comparing with it's respective mask and get multiple samples of size 64x64x3. 
- These would be considered as the main features of the image which can be used to train a Deep Learning Model such as a CNN.
- Using this sampling method, aprroximately 8 to 10 samples were generated per image.
- All of these samples contain a part of the forged region.
- These are used for training the model.
- References mentioned in the references.txt

### Model Training:
- 'Transfer Learning' was used here to take the advantage of pre-trained models such as VGGNet, ResNet, etc. and fine-tune these models acc. to the given task.
- In this approach, 'ResNet50' was used to detect the manipulated images and the final layers were added and trained using the extracted features from the training data. 
- Using this approach, for binary classification (manipulated or not), the model gave a 75% training accuracy and 66% testing accuracy. 
- This can be improved by data-augumentation, better fine-tuning and using more image manipulation techniques. Due to hardware-constraints, this was the best score that was achieved by this approach.


### Other approaches:
- Tried implementing MVSS_Net mentioned in the references, to create masks from the images and masks provided, and find out the accuracy using dice coefficient. But the code provided by the authors did not have a training feature to train our images.
- Tried implementing BusterNet mentioned in references, didn't yield good results.