## 目录

### [引言](preface.md)

### [第一部分: 基础知识](part1basic/readme.md)

#### [第 1 章 程序基础](part1basic/ch01proc/readme.md)

- [1.1 Go 语言综述](./part1basic/ch01proc/go.md)
- [1.2 传统程序堆栈](./part1basic/ch01proc/stack.md)
- [1.3 系统内核与系统调用](./part1basic/ch01proc/os.md)
- [1.4 Plan 9 汇编语言](./part1basic/ch01proc/asm.md)
- [1.5 CPU 设计与架构](./part1basic/ch01proc/cpu.md)
- [1.6 编译与链接](./part1basic/ch01proc/compile.md)

#### [第 2 章 并行、并发与分布式计算](part1basic/ch02parallel/readme.md)

- [2.1 并行与并发的基本概念](part1basic/ch02parallel/define.md)
- [2.2 缓存技术](part1basic/ch02parallel/cache.md)
    + UMA
    + NUMA
    + 一致性协议
    + 真假共享
- [2.3 性能模型](part1basic/ch02parallel/perfs.md)
- [2.4 分布式计算的基本概念](part1basic/ch02parallel/distributed.md)
- [2.5 共识技术](part1basic/ch02parallel/consensus.md)
- [2.6 顺序进程通讯 CSP](part1basic/ch02parallel/csp.md)
- [2.7 同步锁](part1basic/ch02parallel/locks.md)

#### [第 3 章 排队与调度理论](part1basic/ch03scheduling/readme.md)

- [3.1 排队理论](part1basic/ch03scheduling/queue.md)
- [3.2 单机调度模型](part1basic/ch03scheduling/single.md)
- [3.3 随机调度模型](part1basic/ch03scheduling/stochastic.md)
- [3.4 工作窃取调度理论](part1basic/ch03scheduling/theory.md)
- [3.5 中断与抢占](part1basic/ch03scheduling/interrupt.md)

#### [第 4 章 内存管理工程](part1basic/ch04memory/readme.md)

- [4.1 内存分配器](part1basic/ch04memory/alloc.md)
- [4.2 标记清扫法与三色抽象](part1basic/ch04memory/cms.md)
- [4.3 屏障技术](part1basic/ch04memory/barrier.md)
    + 三色不变性原理
      + 强、弱不变性
      + 赋值器的颜色
      + 新分配对象的颜色
    + 赋值器屏障技术
      + 灰色赋值器的 Dijkstra 插入屏障
      + 黑色赋值器的 Yuasa 删除屏障
    + 进一步阅读的参考文献
- [4.4 垃圾回收统一理论](part1basic/ch04memory/unifiedgc.md)

#### [第 5 章 Go 程序生命周期](part1basic/ch05boot/readme.md)

- [5.1 Go 程序引导](part1basic/ch05boot/boot.md)
    + 入口
    + 引导
    + 小结
    + 进一步阅读的参考文献
- [5.2 运行时初始化概览](part1basic/ch05boot/init.md)
    + CPU 相关信息的初始化
    + 运行时算法初始化
    + 模块链接初始化
    + 核心组件的初始化
    + 小结
- [5.3 主 goroutine 的生与死](part1basic/ch05boot/main.md)
    + 概览
    + pkg.init 顺序
    + 何去何从？

### [第二部分：运行时机制](part2runtime/readme.md)

#### [第 6 章 调度器](part2runtime/ch06sched/readme.md)

- [6.1 基本结构](part2runtime/ch06sched/basic.md)
    + 工作线程的暂止和复始
    + 主要结构
      + M 的结构
      + P 的结构
      + G 的结构
      + 调度器 sched 的结构
    + 小结
    + 进一步阅读的参考文献
- [6.2 调度器初始化](part2runtime/ch06sched/init.md)
    + M 的初始化
    + P 的初始化
    + G 的初始化
      + 一些细节
    + 小结
- [6.3 调度循环](part2runtime/ch06sched/exec.md)
    + 执行前的准备
      + mstart 和 mstart1
      + M 与 P 的绑定
      + M 的暂止和复始
    + 核心调度
      + 偷取工作
      + M 的唤醒
      + M 的创生
        + 系统线程的创建 (darwin)
        + 系统线程的创建 (linux)
      + M/G 解绑
      + M 的死亡
    + 小结
    + 进一步阅读的参考文献
