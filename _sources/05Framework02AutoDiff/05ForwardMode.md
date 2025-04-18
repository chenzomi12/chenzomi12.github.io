<!--适用于[License](https://github.com/chenzomi12/AISystem/blob/main/LICENSE)版权许可-->

# 动手实现自动微分

在这节内容，会介绍是怎么实现自动微分的，因为代码量非常小，也许你也可以写一个玩玩。前面的章节当中，已经把自动微分的原理深入浅出的讲了一下，也引用了非常多的论文。有兴趣的可以顺着综述 A survey 这篇深扒一下。

## 前向自动微分原理

了解自动微分的不同实现方式非常有用。在这里呢，我们将介绍主要的前向自动微分，通过 Python 这个高级语言来实现操作符重载。在正反向模式中的这篇的文章中，我们介绍了前向自动微分的基本数学原理。

> 前向模式（Forward Automatic Differentiation，也叫做 tangent mode AD）或者前向累积梯度（前向模式）

前向自动微分中，从计算图的起点开始，沿着计算图边的方向依次向前计算，最终到达计算图的终点。它根据自变量的值计算出计算图中每个节点的值以及其导数值，并保留中间结果。一直得到整个函数的值和其导数值。整个过程对应于一元复合函数求导时从最内层逐步向外层求导。

![](../images/05Framework02AutoDiff/05ForwardMode01.png)

简单确实简单，可以总结前向自动微分关键步骤为：

- 分解程序为一系列已知微分规则的基础表达式的组合
- 根据已知微分规则给出各基础表达式的微分结果
- 根据基础表达式间的数据依赖关系，使用链式法则将微分结果组合完成程序的微分结果

而通过 Python 高级语言，进行操作符重载后的关键步骤其实也相类似：

- 分解程序为一系列已知微分规则的基础表达式组合，并使用高级语言的重载操作
- 在重载运算操作的过程中，根据已知微分规则给出各基础表达式的微分结果
- 根据基础表达式间的数据依赖关系，使用链式法则将微分结果组合完成程序的微分结果

## 具体实现

首先呢，我们需要加载通用的 numpy 库，用于实际运算的，如果不用 numpy，在 python 中也可以使用 math 来代替。

```python
import numpy as np
```

前向自动微分又叫做 tangent mode AD，所以我们准备一个叫做 ADTangent 的类，这类初始化的时候有两个参数，一个是 x，表示输入具体的数值；另外一个是 dx，表示经过对自变量 x 求导后的值。

需要注意的是，操作符重载自动微分不像源码转换可以给出求导的公式，一般而言并不会给出求导公式，而是直接给出最后的求导值，所以就会有 dx 的出现。

```python
class ADTangent:

    # 自变量 x，对自变量进行求导得到的 dx
    def __init__(self, x, dx):
        self.x = x
        self.dx = dx

    # 重载 str 是为了方便打印的时候，看到输入的值和求导后的值
    def __str__(self):
        context = f'value:{self.x:.4f}, grad:{self.dx}'
        return context
```

下面是核心代码，也就是操作符重载的内容，在 ADTangent 类中通过 Python 私有函数重载加号，首先检查输入的变量 other 是否属于 ADTangent，如果是那么则把两者的自变量 x 进行相加。

其中值得注意的就是 dx 的计算，因为是正向自动微分，因此每一个前向的计算都会有对应的反向求导计算。求导的过程是这个程序的核心，不过不用担心的是这都是最基础的求导法则。最后返回自身的对象 ADTangent(x, dx)。

```python
    def __add__(self, other):
        if isinstance(other, ADTangent):
            x = self.x + other.x
            dx = self.dx + other.dx
        elif isinstance(other, float):
            x = self.x + other
            dx = self.dx
        else:
            return NotImplementedError
        return ADTangent(x, dx)
```

下面则是对减号、乘法、log、sin 几个操作进行操作符重载，正向的重载的过程比较简单，基本都是按照上面的 __add__ 的代码讨论来实现。

```python
    def __sub__(self, other):
        if isinstance(other, ADTangent):
            x = self.x - other.x
            dx = self.dx - other.dx
        elif isinstance(other, float):
            x = self.x - other
            ex = self.dx
        else:
            return NotImplementedError
        return ADTangent(x, dx)

    def __mul__(self, other):
        if isinstance(other, ADTangent):
            x = self.x * other.x
            dx = self.x * other.dx + self.dx * other.x
        elif isinstance(other, float):
            x = self.x * other
            dx = self.dx * other
        else:
            return NotImplementedError
        return ADTangent(x, dx)

    def log(self):
        x = np.log(self.x)
        dx = 1 / self.x * self.dx
        return ADTangent(x, dx)

    def sin(self):
        x = np.sin(self.x)
        dx = self.dx * np.cos(self.x)
        return ADTangent(x, dx)
```

以公式为例：

$$ f(x1,x2)=ln(x1)+x1x2−sin(x2) $$

因为是基于 ADTangent 类进行了操作符重载，因此在初始化自变量 x 和 y 的值需要使用 ADTangent 来初始化，然后通过代码 f = ADTangent.log(x) + x * y - ADTangent.sin(y) 来实现。

由于这里是求 f 关于自变量 x 的导数，因此初始化数据的时候呢，自变量 x 的 dx 设置为 1，而自变量 y 的 dx 设置为 0。

```python
x = ADTangent(x=2., dx=1)
y = ADTangent(x=5., dx=0)
f = ADTangent.log(x) + x * y - ADTangent.sin(y)
print(f)
```

```text
    value:11.6521, grad:5.5
```

从输出结果来看，正向计算的输出结果是跟上面图相同，而反向的导数求导结果也与上图相同。下面一个是 Pytroch 的实现结果对比，最后是 MindSpore 的实现结果对比。

可以看到呢，上面的简单实现的自动微分结果和 Pytroch 、MindSpore 是相同的。还是很有意思的。

Pytroch 对公式 1 的自动微分结果：

```python
import torch
from torch.autograd import Variable

x = Variable(torch.Tensor([2.]), requires_grad=True)
y = Variable(torch.Tensor([5.]), requires_grad=True)
f = torch.log(x) + x * y - torch.sin(y)
f.backward()

print(f)
print(x.grad)
print(y.grad)
```

输出结果：

```text
    tensor([11.6521], grad_fn=<SubBackward0>)
    tensor([5.5000])
    tensor([1.7163])
```

MindSpore 对公式 1 的自动微分结果：

```python
import numpy as np
import mindspore.nn as nn
from mindspore import Parameter, Tensor

class Fun(nn.Cell):
    def __init__(self):
        super(Fun, self).__init__()

    def construct(self, x, y):
        f = ops.log(x) + x * y - ops.sin(y)
        return f

x = Tensor(np.array([2.], np.float32))
y = Tensor(np.array([5.], np.float32))
f = Fun()(x, y)

grad_all = ops.GradOperation()
grad = grad_all(Fun())(x, y)

print(f)
print(grad[0])
```

输出结果：

```text
    [11.65207]
    5.5
```

## 小结与思考

- 介绍了前向自动微分（Forward Automatic Differentiation, FAD）的实现原理和过程，通过 Python 语言的操作符重载技术，创建了 ADTangent 类来自动计算导数，并通过实例代码演示了如何使用该类来计算给定函数的导数。

- 通过具体的 Python 代码示例，展示了如何利用 ADTangent 类进行操作符重载，实现正向自动微分，并与 PyTorch 和 MindSpore 等 AI 框架的自动微分结果进行了对比，验证了实现的正确性。

## 本节视频

<html>
<iframe src="https://player.bilibili.com/player.html?aid=646165538&bvid=BV1Ne4y1p7WU&cid=909293015&page=1&as_wide=1&high_quality=1&danmaku=0&t=30&autoplay=0" width="100%" height="500" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
</html>