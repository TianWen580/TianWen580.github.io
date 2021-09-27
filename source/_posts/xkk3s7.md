---

## title: Keras·gpu 训练（单\多）date: 2021-08-07 23:40:18

tags: [深度学习, 语义分割, Keras]
categories: 计算机视觉特辑

在一切开始前，请确定计算机拥有英伟达的显卡。

（不是英特尔！不是英特尔！不是英特尔！） 1.版本号：

• keras2.2.4

• Tensorflow-gpu1.12.0

• CUDA9.0.176

• cuDNN7.6.5 for CUDA 9.0

• Scikit-image

• Opencv-python

2.CUDA 下载

• 从 [https://developer.nvidia.com/cuda-toolkit-archive](https://developer.nvidia.com/cuda-toolkit-archive) 中打开下载中心，找到相应版本，点击版本号即可进入下载页面

![](Keras%C2%B7GPU%E8%AE%AD%E7%BB%83%EF%BC%88%E5%8D%95-%E5%A4%9A%EF%BC%89/%E5%9B%BE1.png#alt=%E5%9B%BE1)

• 选择要下载的平台、版本号等，点击 DOWNLOAD 即可

![](Keras%C2%B7GPU%E8%AE%AD%E7%BB%83%EF%BC%88%E5%8D%95-%E5%A4%9A%EF%BC%89/%E5%9B%BE2.png#alt=%E5%9B%BE2)

3.cuDNN 下载·安装

• 首先，把 CUDA 安装好，从 NVIDIA cuDNN | NVIDIA Developer [https://developer.nvidia.com/zh-cn/cudnn](https://developer.nvidia.com/zh-cn/cudnn)

中打开 cuDNN 中心，点击“下载 cuDNN”，登录之后填写问卷即可下载。最后 bin、include、lib 三个文件夹里的文件复制到 CUDA 的对应文件夹中就行了。

![](Keras%C2%B7GPU%E8%AE%AD%E7%BB%83%EF%BC%88%E5%8D%95-%E5%A4%9A%EF%BC%89/%E5%9B%BE3.png#alt=%E5%9B%BE3)

![](Keras%C2%B7GPU%E8%AE%AD%E7%BB%83%EF%BC%88%E5%8D%95-%E5%A4%9A%EF%BC%89/%E5%9B%BE4.png#alt=%E5%9B%BE4)

![](Keras%C2%B7GPU%E8%AE%AD%E7%BB%83%EF%BC%88%E5%8D%95-%E5%A4%9A%EF%BC%89/%E5%9B%BE5.png#alt=%E5%9B%BE5)

4.单 gpu 训练/多 gpu 训练

• 单 gpu 非常简单，只需要写图中语句即可用 keras 实现单 gpu 训练

![](Keras%C2%B7GPU%E8%AE%AD%E7%BB%83%EF%BC%88%E5%8D%95-%E5%A4%9A%EF%BC%89/%E5%9B%BE6.png#alt=%E5%9B%BE6)

• 多 gpu 需要用到 muti 函数生成模型，代码如下

![](Keras%C2%B7GPU%E8%AE%AD%E7%BB%83%EF%BC%88%E5%8D%95-%E5%A4%9A%EF%BC%89/%E5%9B%BE7.png#alt=%E5%9B%BE7)

5.找不到第二条 gpu

• 有时候 keras 识别不了电脑的第二条 gpu，执行 muti 会报错如下：

![](Keras%C2%B7GPU%E8%AE%AD%E7%BB%83%EF%BC%88%E5%8D%95-%E5%A4%9A%EF%BC%89/%E5%9B%BE8.png#alt=%E5%9B%BE8)

• 我这次是因为执行了这个语句造成的，这个语句只能供单 gpu 的 model 使用

![](Keras%C2%B7GPU%E8%AE%AD%E7%BB%83%EF%BC%88%E5%8D%95-%E5%A4%9A%EF%BC%89/%E5%9B%BE9.png#alt=%E5%9B%BE9)
