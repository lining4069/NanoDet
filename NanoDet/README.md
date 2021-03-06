# NanoDet-PyTorch

* NanoDet作者开源代码地址：https://github.com/RangiLyu/nanodet  （致敬）
* **该代码基于NanoDet项目进行小裁剪，专门用来实现Python语言、PyTorch 版本的代码，支持图片、视频文件、摄像头实时目标检测。**

## NanoDet模型介绍

https://guo-pu.blog.csdn.net/article/details/110410940  

（借鉴，说明）下为上述模型介绍中的截取内容。

## 模型性能

Model     |Resolution|COCO mAP|Latency(ARM 4xCore)|FLOPS|Params   | Model Size(ncnn bin)
:--------:|:--------:|:------:|:-----------------:|:---:|:-------:|:-------:
NanoDet-m | 320*320 |  20.6 | 10.23ms | 0.72B   | 0.95M | 1.8mb
NanoDet-m | 416*416 |  21.7 | 16.44ms | 1.2B    | 0.95M | 1.8mb
YoloV3-Tiny| 416*416 | 16.6 | 37.6ms  | 5.62B   | 8.86M | 33.7mb
YoloV4-Tiny| 416*416 | 21.7 | 32.81ms | 6.96B   | 6.06M | 23.0mb

说明：
* 以上性能基于 ncnn 和麒麟 980 (4xA76+4xA55) ARM CPU 获得的
* 使用 COCO mAP (0.5:0.95) 作为评估指标，兼顾检测和定位的精度，在 COCO val 5000 张图片上测试，并且没有使用 Testing-Time-Augmentation。

## NanoDet损失函数
* NanoDet 使用了李翔等人提出的 Generalized Focal Loss 损失函数。该函数能够去掉 FCOS 的 Centerness 分支，省去这一分支上的大量卷积，从而减少检测头的计算开销，非常适合移动端的轻量化部署。
* 详细请参考：Generalized Focal Loss: Learning Qualified and Distributed Bounding Boxes for Dense Object Detection

## NanoDet 优势
* 超轻量级：模型文件大小仅几兆（小于4M——nanodet_m.pth）；
* 速度超快：在移动 ARM CPU 上的速度达到 97fps（10.23ms）；
* 训练友好：GPU 内存成本比其他模型低得多。GTX1060 6G 上的 Batch-size 为 80 即可运行；
* 方便部署：提供了基于 ncnn 推理框架的 C++ 实现和 Android demo。

## 开发环境
```text
Cython
termcolor
numpy
torch>=1.3
torchvision
tensorboard
pycocotools
matplotlib
pyaml
opencv-python
tqdm
```


## 运行程序
```text
'''目标检测-图片'''
# python detect_main.py image --config ./config/nanodet-m.yml --model model/nanodet_m.pth --path  street.png

'''目标检测-视频文件'''
# python detect_main.py video --config ./config/nanodet-m.yml --model model/nanodet_m.pth --path  test.mp4

'''目标检测-摄像头'''
# python detect_main.py webcam --config ./config/nanodet-m.yml --model model/nanodet_m.pth --path  0
```

## 详细介绍
https://guo-pu.blog.csdn.net/article/details/110410940

