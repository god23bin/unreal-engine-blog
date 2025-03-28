---
title: 《计算机组成原理》目录
date: 2024/12/01 12:35:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201718002.jpg
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201718002.jpg
categories:
  - [计算机科学基础,计算机组成原理,初学者入门]
tag:
  - 计算机组成原理
  - 目录
published: true
---
# 《计算机组成原理》初学者入门学习目录

🎉 欢迎来到计算机组成原理的世界！本学习目录旨在引导零基础的你，一步步理解计算机的内部构造和工作方式。让我们一起开始愉快的学习之旅吧！

## 🚀  第一阶段：基础知识预热 (夯实地基)

### 1. 计算机的世界观

*   **1.1 什么是计算机组成原理？**
    *   计算机科学体系结构中的位置
    *   为什么学习计算机组成原理？ (重要性、应用场景)
    *   与 "计算机体系结构"、"计算机操作系统" 等课程的关系
*   **1.2 计算机发展简史**
    *   机械计算机的时代 (巴贝奇差分机等)
    *   电子管计算机的诞生 (ENIAC)
    *   晶体管计算机、集成电路计算机、大规模集成电路计算机
    *   摩尔定律与计算机发展趋势
*   **1.3 计算机系统的层次结构**
    *   硬件与软件的概念
    *   计算机系统的五层结构（从下往上）：
        *   微程序机器层 (实际机器)
        *   传统机器层 (机器语言机器)
        *   操作系统层
        *   汇编语言层
        *   高级语言层
    *   各层次之间的关系与作用

### 2. 数制与编码 (计算机的语言)

*   **2.1 常用数制**
    *   十进制 (Decimal - D)
    *   二进制 (Binary - B) - 重点
    *   八进制 (Octal - O)
    *   十六进制 (Hexadecimal - H)
    *   不同数制之间的转换 (重点和难点)
        *   二进制转十进制、十进制转二进制
        *   二进制转八进制、十六进制，反之亦然 (技巧)
*   **2.2 计算机中的编码**
    *   **数值数据的表示**
        *   机器数与真值
        *   原码、反码、补码、移码 (重点和难点)
            *   正数、负数的表示
            *   不同编码的特点与适用场景
            *   补码运算的优势 (加法、减法统一)
        *   定点数与浮点数
    *   **非数值数据的表示**
        *   字符编码：ASCII 码、Unicode 编码 (了解)
        *   汉字编码：GBK, UTF-8 等 (了解)

## 🛠️ 第二阶段：硬件系统的核心部件 (构建计算机骨架)

### 3. 运算方法与运算器 (计算机的心脏)

*   **3.1 定点数的加法与减法运算**
    *   原码加减法、补码加减法 (重点)
    *   溢出检测与判断 (重点)
        *   上溢、下溢的概念
        *   溢出检测的方法
*   **3.2 定点数的乘法与除法运算 (了解)**
    *   原码乘法、补码乘法 (简单了解思想)
    *   原码除法、补码除法 (简单了解思想)
*   **3.3 浮点数的运算 (了解)**
    *   浮点数的表示形式
    *   浮点数的加减运算步骤 (对阶、尾数运算、规格化、舍入)
*   **3.4 运算器的基本结构**
    *   算术逻辑单元 ALU (核心部件)
    *   累加器 ACC
    *   通用寄存器组
    *   数据缓冲寄存器
    *   状态条件寄存器 PSW

### 4. 存储系统 (数据的仓库)

*   **4.1 存储器的分类**
    *   按存储介质：半导体存储器、磁表面存储器、光存储器
    *   按存取方式：随机存取存储器 RAM、只读存储器 ROM、串行访问存储器
    *   按在计算机中的作用：主存储器、辅助存储器、高速缓冲存储器 Cache
*   **4.2 主存储器**
    *   **半导体存储芯片**
        *   SRAM (静态 RAM)
        *   DRAM (动态 RAM)
        *   ROM 的类型 (MROM, PROM, EPROM, EEPROM, Flash Memory)
    *   **主存储器的基本组成**
        *   存储体
        *   MAR (存储器地址寄存器)
        *   MDR (存储器数据寄存器)
        *   地址译码电路、驱动电路、读写控制电路
    *   **主存储器与 CPU 的连接**
        *   地址线的数量与寻址范围
        *   数据线的数量与数据宽度
        *   控制线的功能 (读/写信号等)
*   **4.3 高速缓冲存储器 (Cache)**
    *   Cache 的作用和原理 (解决 CPU 和主存速度不匹配问题)
    *   Cache 的基本结构
    *   Cache 的地址映射方式 (直接映射、全相联映射、组相联映射) - 了解思想
    *   Cache 的替换算法 (了解)
*   **4.4 辅助存储器 (外存储器)**
    *   磁盘存储器 (硬盘、软盘 - 了解)
    *   固态硬盘 SSD (了解)
    *   光盘存储器 (CD-ROM, DVD-ROM - 了解)

### 5. 指令系统 (指挥计算机行动的命令)

*   **5.1 指令格式**
    *   指令的基本组成：操作码、地址码
    *   操作码的作用 (指令的功能)
    *   地址码的作用 (操作数的位置)
    *   指令字长、机器字长、存储字长 的概念
    *   定长指令格式、变长指令格式
*   **5.2 指令的类型**
    *   数据传送类指令
    *   算术运算类指令
    *   逻辑运算类指令
    *   移位操作类指令
    *   控制转移类指令 (重点)
        *   条件转移指令、无条件转移指令
        *   子程序调用与返回指令
        *   中断指令
