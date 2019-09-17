

# TextSR-pytorch(code coming soon)

## introduction

* This project is a pytorch inplementation of the scene text picture super-resolution algorithm [TextSR](https://arxiv.org/abs/1909.07113).   TextSR is an end-to-end network aimed at restoring the low-resolution scene text images, in which the results of the text recognition network can feed back to guide the training of the super-resolution network. Under the guidance of the text recognition network, the super-resolution network would focus on refining the text region, and thus generate clear, sharp and identifiable text images.

* We mainly compare our method with SOTA super-resolution  method SRGAN.

* Demo: scene text image 'RONALDO' , for more details, refer to [TextSR](https://arxiv.org/abs/1909.07113).

![demo](./demo_pics/WechatIMG65.png)



## Datasets

* **Train:**

| Dataset       | Number | Note                                                         |
| ------------- | ------ | ------------------------------------------------------------ |
| SynthText     | 726W   | SynthText is the synthetic text dataset proposed in (Gupta, Vedaldi, and Zisserman 2016). It is proposed for text detection. We crop the words using the groundtruth word bounding boxes. You can crop the images by`python3 utils/crop_800k.py`, the output file syntax_crop.odgt contains the needed information to create the lmdb file of SynthText. |
| SynthText_hr: | 129W   | SynthText_hr are the images bigger than 128*32 in SynthText. |
| SynthText_HR: | 7W     | SynthText_HR are the images bigger than 256*64 in SynthText. |

* **Test:** 

Ic13, ic15, ic03, cute, svt, svtp, iiit5k

The 7 scene text recognition datasets can be found here: [STR datasets](https://github.com/chengzhanzhan/STR)

* **Convert LMDB:**

The LMDB files can be created by 

```go
python3 utils/create_lmdb.py
```

## Downloads

* Our re-implemented aster model: 

* Our re-implemented aster model(finetune): 

* Our TextSR model (128*32, trained on SynthText_hr): 

* Our TextSR model (256*64, trained on SynthText_HR): 

* SRGAN model (trained on ICDAR2013, ICDAR2015, SynthText_HR, 120 epochs): 

## Prerequisites

- Pytorch 1.1.0
- Cuda 9.0
- 
- 





## Training & testing & converting images

* **Training**

```go
python3 main.py --train_data_dir='syn800k_hr' --val_data_dir='ic15_1811' --width=128 --height=32 --epochs=10 --
```

* **Testing (lmdb file needed)**

Test all(super-resolute all the images)

```go
python3 main.py --test --test_data_dir='ic15_1811' --width=128 --height=32 
```

Test one by one (super_resolute the images of which original sizes are smaller than blur_w * blur_h)

```go
python3 main.py --test --single_test --test_data_dir='ic15_1811' --width=128 --height=32 --blur_w=64 --blur_h=32
```

* **Converting images to bicubic & SRGAN & TextSR**

```go
python3 main.py --convert --image_path='./' --width=128 --height=32 --ds_scale=4
```



## Demonstration

* **Recognition accuracy inprovement on scene text recognition datasets:**

Generator trained and tested on SynthText_hr (129W) with the input size of **128*32**

| dataset         | ic15 | ic13 | ic03 | CUTE80 | svt  | svtp | IIIT5K |
| --------------- | ---- | ---- | ---- | ------ | ---- | ---- | ------ |
| ASTER           |      |      |      |        |      |      |        |
| **improvement** |      |      |      |        |      |      |        |
| ASTER(fintune)  |      |      |      |        |      |      |        |
| **improvement** |      |      |      |        |      |      |        |

Generator trained and tested on SynthText_HR (7W) with the input size of **256*64**

| dataset         | ic15 | ic13 | ic03 | CUTE80 | svt  | svtp | IIIT5K |
| --------------- | ---- | ---- | ---- | ------ | ---- | ---- | ------ |
| ASTER           |      |      |      |        |      |      |        |
| **improvement** |      |      |      |        |      |      |        |
| ASTER(fintune)  |      |      |      |        |      |      |        |
| **improvement** |      |      |      |        |      |      |        |

* **Restoration ability on low-resolution text image recognition:**

With the test size decreases, the recognition accuracy of the images restored by TextSR are much higher than that by SRGAN. When the test images are downsampled to 20*5, our methods still have an accuracy of more than 40% whereas there are only 100 pixels in each image. 

**ICDAR2013**

Model trained on SynthText_HR (129W) with the input size of **128*32**

| size    | 128*32 | 64*16 | 32*8  | 24*6  | 20*5  |
| ------- | ------ | ----- | ----- | ----- | ----- |
| Bicubic | 90.5%  | 89.7% | 63.9% | 30.8% | 16.1% |
| SRGAN   | 90.6%  | 90.1% | 72.7% | 44.9% | 20.0% |
| TextSR  | 91.3%  | 90.5% | 83.1% | 62.6% | 42.8% |