- [6.4 线程管理](part2runtime/ch06sched/thread.md)
    + LockOSThread
    + UnlockOSThread
    + lockedg/lockedm 与调度循环
    + 模板线程
    + 小结
    + 进一步阅读的参考文献
- [6.5 信号处理机制](part2runtime/ch06sched/signal.md)
    + 信号与软中断
    + 初始化
    + 获取原始信号屏蔽字
    + 初始化信号栈
    + 初始化信号屏蔽字
    + 信号处理
    + Extra M
    + 小结
    + 进一步阅读的参考文献
- [6.6 执行栈管理](part2runtime/ch06sched/stack.md)
    + goroutine 栈结构
    + 执行栈初始化
    + G 的创生
    + 执行栈的分配
      + 小栈分配
      + 大栈分配
      + 堆上分配
    + 执行栈的伸缩
      + 分段标记
      + 栈的扩张
      + 栈的拷贝
      + 栈的收缩
    + 小结
- [6.7 协作与抢占](part2runtime/ch06sched/preemption.md)
    + 协作式调度
      + 主动用户让权: Gosched
      + 主动调度弃权: 栈扩张与抢占标记
      + 被动监控弃权: 阻塞监控
    + 抢占式调度
    + 小结
    + 进一步阅读的参考文献
- [6.8 运行时同步原语](part2runtime/ch06sched/sync.md)
    + 运行时通知机制 note
      + 结构
      + 注册通知
      + 发送通知
      + 清除通知
    + 运行时互斥量机制 mutex
      + 结构
      + lock
      + unlock
    + 运行时信号量机制 semaphore
      + sudog 缓存
      + 基于 goroutine 抽象的信号量
    + 小结
    + 进一步阅读的参考文献
- [6.9 系统监控](part2runtime/ch06sched/sysmon.md)
    + 监控循环
    + 小结
- [6.10 网络轮询器](part2runtime/ch06sched/poller.md)
- [6.11 计时器](part2runtime/ch06sched/timer.md)
    + Timer 状态机
      + Timer 的启动
      + Timer 的终止
      + Timer 的重置
      + Timer 的执行
    + Timer 的触发时机
      + 从调度循环中直接触发
      + 从系统监控中触发
    + 小结
    + 进一步阅读的参考文献
- [6.12 用户层 APIs](part2runtime/ch06sched/calls.md)
- [6.13 过去、现在与未来](part2runtime/ch06sched/history.md)
    + 演进史
      + 单线程版调度器
      + 多线程版调度器
      + 工作窃取调度器
    + 改进展望：非均匀访存感知的调度器设计
    + 小结
    + 进一步阅读的参考文献

#### [第 7 章 内存分配器](part2runtime/ch07alloc/readme.md)

- [7.1 基本知识](part2runtime/ch07alloc/basic.md)
    + 主要结构
    + Arena
      + heapArena
      + arenaHint
    + mspan
    + mcache
    + mcentral
    + mheap
    + 分配概览
    + 分配入口
      + 小对象分配
      + 微对象分配
      + 大对象分配
    + 小结
    + 进一步阅读的参考文献
- [7.2 组件](part2runtime/ch07alloc/component.md)
    + fixalloc
      + 结构
      + 初始化
      + 分配
      + 回收
    + linearAlloc
    + mcache
      + 分配
      + 释放
      + per-P? per-M?
    + 其他
      + memclrNoHeapPointers
    + 系统级内存管理调用
- [7.3 初始化](part2runtime/ch07alloc/init.md)
- [7.4 大对象分配](part2runtime/ch07alloc/largealloc.md)
    + 从堆上分配
    + 从操作系统申请
- [7.5 小对象分配](part2runtime/ch07alloc/smallalloc.md)
    + 从 mcache 获取
    + 从 mecentral 获取
    + 从 mheap 获取
