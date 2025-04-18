<!--适用于[License] (https://github.com/chenzomi12/AISystem/blob/main/LICENSE)版权许可-->

# 内容介绍

什么是 AI 算法？什么是神经网络？神经网络有什么用？为什么神经网络需要训练？什么是模型？AI 框架有什么用？AI 框架能解决什么问题？

上面的几个问题其实还挺有挑战的，也是本节需要回答的一个问题。下面来对一些基础概念进程澄清：首先深度学习是机器学习研究领域中的一种范式，而深度学习的概念源于对人工神经网络的研究，很多深度学习算法都使用神经网络进行表示，因为神经网络的性能精度和通用效果都非常好，于是业界习惯性地把深度学习算法等同于 AI。

![ AI 发展路线](../images/05Framework01Foundation/01Introduction01.png)

## AI 框架基础介绍

在 AI 框架基础系列里面，将会先介绍神经网络和深度学习的基本概念，了解深度学习、神经网络、 AI 多个新名词和新概念之间的种种关联关系。简单而言，而深度学习是通过函数逼近来解析神经网络的数学原理，通过反向求导算法来求解神经网络中参数的偏导，从而迭代地求解神经网络中的最优值。不过上面的叙述还是有点难以理解复杂的数学原理，因此在 AI 框架作用中的深度学习基础，将会深入浅出地介绍介绍深度学习的基础。

有了深度学习的基础之后，就能够比较好地理解 AI 框架的实际作用，即作为 AI 算法（深度学习算法）的模型设计、训练和验证的一套标准接口、特性库和工具包，集成了算法的封装、数据的调用以及计算资源的使用，同时面向开发者提供了开发界面和高效的执行平台，是现阶段 AI 算法开发的必备工具。

有了对深度学习的认识、对 AI 框架作用的认识，自然就理解 AI 框架的目的和为什么目前国内厂商，无论是华为昇腾构建 MindSpore、百度打造飞桨 PaddlePaddle、之江实验室联合一流科技开发的 OneFlow，包括商汤、旷视都推出自己的自研 AI 框架了。

可是 AI 的框架发展并不顺利，从萌芽阶段（2000 年初期）、 成长阶段（2012~2014 年）、稳定阶段（2015 年~2019 年）、深化阶段（2020 年以后）。其发展脉络与 AI ，特别是神经网络技术的异峰突起有非常紧密的联系。中间又经历了三代框架，这里面提到的 AI 框架三代并不是以时间为维度，更多的是以技术为区分维度，通过不同的技术手段走过三代技术框架，从而使得 AI 框架慢慢走向成熟。

截至目前为止，国际主流的 AI 框架（PyTorch、TensorFlow 等）基本均已经实现动态图开发、静态图部署的编程范式，具备动静态图转换的能力，不过基于开发效率考虑，动态图与静态图的转换与统一需要持续迭代优化。

上面提到的编程范式主要是跟开发者的编程习惯和编程方式息息相关。实际上，编程范型、编程范式或程式设计法（Programming paradigm），是指软件工程中的一类典型的编程风格。

常见的编程范型有：函数式编程、指令式编程、过程式编程、面向对象编程等等。编程范型提供并决定了程序员对程序执行的看法，而 AI 框架的编程范式目前主要集中在声明式编程与命令式编程两种之间。

## 小结与思考

- 了解国内产商自研 AI 框架的意义和 AI 框架具体作用

- 了解 AI 框架框架的发展历史和技术带给行业的 AI 快乐

- 了解了程序员天天为之吵架的编程范式

## 本节视频

<html>
<iframe src="https://player.bilibili.com/player.html?aid=558671844&bvid=BV1he4y1z7oD&cid=911380319&page=1&as_wide=1&high_quality=1&danmaku=0&t=30&autoplay=0" width="100%" height="500" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
</html>
