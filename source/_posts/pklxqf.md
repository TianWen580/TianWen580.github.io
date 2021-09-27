---

## title: Anaconda 环境日志 date: 2021-08-07 22:08:11

tags: [深度学习, 语义分割, Anaconda, Python]
categories: 计算机视觉特辑

1.创建虚拟环境

• conda create -n your_env_name python=X.X

2.更新 conda（慎用！！！，新 conda 可能用不了）

• conda updata conda

3.查看虚拟环境菜单和环境内已载入库

• conda env list/conda info -e

• conda list 4.激活虚拟环境

• Conda activate your_env_name

5.前人配置好的版本

• Keras2.2.4

• Tensorflow-gpu1.12.0

6.如果遇到 conda 安装频繁报错，使用如下语句：

• conda clean -i

7.如果不幸要删除虚拟环境

• conda remove -n your_env_name --all

8.如果 pip 安装报错如下，可以检查一下是不是翻墙了

![](Anaconda%E7%8E%AF%E5%A2%83%E6%97%A5%E5%BF%97/%E5%9B%BE1.png#alt=%E5%9B%BE1)

9.镜像 pip

• pip install -i [https://pypi.tuna.tsinghua.edu.cn/simple](https://pypi.tuna.tsinghua.edu.cn/simple) opencv-python

• pip install -i [https://pypi.douban.com/simple](https://pypi.douban.com/simple) opencv-python

10.大电脑虚拟环境记录：

• Main5：keras 开发框架

• labelme：用于打开 labelme 工具

• torch：Torch 开发框架

⚠️tensorflow、keras、python 对应版本关系：

![](Anaconda%E7%8E%AF%E5%A2%83%E6%97%A5%E5%BF%97/%E5%9B%BE2.png#alt=%E5%9B%BE2)

⚠️Tensorflow、CUDA、python、cudnn 版本关系：

![](Anaconda%E7%8E%AF%E5%A2%83%E6%97%A5%E5%BF%97/%E5%9B%BE3.png#alt=%E5%9B%BE3)

⚠️ 前人配置环境全赏:

![](Anaconda%E7%8E%AF%E5%A2%83%E6%97%A5%E5%BF%97/%E5%9B%BE4.jpg#alt=%E5%9B%BE4)
