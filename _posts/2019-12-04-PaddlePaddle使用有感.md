---
layout: post
title: PaddlePaddle使用有感
tags: PaddlePaddle
---

今年十月份学校成立了个人工智能学院，准备在明年开始招生；估计是学校想做下教学实验，最近我的Java老师组了个AI兴趣班，也因此我接触到了PaddlePaddle。

先放一句总结：用PaddlePaddle，就请做好读源码准备(特别是那些想要用动态图的人)。

## 第一印象

作为用过Tensorflow的苦手，PaddlePaddle上手十分容易。一是中文文档较之英文易读，二是有百度的`AI Studio`练手，这一过程还是比较"愉快"的；同时官方还给出了[TensorFlow-Fluid常用接口对应表](https://paddlepaddle.org.cn/documentation/docs/zh/api_guides/X2Paddle/TensorFlow-Fluid.html)，总之，对使用过Tensorflow的用户十分之友好。

## 深入使用

我用PaddlePaddle做的第一个项目是Image Captioning任务，代码基本照抄`Show Attend and Tell`的Tensorflow版实现，这里讲下我的体验：一是绝对不能想当然，用Tensorflow的经验去套PaddlePaddle，举个例子，`fc`层(即`Dense`)里有个`num_flatten_dims`，不查文档还真就出大问题了；二是官方的使用指南不太完善，想要用预训练模型却不知道怎么导入参数，最后是翻` fluid.io.save_persistables `的源码才找到`load_vars`这个操作，并模仿源码写了个` predicate `才把参数导入进去的。三是"Bug"，`softmax_with_cross_entropy`这个函数似乎在梯度传导时有些毛病，搜索了好一番才在github的issue里找到了解决方法(顺带一提，PaddlePaddle的社区比Tensorflow差远了)。

## 吐槽PaddlePaddle动态图

整个文档只有这么一个[页面](https://paddlepaddle.org.cn/documentation/docs/zh/user_guides/howto/dygraph/DyGraph.html)是介绍动态图的。估计官方的意思是："想要用动态图？自己看源码去"。不说了，你们自己看看文档体会一下吧。



To be continue

