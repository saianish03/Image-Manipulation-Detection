# Image-Manipulation-Detection
## SpoofSense.ai task

The given task is to detect image manipulation in the given set of images which contains authentic(unforged) and forged(copy-moved, spliced) images.
The approach used here is to sample the forged image around the forged region by comparing with it's respective mask and get multiple samples of size 64x64x3. These would be considered as the main features of the image which can be used to train a Deep Learning Model such as a CNN.

More precisely, 'Transfer Learning' was used here to take the advantage of pre-trained models such as VGGNet, ResNet, etc. and fine-tune these models acc. to the given task.
In this approach, 'ResNet50' was used to detect the manipulated images and the final layers were added and trained using the extracted features from the training data. 

This approach gave a 75% training accuracy and 66% testing accuracy. This can be improved by data-augumentation, better fine-tuning and using more image manipulation techniques. Due to hardware-constraints, this was the best score that was achieved by this approach.
