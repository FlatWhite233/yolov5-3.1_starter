# ✨YOLOv5

## yolov5原仓库地址

https://github.com/ultralytics/yolov5

更多详细信息可阅读官方文档

<br>

# ✨项目说明

## 项目介绍

此项目主要用于

- 构建 **yolov5-3.1** 训练及检测环境

- 快速开始自定义训练与检测

<br>

训练所需权重可在 [yolov5-3.1 Release](https://github.com/ultralytics/yolov5/releases/tag/v3.1) 下载

<br>

**！注意：weights（权重）必须在下载 yolov5-3.1版本对应权重**

**！注意：weights（权重）必须在下载 yolov5-3.1版本对应权重**

**！注意：weights（权重）必须在下载 yolov5-3.1版本对应权重**

<br>

# ✨项目结构

- data

  - Annotations

    存放xml

  - images

    存放图片

- inference

  - images

    存放检测图片

- testTorchEnv.py

  检测torch环境

- makeTxt.py

  划分训练集验证集测试集

- voc_label.py

  标注转换yolo格式

- train.py

  训练

- detect.py

  检测

<br>

# ✨环境配置

建议使用[Miniconda]([Miniconda — conda documentation](https://docs.conda.io/en/latest/miniconda.html))或者[Anaconda](https://www.anaconda.com/)配置环境

首先配置 PyTorch CUDA环境

此部分可参考

[【深度学习】PyTorch CUDA环境配置及安装 - 双份浓缩馥芮白 - 博客园 (cnblogs.com)](https://www.cnblogs.com/Flat-White/p/14678586.html)

<br>

配置其余环境配置请运行：

```bash
pip install -r requirements.txt
```

原本yolov5-3.1的`requirements.txt`在本`starter`中被重命名为`requirements_backup.txt`

在`requirements.txt`中注释了部分torch、torchvision与非必要module

如果在`requirements.txt`中不注释torch、torchvision

`pip install -r requirements.txt`会默认安装CPU版PyTorch

当然若该环境仅用于单次推断不用于训练则CPU版PyTorch足矣

**运行前请自行检查`requirements.txt`**

<br>

## whl下载

torch：

https://download.pytorch.org/whl/torch_stable.html

opencv：

https://pypi.tuna.tsinghua.edu.cn/simple/opencv-python/

<br>

## pip国内源

```
豆瓣 https://pypi.doubanio.com/simple/
网易 https://mirrors.163.com/pypi/simple/
阿里云 https://mirrors.aliyun.com/pypi/simple/
腾讯云 https://mirrors.cloud.tencent.com/pypi/simple
清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/
```

<br>

## 已验证可运行环境

此项目在如下环境中依据下文**“快速开始自定义训练与检测”**可完美运行。

```
GPU：GTX 1060
torch：1.6
CUDA：10.2
cuDNN：8.1.0
```

```
GPU：RTX 3070Ti
torch：1.11.0
CUDA：11.3
cuDNN：8.6.0.163
```

<br>

# ✨快速开始自定义训练

训练前确保拥有如下数据及环境

- 数据集图片
- 数据集标注（通常为**labelImg**或者**精灵标注**标注得到的**xml文件**）
- PyTorch CUDA环境
- 训练所需权重（可前往 [yolov5-3.1 Release](https://github.com/ultralytics/yolov5/releases/tag/v3.1) 下载）

<br>

**注：yolov5-3.1安装最新版本的module进行训练可能会报错**

因此修改了`requirements.txt`中的>=为==

保证环境最大限度匹配

另外`opencv-python==4.1.2`不存在 需要安装`opencv-python==4.1.2.30`

<br>

## 1. 在相应目录存放图片与xml

- data

  - Annotations

    存放xml

  - images

    存放图片

<br>

## 2. 运行makeTxt.py（划分训练集验证集测试集）

<br>

## 3. 修改voc_label.py相关参数后运行（xml转换yolo格式）

```python
classes = ['demo']
```

<br>

## 4. 修改 data/demo.yaml

此步骤较好的习惯为将原`data`目录下的`coco.yaml`复制一份

然后重命名为`demo.yaml`

（demo可以修改为需要训练的数据集名称）

然后修改如下`demo.yaml`中的`nc`(类别数)与`names`(类别名称)

```yaml
# number of classes
nc: 1

# class names
names: ['demo']
```

<br>

## 5. 修改 models/yolov5s-demo.yaml

`models`目录下原本存在`yolov5s.yaml`、`yolov5l.yaml`、`yolov5m.yaml`、`yolov5x.yaml`

此步骤较好的习惯为将原`models`目录下的`yolov5s.yaml`

然后重命名为`yolov5s-demo.yaml`

（demo可以修改为需要训练的数据集名称，对于复制`yolov5s.yaml`、`yolov5l.yaml`、`yolov5m.yaml`、`yolov5x.yaml`中的哪一个根据实际训练需要）

然后修改如下`yolov5s-demo.yaml`中的`nc`(类别数)

```yaml
# parameters
nc: 1  # number of classes
```

<br>

## 6. 修改train.py 相关参数 开始训练

runs目录下查看训练结果

<br>

## 7. 设备性能不足

如果遇到 `OSError: [WinError 1455] 页面文件太小，无法完成操作。`

请减少 `batch-size`

~~或者使用虚拟内存~~

<br>

# ✨快速开始检测

## 1. 指定被检测的图片

在相应目录存放图片

inference

- images

  存放检测图片

<br>

或者也可以自行指定需要检测的图片/视频目录

修改`detect.py`中的`--source`参数即可

<br>

## 2. 开始检测

修改`detect.py`相关参数

运行`detect.py`开始检测

inference/output目录下查看检测后的图片

<br>

# ✨训练与检测 详细说明

## 训练

#### 1. 快速训练/复现训练

下载 [COCO数据集](https://github.com/wudashuo/yolov5/blob/master/data/scripts/get_coco.sh)，然后执行下面命令。根据你的显卡情况，使用最大的 `--batch-size` ，(下列命令中的batch size是16G显存的显卡推荐值).

```bash
$ python train.py --data coco.yaml --cfg yolov5s.yaml --weights '' --batch-size 64
                                         yolov5m.yaml                           40
                                         yolov5l.yaml                          24
                                         yolov5x.yaml                          16
```

四个模型yolov5s/m/l/x使用COCO数据集在单个V100显卡上的训练时间为2/4/6/8天。
<img src="https://user-images.githubusercontent.com/26833433/90222759-949d8800-ddc1-11ea-9fa1-1c97eed2b963.png" width="900">

#### 2. 自定义训练

##### 2.1 准备标签

yolo格式的标签为txt格式的文件，文件名跟对应的图片名一样，除了后缀改为了.txt。
具体格式如下：

- 每个目标一行，整个图片没有目标的话不需要有txt文件
- 每行的格式为`class_num x_center y_center width height`
- 其中`class_num`取值为`0`至`total_class - 1`，框的四个值`x_center` `y_center` `width` `height`是相对于图片分辨率大小正则化的`0-1`之间的数，左上角为`(0,0)`，右下角为`(1,1)`
  <img src="https://user-images.githubusercontent.com/26833433/91506361-c7965000-e886-11ea-8291-c72b98c25eec.jpg" width="900">
  最终的标签文件应该是这样的：
  <img src="https://user-images.githubusercontent.com/26833433/78174482-307bb800-740e-11ea-8b09-840693671042.png" width="900">

##### 2.2 数据规范

不同于DarkNet版yolo，图片和标签要分开存放。yolov5的代码会根据图片找标签，具体形式的把图片路径`/images/*.jpg`替换为`/labels/*.txt`，所以要新建两个文件夹，一个名为`images`存放图片，一个名为`labels`存放标签txt文件，如分训练集、验证集和测试集的话，还要再新建各自的文件夹，如图：
<img src="https://user-images.githubusercontent.com/26833433/83666389-bab4d980-a581-11ea-898b-b25471d37b83.jpg" width="900">

##### 2.3 准备yaml文件

自定义训练需要修改.yaml文件，一个是模型文件(可选)，一个是数据文件。

- 模型文件(可选):可以根据你选择训练的模型，直接修改`./models`里的`yolov5s.yaml` / `yolov5m.yaml` / `yolov5l.yaml` / `yolov5x.yaml`文件，只需要将`nc: 80`中的80修改为你数据集的类别数。其他为模型结构不需要改。
  **注意** :当需要随机初始化时才会使用本文件，官方推荐使用预训练权重初始化。

- 数据文件:根据`./data`文件夹里的coco数据文件，制作自己的数据文件，在数据文件中定义训练集、验证集、测试集路径；定义总类别数；定义类别名称

  ```yaml
  # train and val data as 1) directory: path/images/, 2) file: path/images.txt, or 3) list: [path1/images/, path2/images/]
  train: ../coco128/images/train2017/
  val: ../coco128/images/val2017/
  test:../coco128/images/test2017/
  
  # number of classes
  nc: 80
  
  # class names
  names: ['person', 'bicycle', 'car', 'motorcycle', 'airplane', 'bus', 'train', 'truck', 'boat', 'traffic light',
          'fire hydrant', 'stop sign', 'parking meter', 'bench', 'bird', 'cat', 'dog', 'horse', 'sheep', 'cow',
          'elephant', 'bear', 'zebra', 'giraffe', 'backpack', 'umbrella', 'handbag', 'tie', 'suitcase', 'frisbee',
          'skis', 'snowboard', 'sports ball', 'kite', 'baseball bat', 'baseball glove', 'skateboard', 'surfboard',
          'tennis racket', 'bottle', 'wine glass', 'cup', 'fork', 'knife', 'spoon', 'bowl', 'banana', 'apple',
          'sandwich', 'orange', 'broccoli', 'carrot', 'hot dog', 'pizza', 'donut', 'cake', 'chair', 'couch',
          'potted plant', 'bed', 'dining table', 'toilet', 'tv', 'laptop', 'mouse', 'remote', 'keyboard', 
          'cell phone', 'microwave', 'oven', 'toaster', 'sink', 'refrigerator', 'book', 'clock', 'vase', 'scissors', 
          'teddy bear', 'hair drier', 'toothbrush']
  ```

##### 2.4 进行训练

训练直接运行`train.py`即可，后面根据需要加上指令参数，`--weights`指定权重，`--data`指定数据文件，`--batch-size`指定batch大小，`--epochs`指定epoch。一个简单的训练语句：

```bash
# 使用yolov5s模型训练coco128数据集5个epochs，batch size设为16

$ python train.py --batch 16 --epochs 5 --data ./data/coco128.yaml --weights ./weights/yolov5s.pt
```

#### 3. 训练指令说明

有参：

- `--weights` (⭐)指定权重，如果不加此参数会默认使用COCO预训的`yolov5s.pt`，`--weights ''`则会随机初始化权重
- `--cfg` 指定模型文件
- `--data` (⭐)指定数据文件
- `--hyp`指定超参数文件
- `--epochs` (⭐)指定epoch数，默认300
- `--batch-size` (⭐)指定batch大小，默认`16`，官方推荐越大越好，用你GPU能承受最大的`batch size`，可简写为`--batch`
- `--img-size` 指定训练图片大小，默认`640`，可简写为`--img`
- `--name` 指定结果文件名，默认`result.txt`        
- `--device` 指定训练设备，如`--device 0,1,2,3`
- `--local_rank` 分布式训练参数，不要自己修改！
- `--log-imgs` W&B的图片数量，默认16，最大100
- `--workers` 指定dataloader的workers数量，默认`8`
- `--project` 训练结果存放目录，默认./runs/train/
- `--name` 训练结果存放名，默认exp

无参： 

- `--rect`矩形训练
- `--resume` 继续训练，默认从最后一次训练继续
- `--nosave` 训练中途不存储模型，只存最后一个checkpoint
- `--notest` 训练中途不在验证集上测试，训练完毕再测试
- `--noautoanchor` 关闭自动锚点检测
- `--evolve`超参数演变
- `--bucket`使用gsutil bucket
- `--cache-images` 使用缓存图片训练
- `--image-weights` 训练中对图片加权重
- `--multi-scale` 训练图片大小+/-50%变换
- `--single-cls` 单类训练
- `--adam` 使用torch.optim.Adam()优化器
- `--sync-bn` 使用SyncBatchNorm，只在分布式训练可用
- `--log-artifacts` 输出artifacts,即模型效果
- `--exist-ok` 如训练结果存放路径重名，不覆盖已存在的文件夹
- `--quad` 使用四分dataloader



## 检测

推理支持多种模式，图片、视频、文件夹、rtsp视频流和流媒体都支持。

#### 1. 简单检测命令

直接执行`detect.py`，指定一下要推理的目录即可，如果没有指定权重，会自动下载默认COCO预训练权重模型。手动下载：[Google Drive](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)、[国内网盘待上传](https://github.com/wudashuo/yolov5/blob/master/待上传)。 推理结果默认会保存到 `./runs/detect`中。

```
# 快速推理，--source 指定检测源，以下任意一种类型都支持：
$ python detect.py --source 0  # 本机默认摄像头
                            file.jpg  # 图片 
                            file.mp4  # 视频
                            path/  # 文件夹下所有媒体
                            rtsp://170.93.143.139/rtplive/470011e600ef003a004ee33696235daa  # rtsp视频流
                            http://112.50.243.8/PLTV/88888888/224/3221225900/1.m3u8  # http视频流
```

#### 2. 自定义检测

使用权重`./weights/yolov5s.pt`去推理`./data/images`文件夹下的所有媒体，并且推理置信度阈值设为0.5:

```
$ python detect.py --source ./data/images/ --weights ./weights/yolov5s.pt --conf 0.5
```

#### 3. 检测指令说明

自己根据需要加各种指令，新手只需关注带⭐的指令即可。

有参：

- `--source` (⭐)指定检测来源，详见上面的介绍
- `--weights` (⭐)指定权重，不指定的话会使用yolov5s.pt预训练权重
- `--img-size` `--imgsz` `--img` (⭐)指定推理图片分辨率，默认640，三个指令一样
- `--conf-thres` (⭐)指定置信度阈值，默认0.4，也可使用`--conf`
- `--iou-thres` 指定NMS(非极大值抑制)的IOU阈值，默认0.5
- `--max-det` 每张图最多检测多少目标
- `--device` 指定设备，如`--device 0` `--device 0,1,2,3` `--device cpu`
- `--classes` 只检测特定的类，如`--classes 0 2 4 6 8`
- `--project` 指定结果存放路径，默认./runs/detect/
- `--name` 指定结果存放名,默认exp
- `--line-thickness` 画图时线条宽度

无参：

- `--view-img` 图片形式显示结果
- `--save-txt` 输出标签结果(yolo格式)
- `--save-conf` 在输出标签结果txt中同样写入每个目标的置信度
- `--save-crop` 从图片\视频上把检测到的目标抠出来保存
- `--nosave` 不保存图片/视频
- `--agnostic-nms` 使用agnostic NMS(前背景)
- `--augment` 增强识别，速度会慢不少。[详情](https://github.com/ultralytics/yolov5/issues/303)
- `--update` 更新所有模型
- `--exist-ok` 若重名不覆盖
- `--hide-labels` 隐藏标签
- `--hide-conf` 隐藏置信度
- `--half` 半精度检测(FP16)

<br>

# ✨参考及引用

https://github.com/ultralytics/yolov5

https://github.com/wudashuo/yolov5

https://github.com/ultralytics/yolov5/wiki/Train-Custom-Data

https://blog.csdn.net/oJiWuXuan/article/details/107558286

<br>

# ⭐转载请注明出处

本文作者：双份浓缩馥芮白

版权所有，如需转载请注明出处。