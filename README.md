# Convolutional Neural Network (CNN) Project

This project demonstrates the implementation of a Convolutional Neural Network (CNN) for image processing using deep learning techniques. CNNs are a class of deep learning models that are particularly effective for analyzing visual data.

## Table of Contents

1. [Introduction](#introduction)
2. [Brief Introduction to CNN](#brief-introduction-to-cnn)
3. [Kernels in CNN](#kernels-in-cnn)
4. [Horizontal & Vertical Kernels](#horizontal--vertical-kernels)
5. [Edge & Depth Detection](#edge--depth-detection)
6. [Padding in CNN](#padding-in-cnn)
7. [Strides & Output Formula](#strides--output-formula)
8. [Different Scenarios Using Padding, Kernels, and Strides](#different-scenarios-using-padding-kernels-and-strides)
9. [Pooling](#pooling)
10. [CNN on Color Images](#cnn-on-color-images)
11. [Implementation](#implementation)
12. [Conclusion](#conclusion)
13. [References](#references)

## Introduction

In this project, we explore how to use pixels to perform image analysis using machine learning and deep learning techniques. While traditional machine learning approaches often fall short in accuracy, CNNs have proven to be highly effective in handling visual data.

## Brief Introduction to CNN

A Convolutional Neural Network (CNN) is a deep learning algorithm that can take an input image, assign importance (learnable weights and biases) to various aspects/objects in the image, and differentiate one from the other. The pre-processing required in a CNN is much lower compared to other classification algorithms. While in primitive methods filters are hand-engineered, CNNs can learn these filters/characteristics with enough training.

## Kernels in CNN

Kernels (or filters) in CNNs are small-sized matrices used to apply effects such as blurring, sharpening, edge detection, etc., to the input image. The kernel is convolved with the input data to produce a feature map.

## Horizontal & Vertical Kernels

Horizontal and vertical kernels are used to detect edges in images. Horizontal kernels emphasize horizontal edges, while vertical kernels emphasize vertical edges.

## Edge & Depth Detection

Edges in images are detected using filters/kernels by highlighting the high-frequency components. Depth in CNNs refers to the number of layers in the network, which allows for capturing more complex features from the images.

## Padding in CNN

Padding is the process of adding extra pixels around the border of an image. Padding allows us to control the spatial dimensions of the output feature maps. The formula for calculating the output dimensions when padding is used is:

\[ \text{Output\_height} = \frac{\text{Input\_height} + 2 \times \text{padding} - \text{kernel\_height}}{\text{stride}} + 1 \]

\[ \text{Output\_width} = \frac{\text{Input\_width} + 2 \times \text{padding} - \text{kernel\_width}}{\text{stride}} + 1 \]

## Strides & Output Formula

Strides are the number of pixels by which we slide our filter matrix over the input matrix. The formula for calculating the output dimensions when strides are used is:

\[ \text{Output\_height} = \frac{\text{Input\_height} - \text{kernel\_height}}{\text{stride}} + 1 \]

\[ \text{Output\_width} = \frac{\text{Input\_width} - \text{kernel\_width}}{\text{stride}} + 1 \]

## Different Scenarios Using Padding, Kernels, and Strides

1. **Only Kernel:**
   - When no padding and a stride of 1 are used.
   - Output dimensions are smaller than the input dimensions.

2. **Padding + Kernel:**
   - Padding is added to the input image, with a stride of 1.
   - Helps in retaining the original dimensions after convolution.

3. **Strides + Kernel:**
   - No padding is used, but strides are greater than 1.
   - Reduces the spatial dimensions of the output.

4. **Padding + Strides + Kernel:**
   - Both padding and strides are used.
   - Allows control over the spatial dimensions of the output more precisely.

## Pooling

Pooling is a down-sampling operation that reduces the dimensionality of the feature map. It retains the most important information while reducing computation.

### Types of Pooling

1. **Max Pooling:**
   - Takes the maximum value from the feature map region covered by the kernel.
   - Retains the most prominent features, making it effective for model learning.

2. **Average Pooling:**
   - Takes the average value from the feature map region covered by the kernel.
   - Smoothens the feature map, which might be useful in some scenarios.

3. **Min Pooling:**
   - Takes the minimum value from the feature map region covered by the kernel.
   - Useful in specific cases where the least prominent feature is of interest.

## CNN on Color Images

A color image has three channels: red, green, and blue (RGB).

For example, an 8x8 RGB image can be represented as:
- Red: 8x8x1
- Green: 8x8x1
- Blue: 8x8x1
- Combined: 8x8x3

When applying CNN on a color image:
- Red channel: 6x6x1
- Green channel: 6x6x1
- Blue channel: 6x6x1
- Combined: 6x6x3

Using three 3x3x3 kernels, the operation will process all RGB channels.

## Implementation

Below is an example implementation of a CNN using Python and TensorFlow/Keras:

```python
import tensorflow as tf
from tensorflow.keras import layers, models

# Define the model
model = models.Sequential()

# Add a convolutional layer
model.add(layers.Conv2D(32, (3, 3), activation='relu', input_shape=(28, 28, 1)))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))

# Add a dense layer
model.add(layers.Flatten())
model.add(layers.Dense(64, activation='relu'))
model.add(layers.Dense(10, activation='softmax'))

# Compile the model
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

# Summary of the model
model.summary()
```

## Conclusion

This README provided an overview of Convolutional Neural Networks, including key concepts such as kernels, padding, strides, pooling, and how they impact the output dimensions. The implementation section provided a basic example of constructing a CNN using TensorFlow/Keras. For more details, refer to the full code in the repository.

## References

- [Deep Learning with Python by François Chollet](https://www.manning.com/books/deep-learning-with-python)
- [Convolutional Neural Networks (CNNs) explained](https://cs231n.github.io/convolutional-networks/)