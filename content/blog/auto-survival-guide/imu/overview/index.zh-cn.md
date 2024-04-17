---
title: IMU 综述
date: 2022-12-01
authors:
  - name: Minghang Li
    link: https://github.com/lmh12138
    image: https://github.com/lmh12138.png
description: IMU（Inertial measurement unit），惯性测量单元
excludeSearch: false
math: true
---

> IMU（Inertial measurement unit），惯性测量单元。其作用是测量本身的加速度以及角速度，有时还通过磁力计来测量朝向，当包含磁力计时，IMU一般被称为IMMU。

## 零、测量原理

IMU的工作原理是通过其中包含的加速度计来测量X、Y、Z三个移动方向上的加速度，通过一重积分得到速度，通过二重积分得到位置，通过包含的陀螺仪测量Roll、Pitch、Yaw三个旋转方向上的角速度，通过一重积分得到姿态，包含磁力计的IMU还可以通过测量与地球磁场的夹角来确定当前的朝向，弥补加速度计在水平面上的测量缺失问题。

## 一、发展历程

这里引用一下知乎用户[任乾](https://www.zhihu.com/people/ren-gan-16)的几张图

![1](https://git.nrs-lab.com/LiMinghang23m/picgo-pic/-/raw/main/pictures/2023/01/18_11_43_54_caa43857180b5df9c242c59f9dc8011e.jpeg)

陀螺仪发展历程：

![2](https://git.nrs-lab.com/LiMinghang23m/picgo-pic/-/raw/main/pictures/2023/01/18_11_43_58_567709e353f7d721912910ffe0824086.jpeg)

加速度计发展历程：

![3](https://git.nrs-lab.com/LiMinghang23m/picgo-pic/-/raw/main/pictures/2023/01/18_11_44_4_e5a684d7b3988e15fc8c9d796708be43.jpeg)

## 二、作用与缺点

最早的IMU是用来给导弹、潜艇、船舶作惯性导航的，还可用在车辆上，尽可能多的收集当前车辆的速度、转弯率、航向的准确数据。现在的民用级IMU是广泛运用在智能手机、运动设备、游戏手柄等，主要用于感知姿态和方向，用作估计距离的地方不多

在导航中，通过卡尔曼滤波融合陀螺仪角速度积分与加速度计重力矢量解算得到的位置来估计高精度姿态。同时估计出的姿态用于将加速度计测量值转换为惯性参考系，一次积分得到线速度，二次积分得到位置，从而实现导航的目标。其好处在于不需要任何外来输入，也不需要装备在机身外侧，从而拥有了很好的隐蔽性以及抗干扰性。

用IMU进行导航的缺点是IMU会出现累计误差，所以导航和民用设备所需的IMU的精度也是大不相同的，陀螺仪的精度从0.1°/s到0.001°/h均有，加速度计从100mg到10ug的也都有，这些精度粗略的对比的话，意味着对于均未校准过的IMU来说，最便宜的精度100mg的加速度计在10秒之后会丧失了提供50米精度的能力，而最贵的精度10ug的IMU在17分钟之后才丧失提供50米精度的能力。

## 三、IMU误差

IMU的误差通常由以下几部分组成：

- 偏移误差：此项误差可分为传感器保持输入条件不变时的漂移，以及相同条件下的两次测量的不同
- 刻度因数误差：由于加速度计和陀螺仪均通过刻度因数进行信号转换，此中引入的非线性因素会导致误差
- 非敏感轴互耦误差：指的是传感器本身的轴存在不正交的情况导致的误差
- 安装误差：指的是传感器旋转与外界机身旋转不同轴带来的误差，与第三项误差基本相同，一个内一个外
- 加速度灵敏度误差：此项误差仅指陀螺仪，指的是陀螺仪的角速率测量因加速度的影响带来的误差
- 随机噪声：主要由结构的随机噪声和电路的随机噪声组成

不同领域对IMU精度的不同要求：

![4](https://git.nrs-lab.com/LiMinghang23m/picgo-pic/-/raw/main/pictures/2023/01/18_11_44_11_b44a8f21bffbef8247fe139ab50e244b.jpeg)

## 附、某学长写过的IMU专栏

[车把手和轱辘印的知乎专栏](https://www.zhihu.com/column/c_1428150857455681536)  