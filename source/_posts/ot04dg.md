---

## title: 损失函数与语义分割任务 date: 2021-08-07 22:29:17

tags: [深度学习, 语义分割]
categories: 计算机视觉特辑

1.基于分布的损失函数，基于区域的损失函数，基于边界的损失函数和基于复合的损失函数（ Distribution-based,Region-based,  Boundary-based,  and  Compounded）
![](%E6%8D%9F%E5%A4%B1%E5%87%BD%E6%95%B0%E4%B8%8E%E8%AF%AD%E4%B9%89%E5%88%86%E5%89%B2%E4%BB%BB%E5%8A%A1/%E5%9B%BE1.png#alt=%E5%9B%BE1)

2.分类标签不平衡问题：

• 道路识别中，数据集拥有的正样本非常少，有时候背景负样本带来很多没必要的损失函数值的参数更新，类似噪声干扰了正样本训练，无论双分类训练还是多分类训练都存在该问题，更不用说多分类任务。

• 解决方案

损失函数本身对训练影响弱于数据集，但是，如果数据集中标签严重不平衡，还是应该选择二进制交叉熵(binary-cross entropy)之外的其他损失函数，如 DiceLoss 系列。

○ 普通 DiceLoss 损失函数

![](%E6%8D%9F%E5%A4%B1%E5%87%BD%E6%95%B0%E4%B8%8E%E8%AF%AD%E4%B9%89%E5%88%86%E5%89%B2%E4%BB%BB%E5%8A%A1/%E5%9B%BE2.png#alt=%E5%9B%BE2)

![](%E6%8D%9F%E5%A4%B1%E5%87%BD%E6%95%B0%E4%B8%8E%E8%AF%AD%E4%B9%89%E5%88%86%E5%89%B2%E4%BB%BB%E5%8A%A1/%E5%9B%BE3.png#alt=%E5%9B%BE3)

上面公式比较通俗，右侧部分称 Dice 系数（dice coefficient），由 1 减去就得到了 DiceLoss。对于分割任务而言，绝对值 X 和 Y 分别代表 ground_truth 和 predict_mask。一般和 IoU 一样作为测试的评价指数，实际训练效果非常糟糕。

○ Log-Cosh Dice Loss

普通 DiceLoss 由于其非凸性，它多次都无法获得最佳结果。Lovsz-softmax 损失旨在通过添加使用 Lovsz 扩展的平滑来解决非凸损失函数的问题。同时，Log-Cosh 方法已广泛用于基于回归的问题中，以平滑曲线。

![](%E6%8D%9F%E5%A4%B1%E5%87%BD%E6%95%B0%E4%B8%8E%E8%AF%AD%E4%B9%89%E5%88%86%E5%89%B2%E4%BB%BB%E5%8A%A1/%E5%9B%BE4.png#alt=%E5%9B%BE4)

但是该损失函数无法在我的项目中运行（ExpLog_Dice）

○ Tversky Loss

![](%E6%8D%9F%E5%A4%B1%E5%87%BD%E6%95%B0%E4%B8%8E%E8%AF%AD%E4%B9%89%E5%88%86%E5%89%B2%E4%BB%BB%E5%8A%A1/%E5%9B%BE5.png#alt=%E5%9B%BE5)

Tversky 系数是 Dice 系数和 Jaccard 系数的一种推广。当设置 α=β=0.5，此时 Tversky 系数就是 Dice 系数。而当设置 α=β=1 时，此时 Tversky 系数就是 Jaccard 系数。α 和 β 分别控制假阴性和假阳性。通过调整 α 和 β，可以控制假阳性和假阴性之间的平衡。

![](%E6%8D%9F%E5%A4%B1%E5%87%BD%E6%95%B0%E4%B8%8E%E8%AF%AD%E4%B9%89%E5%88%86%E5%89%B2%E4%BB%BB%E5%8A%A1/%E5%9B%BE6.png#alt=%E5%9B%BE6)

○ Focal Tversky Loss

![](%E6%8D%9F%E5%A4%B1%E5%87%BD%E6%95%B0%E4%B8%8E%E8%AF%AD%E4%B9%89%E5%88%86%E5%89%B2%E4%BB%BB%E5%8A%A1/%E5%9B%BE7.png#alt=%E5%9B%BE7)

参考文章： Loss Functions for Medical Image Segmentation: A Taxonomy | by JunMa | Medium [https://medium.com/@junma11/loss-functions-for-medical-image-segmentation-a-taxonomy-cefa5292eec0#:~:text=Generalized Dice loss is the multi-class extension of,negatives and false positives in generalized Dice loss](https://medium.com/@junma11/loss-functions-for-medical-image-segmentation-a-taxonomy-cefa5292eec0#:~:text=Generalized%20Dice%20loss%20is%20the%20multi-class%20extension%20of,negatives%20and%20false%20positives%20in%20generalized%20Dice%20loss).

GitHub： GitHub - JunMa11/SegLoss: A collection of loss functions for medical image segmentation [https://github.com/JunMa11/SegLoss](https://github.com/JunMa11/SegLoss)

论文：[https://arxiv.org/pdf/2006.14822.pdf](https://arxiv.org/pdf/2006.14822.pdf)
