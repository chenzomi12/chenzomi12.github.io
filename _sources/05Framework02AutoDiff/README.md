<!--Copyright © ZOMI 适用于[License](https://github.com/chenzomi12/AISystem)版权许可-->

# 自动微分(DONE)

《自动微分》AI 框架会默认提供自动微分功能，避免用户手动地去对神经网络模型求导，这些复杂的工作交给 AI 框架就好了，于是自动微自然成为分作为 AI 框架的核心功能。

本节自动微分系列将会大概初步谈了谈从手动微分到自动微分的过程，03 自动微分正反模式中深入了自动微分的正反向模式具体公式和推导。实际上 02 了解到正反向模式只是自动微分的原理模式，在实际代码实现的过程，04 会通过三种实现方式（基于库、操作符重载、源码转换）来实现。05 和 06 则是具体跟大家一起手把手实现一个类似于 PyTorch 的自动微分框架。07 最后做个小小的总结，一起 review 自动微分面临易用性、性能的挑战，最后在可微分编程方面畅享了下未来。

> 希望这个系列能够给大家、朋友们带来一些些帮助，也希望自己能够继续坚持完成所有内容哈！

**内容大纲**

> `PPT`和`字幕`需要到 [Github](https://github.com/chenzomi12/AISystem) 下载，网页课程版链接会失效哦~
> 
> 建议优先下载 PDF 版本，PPT 版本会因为字体缺失等原因导致版本很丑哦~

| 小节                | 链接                                                                                                                             |
|:-----------------:|:------------------------------------------------------------------------------------------------------------------------------:|
| 01 基本介绍           | [文章](./01Introduction.md), [PPT](./01Introduction.pdf), [视频](https://www.bilibili.com/video/BV1FV4y1T7zp/), [字幕](./srt/01.srt) |
| 02 什么是微分          | [文章](./02BaseConcept.md), [PPT](./02BaseConcept.pdf), [视频](https://www.bilibili.com/video/BV1Ld4y1M7GJ/), [字幕](./srt/02.srt)   |
| 03 正反向计算模式        | [文章](./03GradMode.md), [PPT](./03GradMode.pdf), [视频](https://www.bilibili.com/video/BV1zD4y117bL/), [字幕](./srt/03.srt)         |
| 04 三种实现方法         | [文章](./04Implement.md), [PPT](./04Implement.pdf), [视频](https://www.bilibili.com/video/BV1BN4y1P76t/), [字幕](./srt/04.srt)       |
| 05 手把手实现正向微分框架    | [文章](./05ForwardMode.md), [视频](https://www.bilibili.com/video/BV1Ne4y1p7WU/), [字幕](./srt/05.srt)                               |
| 06 亲自实现一个 PyTorch | [文章](./06ReversedMode.md), [视频](https://www.bilibili.com/video/BV1ae4y1z7E6/), [字幕](./srt/06.srt)                              |
| 07 自动微分的挑战&未来     | [文章](./07Challenge.md), [PPT](./07Challenge.pdf), [视频](https://www.bilibili.com/video/BV17e4y1z73W/), [字幕](./srt/07.srt)       |

## 备注

文字课程内容正在一节节补充更新，每晚会抽空继续更新正在 [AISys](https://chenzomi12.github.io/) ，希望您多多鼓励和参与进来！！！

文字课程开源在 [AISys](https://chenzomi12.github.io/)，系列视频托管[B 站](https://space.bilibili.com/517221395)和[油管](https://www.youtube.com/@ZOMI666/videos)，PPT 开源在[github](https://github.com/chenzomi12/AISystem)，欢迎取用！！！

> 非常希望您也参与到这个开源项目中，B 站给 ZOMI 留言哦！
> 
> 欢迎大家使用的过程中发现 bug 或者勘误直接提交代码 PR 到开源社区哦！
> 
> 希望这个系列能够给大家、朋友们带来一些些帮助，也希望自己能够继续坚持完成所有内容哈！

```{toctree}
01Introduction
02BaseConcept
03GradMode
04Implement
05ForwardMode
06ReversedMode
07Challenge
```