*   **5.3 寻址方式 (如何找到操作数)**
    *   指令寻址：顺序寻址、跳跃寻址
    *   数据寻址 (重点)
        *   立即寻址
        *   寄存器寻址
        *   直接寻址
        *   间接寻址
        *   寄存器间接寻址
        *   基址寻址
        *   变址寻址
        *   相对寻址
    *   不同寻址方式的特点、有效地址的计算

### 6. 中央处理器 CPU (计算机的大脑)

*   **6.1 CPU 的功能与基本组成**
    *   CPU 的功能：指令控制、操作控制、时间控制、数据加工
    *   CPU 的基本组成部件
        *   运算器 (ALU) - 已学过
        *   控制器 (Control Unit - CU) -  重点
        *   寄存器组 (Registers) -  重点
        *   内部总线
*   **6.2 控制器的功能与工作原理**
    *   **指令周期**
        *   取指令周期、分析指令周期、执行指令周期
        *   间址周期、中断周期 (了解)
    *   **指令执行流程**
        *   取指、译码、执行 (Fetch, Decode, Execute)
    *   **控制方式**
        *   同步控制
        *   异步控制
        *   联合控制
*   **6.3 寄存器组**
    *   用户可见寄存器 (通用寄存器、数据寄存器、地址寄存器、条件码寄存器)
    *   用户不可见寄存器 (指令寄存器 IR、程序计数器 PC、存储器地址寄存器 MAR、存储器数据寄存器 MDR)
*   **6.4 时序系统**
    *   时钟周期、时钟频率
    *   指令周期、机器周期、节拍 (T 周期)

### 7. 总线系统 (计算机的神经系统)

*   **7.1 总线的概念与分类**
    *   总线的定义：连接各个部件的信息传输通路
    *   总线的分类
        *   按功能分：数据总线 DB、地址总线 AB、控制总线 CB
        *   按连接部件分：片内总线、系统总线、通信总线
*   **7.2 系统总线的结构**
    *   单总线结构
    *   双总线结构
    *   三总线结构
*   **7.3 总线特性及性能指标**
    *   总线宽度 (数据线的根数)
    *   总线频率 (时钟频率)
    *   总线带宽 (数据传输率)
    *   总线标准 (如 PCI, USB 等 - 了解)
*   **7.4 总线控制**
    *   总线判优控制 (集中式判优、分布式判优 - 了解)
    *   总线通信控制 (同步通信、异步通信、半同步通信、分离式通信 - 了解)

### 8. 输入/输出系统 (计算机与外部世界的桥梁)

*   **8.1 I/O 系统的组成**
    *   I/O 软件 (驱动程序、操作系统中的 I/O 管理模块)
    *   I/O 硬件 (I/O 接口、I/O 设备)
*   **8.2 I/O 接口**
    *   I/O 接口的功能
    *   I/O 接口的基本组成
        *   数据缓冲寄存器
        *   状态寄存器
        *   控制寄存器
        *   地址译码电路
        *   控制逻辑
*   **8.3 I/O 方式**
    *   程序查询方式 (轮询方式)
    *   程序中断方式 (重点)
        *   中断请求、中断响应、中断处理
        *   中断优先级
    *   DMA 方式 (Direct Memory Access - 直接存储器访问) - 了解
        *   DMA 控制器的功能
        *   DMA 传输过程
    *   通道方式 (了解)
*   **8.4 常用 I/O 设备 (了解)**
    *   输入设备：键盘、鼠标、扫描仪等
    *   输出设备：显示器、打印机、绘图仪等
    *   输入/输出设备：磁盘、磁带、光盘等 (也属于存储器)

## 📚 第三阶段：深入与扩展 (进阶学习)

### 9.  高级计算机体系结构概念 (拓展视野)

*   **9.1 流水线技术 (Pipeline)** - 了解基本思想
    *   指令流水线、运算流水线
    *   流水线性能指标 (吞吐率、加速比)
    *   流水线冲突 (结构冲突、数据冲突、控制冲突)
*   **9.2 并行处理技术 (Parallel Processing)** - 了解基本概念
    *   SIMD (单指令多数据流)
    *   MIMD (多指令多数据流)
    *   多核处理器、多处理器系统、集群系统
*   **9.3  存储器层次结构 (Memory Hierarchy)** -  回顾与深入
    *   Cache - 主存 - 外存  多级存储体系
    *   虚拟存储器 (Virtual Memory) - 了解概念
*   **9.4  输入输出系统的新发展 (New Trends in I/O)** -  了解发展趋势
    *   高速 I/O 接口技术 (如 Thunderbolt, NVMe)
    *   网络 I/O、云计算环境下的 I/O

##  📖  学习资源推荐

*   **教材推荐:**  《计算机组成原理》（唐朔飞版）、《Computer Organization and Design》（Patterson and Hennessy）等
*   **在线课程:**  中国大学 MOOC、Coursera、edX 等平台上的相关课程
*   **实验平台:**  Logisim (数字电路模拟器)、MARS (MIPS 汇编模拟器) 等
*   **学习网站/社区:**  CSDN、博客园、Stack Overflow、GitHub 等

##  🎯  学习方法建议

*   **理论与实践结合:**  多做习题、实验，加深理解。
*   **画图与总结:**  将抽象概念可视化，绘制框图、流程图等，并及时总结知识点。
*   **主动思考与提问:**  遇到问题不要怕，积极思考，查阅资料，或向老师、同学请教。
*   **坚持不懈:**  计算机组成原理内容较多，需要投入时间和精力，坚持学习才能取得进步。

**祝你学习顺利，在计算机组成原理的世界里收获满满！** 😊