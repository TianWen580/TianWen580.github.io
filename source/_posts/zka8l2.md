---

## title: TensorboardX 训练可视化 date: 2021-08-07 22:43:00

tags: [深度学习, 语义分割, 可视化, TensorboardX]
categories: 计算机视觉特辑

1.conda 环境配置：

• tensorboardX2.2

• Tensorboard2.5.0

• PyTorch1.8.1

• Torchvision0.9.1 2.查看记录

• 首先学习以下 tensorboardX 怎么用。一般训练代码运行之后会同时生成 tensorboardX 的日志文件。这时复制日志文件所在文件夹路径，打开 Anaconda 命令行，切换环境至 torch，输入图中语句为日志文件夹创建 tensorboardX 默认的本地端口（格式：tensorboard --logdir PATH）

![](TensorboardX%E8%AE%AD%E7%BB%83%E5%8F%AF%E8%A7%86%E5%8C%96/%E5%9B%BE1.png#alt=%E5%9B%BE1)

• 执行得到端口地址，复制到浏览器打开即可查看训练可视化内容

![](TensorboardX%E8%AE%AD%E7%BB%83%E5%8F%AF%E8%A7%86%E5%8C%96/%E5%9B%BE2.png#alt=%E5%9B%BE2)

![](TensorboardX%E8%AE%AD%E7%BB%83%E5%8F%AF%E8%A7%86%E5%8C%96/%E5%9B%BE3.png#alt=%E5%9B%BE3)

• 关闭端口占用，只需长按 CTRL + C

3.训练记录

• 导入 SummaryWriter

![](TensorboardX%E8%AE%AD%E7%BB%83%E5%8F%AF%E8%A7%86%E5%8C%96/%E5%9B%BE4.png#alt=%E5%9B%BE4)

• 在代码中初始化 SummaryWriter 实例，参数填记录的存储文件夹位置（有其他初始化方法，这里不常用）

![](TensorboardX%E8%AE%AD%E7%BB%83%E5%8F%AF%E8%A7%86%E5%8C%96/%E5%9B%BE5.png#alt=%E5%9B%BE5)

• 训练常用记录类型：

○ （scalar）单个数值

§ 参数：

□ Tag：该数据名称（如 train_acc），不同名称数据会用独立图表表示

□ Scalar_value：数据值来源，一般是个 python 变量（如 train_acc）

□ Global_step：存放当前 epoch 值

□ walltime：默认值 time.time()，记录当下时间，一般填 None 不用

§ 用法：如 writer.add_scalar()

○ （scalars）多个数值

多个数值的记录类型利用 python 字典生成日志

§ 参数：

□ Main_tag：该图表总的名称

□ Tag_scalar_dict：各类值的字典（如下）

![](TensorboardX%E8%AE%AD%E7%BB%83%E5%8F%AF%E8%A7%86%E5%8C%96/%E5%9B%BE6.png#alt=%E5%9B%BE6)

□ Global_step：存放当前 epoch 值

□ walltime：默认值 time.time()，记录当下时间，一般填 None 不用

§ 用法：如 writer.add_scalars()

○ （graph）网络结构/运行图

§ 参数：

□ model：待可视化的网络模型

□ Input_to_model：输入的一组真图片或者伪造的零值图片

§ 用法：

□ 首先使用 torch.randn(num,z,x,y)生成假数据，然后正常调用模型并切换至 train 状态

![](TensorboardX%E8%AE%AD%E7%BB%83%E5%8F%AF%E8%A7%86%E5%8C%96/%E5%9B%BE7.png#alt=%E5%9B%BE7)

□ 然后使用 with 语句生成 SummaryWriter 实例并添加运行图

![](TensorboardX%E8%AE%AD%E7%BB%83%E5%8F%AF%E8%A7%86%E5%8C%96/%E5%9B%BE8.png#alt=%E5%9B%BE8)

□ 当下文件夹目录会生成 runs 文件夹，这个文件路径为日志地址

![](TensorboardX%E8%AE%AD%E7%BB%83%E5%8F%AF%E8%A7%86%E5%8C%96/%E5%9B%BE9.gif#alt=%E5%9B%BE9)

• 其他记录类型：

• 一些问题

○ 如果执行 add 操作后没有实时在网页可视化界面看到效果，试试重启 tensorboard
