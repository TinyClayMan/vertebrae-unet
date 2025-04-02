# vertebrae-unet
## Description
This is a project I have done for the AI course in MIREA university (aka "Professional requalification «Software solutions of applied problems of Artificial Intelligence»"), which awarded a diploma (allegedly equivalent to a bachelor diploma). It was a year long course with its first half devoted to things like Python programming, elements of statistics and databases, and with the second part being devoted to all things neural networks: neural network architectures, training techniques, data preparation and normalization, etc.
## Data
The complete dataset consisted of 3192 radiograph images of human spinal columns. With the help of [VGG Image Annotator](https://github.com/ox-vgg/via/tree/master) 290 images were annotated by me and other members of the course, which were used for the training set. Because of insufficient communication, annotations of the data differed (e.g., files used both csv and json, annotated regions had different names) which required the data to be normalized.
## Process
### Data preprocessing
- Load datasets, determine whether they are in truncated form or not. Merge them into a single dataframe.
- Analyze data: count the amount of marked regions, which consist of vertebrae and intervertebral disks (1888 and 1751 regions, respectively).
- Reduce the amount of channels in the images (from 3 to 1), changing image size if needed.
- Draw masks for images with marked regions.
### U-Net creation
- Define the coder and decoder parts.
- Assemble UNet with
  - 4+1 encoders;
  - 4+1 decoders;
  - convolutional layer;
  - and final convolutinal layer with the number of filters equalling the number of classes.
### Training
- Split the dataset: 80% for training, 20% for validation.
- Create a unet with 3 classes and 32 base filters.
- Compile the network using
  - Adam optimizer;
  - Sparse categorical crossentropy for loss function.
- Train.

With the chosen hyperparameters, the created unet has 8.64m trainable parameters. 

40 epochs took ~10 minutes and resulted in a loss of 0.0597 and an accuracy of 0.977.
