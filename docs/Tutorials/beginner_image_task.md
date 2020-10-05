# 2.图像处理任务

### 图像处理任务简介

在RoboMaster比赛中，机器视觉一直是比赛中的核心技术，主要涉及以下两个点：

* 自动瞄准：利用枪口上的摄像头识别对面装甲板，自动控制枪口瞄准敌方装甲板，提高命中率。
* 能量机关：每年的能量机关任务都不一样，但不变的是都是一个非常有分量的视觉任务，从2018年的手写数字识别，到2019的大风车打靶，都离不开视觉的处理。

在视觉任务开发中，相机的驱动，图像的采集是一些重复的工作，rmoss_core/rm_task封装了这部分的操作，使得开发者只需要关心图像处理部分，加速开发速度。

本文涉及模块：

- rm_cam
- rm_task

### 图像处理开发样例：实时显示相机采集到的图像

对于图像相关任务，一般流程如下：

* 图像采集：通过相机采集图像，并发布成图片topic。
* 图像处理：订阅图片topic，对图片进行处理，得到指令，发布指令topic。
* 控制机器人：订阅指令topic，将指令转发给mcu，进而控制机器人采取行动。

本次开发样例，是一个非常简单的例子，只会简单展示一下图像处理的流程。

__step1:运行图像发布节点__

首先，需要启动图像发布节点，实现图像采集功能，这里利用usb相机:

运行：

```bash
ros2 launch rm_cam sim_cam_image.launch.py 
```

测试：

```bash
ros2 topic list #查看所有节点，检查图像节点是否发布
ros2 run rqt_image_view rqt_image_view#ros调试工具，图形化显示图像工具
```

__step2:运行图像处理节点__

运行：

```bash
ros2 launch rm_task task_show_image.launch.py 
```

* 图像将会实时显示（类似rqt_image_view的功能）

### 自定义图像处理任务开发

在显示图像任务中，主要代码在TaskShowImage类中，通过继承TaskImageRelatedBase基类，并实现相关接口，实现功能，在进行自定义开发时，最简单的实现只需要完成两步即可：

* 仿照TaskShowImage类，继承TaskImageRelatedBase，实现taskImageProcess接口。
* 仿照nodes/task_show_image_node.cpp完成main函数入口，启动节点。

具体实现：

* 参考[task_image_related 样例开发文档][1]
* 参考能量机关任务模块以及自动瞄准任务模块的实现



[1]: 

 