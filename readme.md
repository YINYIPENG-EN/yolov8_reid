

# 环境说明

详细查看项目中的requirements.txt

# 训练

将 **r50_ibn_2.pth，resnet50-19c8e357.pth**放在yolov8_reid/weights下【文末有权重下载链接】

```bash

python tools/train.py --config_file configs/softmax_triplet.yml

```

输入上述命令可快速开启训练~

【**这里只是reid的训练，不含yolov8的训练部分**，这是两个算法，请务必分清！这里只是两个算法做级联】

ps:arrow_right:**该训练reid项目与Reid_Search项目是独立的！！**训练完reid后，把训练好的权重放到**person_search/weights**下，切换到Reid_Search项目中在去进行reid识别【不然有时候会报can't import xxx】。

参数说明：

--config_file: 配置文件路径，默认configs/softmax_triplet.yml

--weights: pretrained weight path

--neck:  If train with BNNeck, options: **bnneck** or no

--test_neck:  BNNeck to be used for test, before or after BNNneck options: **before** or **after**

--model_name: Name of backbone.

--pretrain_choice: Imagenet

--IF_WITH_CENTER: us center loss, True or False.

:fountain_pen:

配置文件的修改：

(注意：项目中有两个配置文件，一个是config下的defaults.py配置文件，一个是configs下的yml配置文件，**一般配置yml文件即可**，当两个配置文件参数名相同的时候以yml文件为主，这个需要注意一下)

**configs文件**:

以**softmax_triplet.yml**为例：

```
SOLVER:
  OPTIMIZER_NAME: 'Adam' # 优化器
  MAX_EPOCHS: 120  # 总epochs
  BASE_LR: 0.00035
  IMS_PER_BATCH: 8  # batch
TEST:
  IMS_PER_BATCH: 4 # test batch
  RE_RANKING: 'no'
  WEIGHT: "path"  # test weight path
  FEAT_NORM: 'yes'
OUTPUT_DIR: "/logs" # model save path
```

```
=> Market1501 loaded
Dataset statistics:
  ----------------------------------------
  subset   | # ids | # images | # cameras
  ----------------------------------------
  train    |   751 |    12936 |         6
  query    |   750 |     3368 |         6
  gallery  |   751 |    15913 |         6
  ----------------------------------------
Loading pretrained ImageNet model......


2023-02-24 21:08:22.121 | INFO     | engine.trainer:log_training_loss:194 - Epoch[1] Iteration[19/1484] Loss: 9.194, Acc: 0.002, Base Lr: 3.82e-05
2023-02-24 21:08:22.315 | INFO     | engine.trainer:log_training_loss:194 - Epoch[1] Iteration[20/1484] Loss: 9.156, Acc: 0.002, Base Lr: 3.82e-05
2023-02-24 21:08:22.537 | INFO     | engine.trainer:log_training_loss:194 - Epoch[1] Iteration[21/1484] Loss: 9.119, Acc: 0.002, Base Lr: 3.82e-05


```



# 测试

输入以下命令即可快速开启测试，获得测试结果

【此脚本是针对训练后的模型单独获得测试结果，例如mAP、Rank等指标】

```shell
python tools/test.py --weights weights/ReID_resnet50_ibn_a.pth
```

测试结果如下：

```
Validation Results
mAP: 92.0%
CMC curve, Rank-1  :97.2%
CMC curve, Rank-5  :99.1%
CMC curve, Rank-10 :99.5%
```





#  训练预权重下载：

将 **r50_ibn_2.pth，resnet50-19c8e357.pth**放在yolov8_reid/weights下

链接：https://pan.baidu.com/s/1C4aQIr82kjQEdY-E0H8i3A 
提取码：yypn 



# 说明

开发不易，yolov8 reid中的**核心训练代码部分为有偿提供**。

训练代码为200RMB(不含tensorboard)，如果还需要包含tensorboard可视化为300RMB（含训练代码）。【拒绝讲价】

联系方式：wechat  y24065939s

CSDN：http://t.csdnimg.cn/71glP
