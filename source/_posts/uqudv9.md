---

## title: Pytorch·API 部署 WEB·ONNXdate: 2021-08-07 23:25:16

tags: [深度学习, 语义分割, Pytorch, ONNX, Web 开发]
categories: 计算机视觉特辑

1.API 接口，主要是通过中间商，为目标端暴露功能函数作为输入、处理、输出的桥梁。
2.WEB 预测 API 开发（基于 ONNX）

• ONNX 是用于机器学习模型云端发布的文件格式，是适用于不同框架的规范工具，

参考视频：How to run PyTorch models in the browser with ONNX.js - YouTube

[https://www.youtube.com/watch?v=Vs730jsRgO8](https://www.youtube.com/watch?v=Vs730jsRgO8)

项目地址：pytorch-to-javascript-with-onnx - CodeSandbox

[https://codesandbox.io/s/vgzep?file=/index.html](https://codesandbox.io/s/vgzep?file=/index.html)

• 训练并保存 model.state_dict()

○ ONNX 支持 pt 格式的模型介绍文件（model.state_dict()），训练时输入以下语句保存，也可以是 pth 格式

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE1.png#alt=%E5%9B%BE1)

○ 注意搭建模型的时候检查激活函数是否支持 ONNX，查询相关文档：

[https://github.com/microsoft/onnxjs/blob/v0.1.8/docs/operators.md](https://github.com/microsoft/onnxjs/blob/v0.1.8/docs/operators.md)

切换激活函数后还要更换对应的损失函数算法，比如 softmax 对应 nn.functional.cross_entropy()

○ 另外，ONNX 仅支持单 GPU 训练的 model，切勿使用 DataParellel 等 model。

○ 可以根据网络模型的 github 官网复制代码，搭建网络的时候要告知前端输入的图片尺寸，比如画布要绘制高清图可以预设网络输入尺寸为(280,280,4)，后期在池化层池化十倍即可。若 onnx 不能起作用，检查网络的 pytorch 语句是否有 bug（如池化时不能对图片切片而必须使用 torch.narrow(x)），可以查看 pytorch 官网文档或者中文文档的解释：

[https://pytorch.org/docs/stable/index.html](https://pytorch.org/docs/stable/index.html) or [https://pytorch-cn.readthedocs.io/zh/latest/](https://pytorch-cn.readthedocs.io/zh/latest/)

• pt 转 onnx 文件

○ 载入 pt 文件，切换为 eval 模式

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE2.png#alt=%E5%9B%BE2)

○ 预先构造空的待测影像矩阵，并同相关参数传入 torch.onnx.export()，导出 onnx 文件

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE3.png#alt=%E5%9B%BE3)

• 前端对 ONNX 文件的获取和操作/API 接口搭建

○ 首先，必须输入图中语句调用 ONNX 服务

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE4.png#alt=%E5%9B%BE4)

○ 训练后生成的 ONNX 文件直接部署到前端项目文件夹，ONNX 提供如下 js 操作以执行预测：

§ 新建 Session，并在 Session 中载入 model

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE5.png#alt=%E5%9B%BE5)

§ 获取服务器待预测图片，传入 Tensor

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE6.png#alt=%E5%9B%BE6)

§ 对图片执行预测

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE7.png#alt=%E5%9B%BE7)

§ 获取 model 输出 Tensor

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE8.png#alt=%E5%9B%BE8)

§ 从输出 Tensor 提取出概率分布矩阵

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE9.png#alt=%E5%9B%BE9)

§ 提取概率最大对应的分类结果（转化为分类结果）

![](Pytorch%C2%B7API%E9%83%A8%E7%BD%B2WEB%C2%B7ONNX/%E5%9B%BE10.png#alt=%E5%9B%BE10)

○ 每次后端准备搭建 API，以上都需要后端人员介绍给前端人员。

3.上面内容只是以分类任务为例子，👉

[https://github.com/microsoft/onnxjs/blob/v0.1.8/docs/api.md](https://github.com/microsoft/onnxjs/blob/v0.1.8/docs/api.md) 有更多 API 搭建手段提供给分类、检测、分割等不同计算机视觉任务，关于遥感智能解译还要进一步探索。