- [7.6 微对象分配](part2runtime/ch07alloc/tinyalloc.md)
- [7.7 清道夫及其调步算法](part2runtime/ch08GC/scavenge.md)
- [7.8 内存统计](part2runtime/ch07alloc/mstats.md)
- [7.9 过去、现在与未来](part2runtime/ch07alloc/history.md)

#### [第 8 章 垃圾回收器](part2runtime/ch08GC/readme.md)

- [8.1 基本知识](part2runtime/ch08GC/basic.md)
    + 并发三色回收一瞥
    + 原始的标记清扫算法
    + 内存模型
    + 进一步阅读的参考文献
- [8.2 混合写屏障](part2runtime/ch08GC/barrier.md)
    + 基本思想
    + 可靠性、完备性和有界性的证明
    + 实现细节
    + 小结
    + 进一步阅读的参考文献
- [8.3 并发标记清扫](part2runtime/ch08GC/concurrent.md)
    + 并发标记
    + 并发清扫
    + 并行三色标记
    + 进一步阅读的参考文献
- [8.4 初始化](part2runtime/ch08GC/init.md)
    + 引导阶段的 GC 初始化
    + GC 的后台工作
- [8.5 触发机制及其调步算法](part2runtime/ch08GC/pacing.md)
    + GC 的调控方式
    + 调步算法的设计
    + 实现
- [8.6 GC 周期概述](part2runtime/ch08GC/cycle.md)
    + GC 周期的不同阶段
    + STW 的启动
    + STW 的结束
    + GC 的启动
    + 标记准备阶段
- [8.7 扫描标记与标记辅助](part2runtime/ch08GC/mark.md)
- [8.8 标记终止阶段](part2runtime/ch08GC/termination.md)
- [8.9 内存清扫阶段](part2runtime/ch08GC/sweep.md)
- [8.10 用户层 APIs](part2runtime/ch08GC/finalizer.md)
    + 存活与终结
      + SetFinalizer
      + KeepAlive
- [8.11 过去、现在与未来](part2runtime/ch08GC/history.md)

#### [第 9 章 调试工具](part2runtime/ch09debug/readme.md)

- [9.1 数据竞争检测](part2runtime/ch09debug/race.md)
- [9.2 运行时死锁检测](part2runtime/ch09debug/deadlock.md)
- [9.3 trace 运行时调试](part2runtime/ch09debug/trace.md)

#### [第 10 章 兼容与契约](part2runtime/ch10abi/readme.md)

- [10.1 参与运行时的系统调用](part2runtime/ch10abi/syscall.md)
    + Linux
      + 案例研究 runtime.clone
      + 运行时实现的系统调用清单
    + Darwin
      + libcCall 调用
      + 案例研究: runtime.pthread_create
      + 运行时实现的 libc 调用清单
    + 进一步阅读的参考文献
- [10.2 cgo](part2runtime/ch10abi/cgo.md)
    + 入口
    + cgocall
      + Go 调用 C
      + 实际代码
    + cgocallbackg
      + C 调用 Go
      + 实际代码
    + 小结
    + 进一步阅读的参考文献
- [10.3 WebAssembly](part2runtime/ch10abi/wasm.md)
- [10.4 用户态系统调用](part2runtime/ch10abi/syscall-pkg.md)
    + 由运行时提供支持的系统调用
    + 通用型系统调用
    + `runtime.entersyscall` 和 `runtime.exitsyscall`
    + 返回的错误处理
    + 进一步阅读的参考文献

#### [第 11 章 关键字与类型系统](part2runtime/ch11type/readme.md)

- [11.1 `go`](part2runtime/ch11type/go.md)
- [11.2 `defer`](part2runtime/ch11type/defer.md)
- [11.3 `panic` 与 `recover`](part2runtime/ch11type/panic.md)
    + gopanic 和 gorecover
    + 小结
- [11.4 `map`](part2runtime/ch11type/map.md)
- [11.5 `chan` 与 `select`](part2runtime/ch11type/chan.md)
    + channel 的本质
      + 基本使用
      + channel 的创生
      + 向 channel 发送数据
      + 从 channel 接收数据
      + channel 的死亡
    + select 的本质
      + 随机化分支
      + 发送数据的分支
      + 接收数据的分支
    + channel 的 lock-free 实现
    + 小结
    + 进一步阅读的参考文献
