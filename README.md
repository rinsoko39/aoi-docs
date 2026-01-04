# Aoi 文档

这是自创编程语言 Aoi 的文档。欢迎提 issues；作者表达能力有所欠缺，如有可改进的地方或明显错误，欢迎提交 pull requests。

Aoi 是一个静态强类型的运行在 .NET 上的轻量解释型语言。其名字来源于《你和她和她的恋爱。》中的女主向日葵（Mukou Aoi）。

目前 Aoi 还没有解释器，只存在于设想阶段。

Aoi 在设计上有一些创新：不同于面向对象编程，Aoi 没有继承，没有传统意义的特征或接口，但是它仍然具有面向对象的多态等特性。

以下是 Aoi 的 HelloWorld：

```aoi
printLine "Hello, World!";
```

Aoi 的一个显著特点是它没有函数，取而代之的是一元和二元运算符。在调用时，无需像函数一样每次都使用括号将参数围起来。以下是一个计算阶乘例子：

```aoi
op fac x: int -> int {
    if x == 0 then {
        1
    } else {
        fac (x - 1)
    }
}
printLine fac 10;
```

Aoi 没有继承或接口，不过，Aoi 仍然可以通过其中的泛型和特征实现多态，尽管 Aoi 中的特征和 Rust 中的特征以及其它语言中的接口等不太一样。以下是一个示范，它实现了数列求和，并获取了自定义结构体 `Vector` 的和。

```aoi
op sum[T: Add[T]] array: arr[T] -> T {
    let res = array.[0];
    for i in 1..array.length do {
        res += array.[i];
    }
    res
}
struct Vector {
    x: float;
    y: float;
}
impl of Add[Vector] {
    op a + b {
        new Vector {
            x: a.x + b.x,
            y: a.y + b.y
        }
    }
}
let vectors = new arr[Vector] { ... };
printLine sum vectors;
```

可以看出，Aoi 有些地方与其它语言不太相同，这些地方大多是因为水平不足为了减少编译复杂度（例如泛型使用中括号）。

Aoi 也计划支持闭包、迭代器和 async / await 异步。

Aoi 语言将保持简单，因此砍掉了若干设想，并将许多功能使用更为简单但可能更损耗性能的实现。当然，有很大一部分原因是作者能力不足。
