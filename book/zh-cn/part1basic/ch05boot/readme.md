---
weight: 1500
title: "第 5 章 Go 程序生命周期"
---

# 第 5 章 Go 程序生命周期

- [5.1 Go 程序引导](./boot.md)
    + 入口
    + 引导
      + 步骤1: runtime.check
      + 步骤2: runtime.args
      + 步骤3: runtime.osinit
      + 步骤4: runtime.schedinit
      + 步骤5: runtime.newproc
      + 步骤6: runtime.mstart
    + 小结
    + 进一步阅读的参考文献
- [5.2 运行时初始化概览](./init.md)
    + CPU 相关信息的初始化
    + 运行时算法初始化
    + 模块链接初始化
    + 核心组件的初始化
    + 小结
- [5.3 主 goroutine 的生与死](./main.md)
    + 概览
    + pkg.init 顺序
    + 何去何从？

## 许可

[Go under the hood](https://github.com/changkun/go-under-the-hood) | CC-BY-NC-ND 4.0 & MIT &copy; [changkun](https://changkun.de)