- [11.6 `interface{}`](part2runtime/ch11type/interface.md)
- [11.7 slice](part2runtime/ch11type/slice.md)
- [11.8 string](part2runtime/ch11type/string.md)
- [11.9 运行时类型系统与 reflect 包](part2runtime/ch11type/type.md)

### [第三部分：编译系统](part3compile/readme.md)

#### [第 12 章 泛型](part3compile/ch12generics/readme.md)

- [12.1 泛型的历史及其演化](part3compile/ch12generics/history.md)
- [12.2 泛型的实现](part3compile/ch12generics/implement.md)
- [12.3 泛型的未来？](part3compile/ch12generics/future.md)

#### [第 13 章 编译器](part3compile/ch13gc/readme.md)

- [13.1 unsafe](part3compile/ch13gc/unsafe.md)
    + 任意类型 `ArbitraryType`
    + Go 指针 `Pointer`
    + 指针操作
- [13.2 逃逸分析](part3compile/ch13gc/escape.md)
- [13.3 词法与文法](part3compile/ch13gc/parse.md)
- [13.4 编译后端 SSA](part3compile/ch13gc/ssa.md)
- [13.5 语言的自举](part3compile/ch13gc/bootstrap.md)
- [13.6 过去、现在与未来](part3compile/ch13gc/future.md)

#### [第 14 章 链接器](part3compile/ch14linker/readme.md)

- [14.1 初始化](part3compile/ch14linker/init.md)
- [14.2 模块链接](part3compile/ch14linker/link.md)
- [14.3 目标文件](part3compile/ch14linker/obj.md)

### [第四部分：标准库](part4lib/readme.md)

#### [第 15 章 错误处理](part4lib/ch15errors/readme.md)

- [15.1 错误处理的历史及其演化](part4lib/ch15errors/history.md)
    + `error` 类型的历史形态
    + 错误处理的基本策略
      + 哨兵错误
      + 自定义错误
      + 隐式错误
    + `pkg/errors` 的错误处理原语
    + 争议
      + 对错误处理进行改进的反馈
      + check/handle 关键字
      + 内建函数 try
- [15.2 `errors` 包与错误检查](part4lib/ch15errors/errors.md)
    + 错误检查
      + Unwrap
      + As 与 Is
      + fmt.Errorf 中的 `%w`
- [15.3 错误处理的未来？](part4lib/ch15errors/future.md)

#### [第 16 章 sync 与 atomic 包](part4lib/ch16sync/readme.md)

- [16.1 `sync.Pool`](part4lib/ch16sync/pool.md)
    + 底层结构
    + Get
    + Put
    + 偷取细节
      + pin 和 pinSlow
      + getSlow
    + 缓存的回收
    + poolChain
      + poolChain 的 popHead, pushHead 和 popTail
      + poolDequeue 的 popHead, pushHead popTail
    + noCopy
    + 小结
    + 进一步阅读的参考文献
- [16.2 `sync.Once`](part4lib/ch16sync/once.md)
- [16.3 `sync.Map`](part4lib/ch16sync/map.md)
    + 结构
    + Store
    + Load
    + Delete
    + Range
    + LoadOrStore
    + 小结
- [16.4 `sync.WaitGroup`](part4lib/ch16sync/waitgroup.md)
    + 结构
    + Add/Done
    + Wait
- [16.5 `sync.Mutex` 与 `sync.RWMutex`](part4lib/ch16sync/mutex.md)
- [16.6 `sync.Cond`](part4lib/ch16sync/cond.md)
    + 结构
    + copyChecker
    + Wait/Signal/Broadcast
    + notifyList
- [16.7 `sync/atomic`](part4lib/ch16sync/atomic.md)
    + 公共包方法
      + atomic.Value
      + atomic.CompareAndSwapPointer
    + 运行时实现
    + 原子操作的内存模型
    + 进一步阅读的参考文献

### [结束语：Go 去向何方？](ch17end/readme.md)

### [参考文献](../bibliography/list.md)
### [附录A: 源码索引](appendix/all.md)
### [附录B: 术语表](appendix/glossary.md)