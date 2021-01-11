## 为何卷积

一切对数据科学略有了解的人一定都与这两种数据类型打过交道： 表格数据（tabular data）和图片数据（image data）。它们的定义极为简单直观：

* 表格数据（Tabular data）： 数据由行和列组成，一行代表一个样本（sample），而一列代表一个特征（feature）。
* 图片数据（Image data）: 一个样本（sample）即一张图片，即一个由像素（pixel）排列形成的二维点阵。每一个像素或由1个数字来代表（黑白图像和灰度图像），或由3个数字来代表（RGB图像），甚至由超过3个数据代表（multiplex image）。

直觉上，在数据体量大致相同的情况下，图片数据比表格数据更复杂，蕴藏着更多更深的信息。这一直觉无疑是正确的，原因在于图片数据是像素与像素间的空间排布（spatial structure）的集成，而表格数据不包含任何空间信息。举一个例子：对于1张100*100的灰度图像，我们不但关心这10000个像素点是什么，也关心这10000个像素点的排列结构；我们不但关心每一个像素，还关心它的邻居和社区环境。然而对于一个10000列的表格，我们并不在意列与列之间的排列顺序，不关心某一个特征的前一个或后一个是谁。

在神经网络（NN）诞生以后和卷积神经网络（CNN）诞生以前，我们用对付表格数据的办法来处理图片数据——把一个2维灰度图片拉平为一个1维向量再送入神经网络。（对RGB图片或者更高维的图片的处理没有任何本质的区别，无非是1维向量更长一些罢了。）

这种方法显然缺乏缺乏基本的实操性：想象一个100*100的灰度图片，当它被拉平为1维向量后，每个样本拥有了10000个特征。如果我用矩阵乘法的方式来提取这个图片的特征，我需要一个10000列的矩阵！这是一种极其奢侈的利用计算资源的方式，而且效率甚差。也许对图片预先降维（feature reduction）能够减轻负担，但是我们终究丧失了部分或全部的空间排布信息（spatial structure）。

CNN 诞生了，它用卷积代替矩阵乘法提取特征，将神经网络中的一个或多个全连接层替换为卷积层。卷积完美地解决了空间结构信息（spatial structure）丢失地问题——每一次卷积，都是在集成像素与和它周边像素的信息。

章节链接：https://d2l.ai/chapter_convolutional-neural-networks/index.html

## 何为卷积

#### 连续卷积

卷积（convolution）是对两个函数( <img src="https://www.zhihu.com/equation?tex=f,g" alt="f,g" class="ee_img tr_noresize" eeimg="1"> )的一种操作手段，代号 <img src="https://www.zhihu.com/equation?tex=f*g" alt="f*g" class="ee_img tr_noresize" eeimg="1"> 

<img src="https://www.zhihu.com/equation?tex=(f*g)(x) = \int{f(z)g(x-z)}dz
" alt="(f*g)(x) = \int{f(z)g(x-z)}dz
" class="ee_img tr_noresize" eeimg="1">


