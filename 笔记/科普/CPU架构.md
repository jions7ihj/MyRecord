# CPU架构

最近接近白漂了两年阿里的 ECS，但是暂时还没想起怎么用，“以针会友”？蜜罐爽歪歪？

最后觉定做一个内网穿透吧，也就这个比较实用了；

PS：没有免费的快照真的不想太折腾......

然后我看到了这个：

那么问题来了，我应该下载哪一个呢？根据我的直觉，选择了 amd64，事实证明是对的。

## x86系列

amd 和 Intel 这俩公司的渊源很深，早期时 Intel 先是自己搞了个 **x86 架构**，然后 amd 拿到了 x86 的授权也可以自己做 x86 了。

接着 intel 向 64 位过渡的时候自己搞了个 ia64（x64 架构）但是因为和 x86 架构不兼容市场反应极差，amd 率先搞了 x86 的 64 位兼容（32 和 64 的混合架构）也就是后来的 `x86_64`，后来 Intel 也拿到了生产这货的授权（两家专利交叉的很严重），也搞了 x86_64，因为 amd 先搞出来的所以 x86_64 也叫 amd64。

> AMD 也是个芯片公司，主业除了设计 CPU（AMD 不流片，所以没有制造）还有设计显卡（收购的 ATI），AMD 设计的 CPU 和 intel x86/x86_64 系列兼容。
>
> 苹果公司和 RPM 包管理员以 “x86-64” 或 “x86_64” 称呼此 64 位架构。
> 甲骨文公司及 Microsoft 称之为 “x64”。
> BSD 家族及其他 Linux 发行版则使用 “amd64”，32 位版本则称为 “i386”（或 i486/586/686）。
> Arch Linux 用 x86_64 称呼此 64 位架构。

参考：[知乎](https://www.zhihu.com/question/63627218)

## arm和mips

这两个和 x86 的区别和联系要从 cpu 早期说起，早期的 cpu 有两个设计思路：

1. 把 CPU 内的逻辑电路做的非常复杂，这样可以直接用 CPU 硬件实现复杂指令，这个叫复杂指令集 cisc；
2. 另一个思路是尽可能把 CPU 做的简单，依靠简单指令的组合迭代完成复杂指令，这个叫精简指令集 risc

x86 目前泛指 x86 和 x86_64 架构，这是因为 x86_64 完全兼容 x86。早期的 x86 是复杂指令集（cisc）的代表，后来的发展中逐步引入了 risc 的部分理念，将内部指令的实现大量模块化，准确来说是一个 cisc 外加 risc 部分技术的架构。

目前 x86 的主要产品有 Intel 的至强，酷睿，奔腾，赛扬和凌动；amd 的锐龙，apu 等。

到目前为止 intel 和 amd 的 x86 架构 cpu 虽然指令集上有很大差别了但是还是相互兼容的，所以软件可以直接用。

---

再说 arm，arm 是精简指令集（risc）的典型代表，不过在 arm 的发展过程中引入了部分复杂指令（完全没有复杂指令的话操作系统跑起来异常艰难），所以是一个 risc 基础外加 cisc 技术的 cpu，指令集和 Intel/amd 不兼容。

因为其便宜与功耗低，虽然计算力不如 x86 系列，但这特性让其称为了手机 CPU 的霸主地位，基本所有的手机 CPU 都是 arm 架构。

arm 的主要专利技术在 arm 公司手中，像高通，三星，苹果这些公司需要拿到 arm 的授权。

---

另一个 risc 的典型处理器就是 mips。mips 是一个学院派的 cpu，授权门槛极低，因此很多厂家都做 mips 或者 mips 衍生架构。我们平时接触到的 mips 架构 cpu 主要用在嵌入式领域，比如路由器。

目前最活跃的 mips 是中国的龙芯，其 loongisa 架构其实是 mips 的扩展。

目前无论 mips 还是 arm，性能和主流 x86 差距都很大，不过 arm 贵在便宜低功耗，mips 则纯计算能力很强（学院派的东西貌似都这样）

---

除了上述几家，还有 power cpu（risc 的，老苹果用的就是这货，索尼家的 PS3 用的好像也是这货，难破解的一大原因）；alpha 架构的 cpu（侧重超算，目前貌似最活跃是中国申威）