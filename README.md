

# TextSR-pytorch(code coming soon)

## introduction

This project is a pytorch inplementation of the scene text picture super-resolution algorithm TextSR (arxiv link).     TextSR is an end-to-end network, in which the results of the text recognition network can feed back to guide the training of the super-resolution network. Under the guidance of the text recognition network, the super-resolution network would focus on refining the text region, and thus generate clear, sharp and identifiable text images.

## Demonstration

### Super-resolution results on scene text recognition datasets:

The following images are mainly selected from CUTE80, ICDAR2013, ICDAR2015, ICDAR2003, etc.

| GT   | bicubic | SRGAN | TextSR |
| ---- | ------- | ----- | ------ |
|      |         |       |        |
|      |         |       |        |
|      |         |       |        |
|      |         |       |        |
|      |         |       |        |
|      |         |       |        |



### Super-resolution on scene text detection datasets:

| bicubic | SRGAN | TextSR |
| ------- | ----- | ------ |
|         |       |        |
|         |       |        |
|         |       |        |

###Recognition accuracy gap on scene text recognition datasets:

###Super-resolution effect on restoration of downsampled images:

## Prerequisites

* Pytorch 1.1.0
* Cuda 9.0
* 



## Downloads

Our re-implemented aster model:

Our TextSR model:

SynthText is the synthetic text dataset proposed in (Gupta, Vedaldi, and Zisserman 2016). It is proposed for text detection. We crop the words using the groundtruth word bounding boxes. You can crop the images by .

The LMDB files can be created by 

## Training & testing & converting images

### Trainging

### Testing (lmdb file needed)

###Converting images to bicubic & SRGAN & TextSR

