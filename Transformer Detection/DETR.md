# Transformer+Detection：引入视觉领域的首创DETR

### 论文名称：End-to-End Object Detection with Transformers


### 3.1 DETR原理分析：


本文的任务是Object detection，用到的工具是Transformers，特点是End-to-end。


目标检测的任务是要去预测一系列的Bounding Box的坐标以及Label， 现代大多数检测器通过定义一些`proposal`，`anchor`或者`windows`，把问题构建成为一个`分类`和`回归`问题来间接地完成这个任务。文章所做的工作，就是将transformers运用到了object detection领域，取代了现在的模型需要手工设计的工作，并且取得了不错的结果。在object detection上DETR准确率和运行时间上和Faster RCNN相当；将模型 generalize 到 panoptic segmentation 任务上，DETR表现甚至还超过了其他的baseline。

DETR第一个使用End to End的方式解决检测问题，解决的方法是把**检测问题**视作是一个`set prediction problem`，如下图所示。



网络的主要组成是CNN和Transformer，Transformer借助第1节讲到的self-attention机制，可以显式地对一个序列中的所有elements两两之间的interactions进行建模，使得这类transformer的结构非常适合带约束的set prediction的问题。DETR的特点是：一次预测，端到端训练，set loss function和二分匹配