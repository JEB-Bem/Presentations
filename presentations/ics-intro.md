---
# try also 'default' to start simple
theme: ../seriph-theme
fonts:
  sans: 'PT Serif, Noto Color Emoji'
  serif: 'PT Serif, Noto Color Emoji'
background: /ics-bg.png
title: ICS Lab Intro.
info: |
  Introduction to ICS Labs

# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: fade
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# duration of the presentation
duration: 40min
# 允许下载
---

# 计算机系统基础Ⅱ实验

## 实验安排 & Lab0 发布

<style>
/* 字体：思源黑体（副标题/作者）、思源宋体（主标题回退）取自 Google Fonts */
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@400;500&family=Noto+Serif+SC:wght@500;600&display=swap");

.slidev-layout.cover {
  --navy: #16324f;
  --gray: #4d4d4d;
  position: relative;
  padding: 0 9%;
  text-align: left;
  color: #000 !important;
  /* 浅蓝科技电路图；去掉主题默认叠加的黑色遮罩 */
  background: url("/ics-bg.png") center/cover no-repeat !important;
}

/* 半透明白色渐变遮罩：弱化背景干扰、保证文字可读 */
.slidev-layout.cover::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  background: linear-gradient(100deg,
    rgba(255, 255, 255, .95) 0%,
    rgba(255, 255, 255, .85) 32%,
    rgba(255, 255, 255, .4) 58%,
    rgba(255, 255, 255, 0) 78%);
}

.slidev-layout.cover > * { z-index: 1; }

/* 主标题：华文中宋，深藏青，字距微宽 */
.slidev-layout.cover h1 {
  margin: 0 0 1.2rem;
  color: var(--navy) !important;

  font: 600 3.6rem/1.15 "华文中宋", "STZhongsong", "Noto Serif SC", "Songti SC", SimSun, serif;
  letter-spacing: .08em;
}

/* 副标题 / 作者：思源黑体，深灰 */
.slidev-layout.cover :is(h2, .cover-author) {
  margin: 0;
  color: var(--gray) !important;
  font-family: "Noto Sans SC", "Source Han Sans SC", "思源黑体", sans-serif;
  font-weight: 400;
}
.slidev-layout.cover h2 { font-size: 1.7rem; letter-spacing: .18em; }
/* 作者：左下角，左对齐 */
.slidev-layout.cover .cover-author {
  position: absolute;
  left: 9%;
  bottom: 2.6rem;
  z-index: 1;
  font-size: 1.05rem;
  letter-spacing: .12em;
}
</style>

---

# 实验安排

实验成绩占课程成绩的 20%，即总成绩为 20 pts，各实验的总分、主要内容和预计完成时间如下：

| 实验 | 分值 | 主要内容                 | 预计用时 |
|------|------|--------------------------|----------|
| Lab0 | 2pts | 实验环境配置与基本概念   | 2 周     |
| Lab1 | 5pts | DataLab (位运算)         | 2 周     |
| Lab2 | 7pts | BombLab (二进制逆向分析) | 4 周     |
| Lab3 | 6pts | DOSLab (汇编实验编程)    | 2 周     |

🎉 **展示加分**：每个实验可以申请**课上展示**，可得到每个实验最多 25% 的展示加分，每个实验最终成绩不超过该实验的满分。

---

# 实验课上课方式
实验讲解与作业检查

**课堂展示**

课程前半段进行实验展示，展示名额根据实验难度而定，每次课前公布。

**实验讲解**

若有新实验发布，则讲解新发布的实验。

**实验检查**

剩余时间检查同学们的实验，若当天实验还未截止，只检查已提交实验报告的同学，否则所有人都要检查。

**答疑**

实验课空闲时间可现场答疑。

---
layout: cover
background: #ffffff
---

# Q & A

---

# Lab0 实验环境配置与基本概念
实验介绍

实验已经发布在智慧树平台，截止时间 **10 月 30 日 23:59**.

**实验要求**（详细要求见[实验讲义](https://chrjeb.cn/ics-lab0.html)）：

- **文件命名** `Lab0-姓名-学号.pdf`
- **实验报告内容** 包括实验过程与截图、实验结果与分析、遇到的问题（如果有）.

**实验内容**：

- Lab0 需要我们对整个计算机系统有一个初步的了解，因此我们会提前涉及一些理论课还未提到的内容。尽管稍后我们会学习很多理论知识，但大家不用担心，实验难度一降再降，现在已经“有手就行”了 😉。
- 在本次实验中，我们会初步了解一个二进制程序是怎样在 Linux 系统中运行起来的，并建立起一个**进程**的概念，进而了解进程的加载和执行的过程。
- **任务1**：比较可重定位目标文件和可执行文件
- **任务2**：复现实验讲义演示的“逆向确认常量字符串 `"Hello World"` 在 `bar` 文件中的偏移”

---
layout: cover
background: #ffffff
---

# Lab0 理论知识
~~速通计算机系统基础~~

从 0 开始搭建一个计算机的理论模型  
PS：不要吝啬你的提问

---

# 回想一下
调试一个 C 程序

- 许多同学应该都用过 VSCode 等 IDE 软件，体验过在上面调试程序
  - 我们总有一种感觉，当程序停在断点的时候，对于程序来说整个世界似乎都暂停了
  - 我们点击 Step Over 按钮，程序就向前执行一步
- 这些模糊的感觉似乎都指向一个事实——运行的程序就是一个状态机

![20261015-b95386066103f96a.png](./images/20261015-b95386066103f96a.png){width=450px class="mx-auto block"}

---

# 图灵机
Everything is a state machine

在以前的学习中，相信大家已经有了图灵机的概念

- 一条无限长的纸带
- 一个读写头
- 一套规则（条件分支、循环、递归）

读写头不断在纸带上移动，读取、写入、计算... 数据都保存到了纸带上，而图灵机则根据纸带来进行状态转移（下一步应该读取，写入，还是计算？），而“状态”实际上就是纸带上的数据 + 读写头的位置，因此

**图灵机本质上是一个状态机。**

---

# 计算机
Everything is a state machine

**计算机实际上也可以看作一个图灵机。**

- 纸带就是内存（+硬盘）
- 读写头移动就是 PC 寄存器（保存当前指令执行的位置）变化
- 读写头读取就是 CPU 读写内存和寄存器
- 图灵机内部的状态转移规则就是 CPU 的指令集

***区别在哪里？***{color=#39b2cd}  
[内存并不和纸带一样是无限长的（但它理论上是可无限扩展的 🤓）]{color=#39b2cd}

---
layout: two-cols
---

# 进程
Everything is a state machine

进程可以简单的定义为**运行中**的程序。

计算机是一个状态机 $\xrightarrow{\text{虚拟化}}$ 进程是一个状态机

[*虚拟化*]{color=#39b2cd} 有点不好理解，换个词，“[缸中之脑]{color=#39b2cd}”！

在现代计算机中，或者说现代操作系统中，一个进程因为虚拟化这一操作系统抽象，使得进程获得一种“拥有”整个计算机的假象。即整个计算机上似乎都只有这一个进程在执行。

程序A：“真好，CPU 一直都**只在**执行我这个程序”  
计算机: “让程序 A 执行一秒钟吧”

程序A：“不错，整个内存空间都是我的”  
计算机: “程序 A 要 `0x12996788` 处的内存，把 `0x30771337` 处的内存给他”

::right::

<div class="absolute right-20px top-1/2 -translate-y-1/2">
<img src="/20261010-4f5b88a62aa1d1bc.png" width=450px/>
</div>

---
layout: two-cols
---

# 进程
严谨一点的定义

一个进程的状态由两个明显的组成部分：
- 地址空间（Address Space）
- 寄存器（Registers）

<span v-click>从硬件的视角来看，CPU 就是不断的从地址空间中 PC 指向的位置取出指令，然后执行它，</span><span v-click>执行的过程中可能改变地址空间和寄存器，这就发生了状态的转移，</span><span v-click>执行完毕后，PC 指针指向下一条指令的起始位置，程序执行下一条指令。循环往复。</span><span v-click>因此，计算机实际上就是不停计算的机器.</span>

✌️ 到这里，我们已经建立起一个进程的基本模型了。

::right::

<div class="absolute right-20px top-1/2 -translate-y-1/2">
<img src="/20261010-4f5b88a62aa1d1bc.png" width=450px/>
</div>

---

# 地址空间（Address Space）

前面提到了虚拟化，进程好像独占了整个计算机，我们把“虚拟化”拆开，聊聊内存虚拟化。

所谓内存虚拟化

- 在 IA-32 上，就好像是进程拥有了 $[0, 2^{32})$ 共 $2^{32}$ Bytes = $4$ GB 这么大的内存；
- 在 x86-64 上，就好像是进程拥有了 $[0, 2^{64})$ 共 $2^{64}$ Bytes = $1.7 \times 10^{10}$ GB 这么大的内存.

![20261011-ad0358c261e4f28c.png](/20261011-ad0358c261e4f28c.png){width=450px class="mx-auto block"}

---

# 地址空间（Address Space）

地址空间存放了代码和运行时产生/加载的数据。

- 进程运行时会分配栈和堆，这可以看作是一个程序运行时的“草稿纸”，所有运行时产生的非持久数据都储存在里面。
- 我们的程序本体（那个神秘的二进制文件，在 Linux 中称之为 ELF）也会被加载到内存中
  - 其中一些可读可写的段（一个 ELF 被划分为若干个段），存放了包括全局变量在内的东西，实际上也是“草稿纸”的一部分，
  - 另一些只读的段，除了我们定义的常量以外，就是代码了，这可以看作一个进程的“大脑”，下一步做什么？根据运算得到的结果该做怎样的处理？什么时候停止？都是由从文件加载进来的那些只读的段来决定的。
  - 当然，以上过程是简化之后的。

[heap.c](vscode://file/home/jeb/tmp/demos/Lab0/heap.c)

![20261011-7a9cc10518f0a1ef.png](/20261011-7a9cc10518f0a1ef.png)

---

# 寄存器（Registers）
比内存更快亿点点的东西

寄存器是计算真正发生的地方，我们把内存比作草稿纸的话，寄存器就可以比作大脑的瞬时记忆了，当我们在草稿纸上看到一个 $7 \times 2 = ?$ 的计算题时，$7$, $2$, $\times$ 就被大脑读取了，在脑中经过一番酣畅淋漓的计算之后，我们得出答案 $14$，于是将这个答案写到草稿纸上。

计算机也是这样，*数据从内存被读取到寄存器中，CPU 用寄存器进行计算，再将结果写回到内存中。*

![20261011-200ae0472ddde4f7.png](/20261011-200ae0472ddde4f7.png){width=450px class='mx-auto block'}

---
layout: two-cols
---

# 寄存器（Registers）

寄存器大概分为这几种

- General Registers (通用寄存器)
- Segment Registers (段寄存器)
- Status Registers (状态寄存器)
- Instruction Register (指令寄存器) or Program Counter (程序计数器)

::right::

<div class="absolute right-20px top-1/2 -translate-y-1/2">
<img src="/20261010-4f5b88a62aa1d1bc.png" width=450px/>
</div>

---
layout: two-cols-header
---

## 通用寄存器（Registers）

::left::

| 64bit | 32bit | 16bit | 8bit (高) | 8bit (低) |
|-------|-------|-------|-----------|-----------|
| RAX   | EAX   | AX    | AH        | AL        |
| RBX   | EBX   | BX    | BH        | BL        |
| RCX   | ECX   | CX    | CH        | CL        |
| RDX   | EDX   | DX    | DH        | DL        |
| RSI   | ESI   | SI    | —         | SIL       |
| RDI   | EDI   | DI    | —         | DIL       |
| RBP   | EBP   | BP    | —         | BPL       |
| RSP   | ESP   | SP    | —         | SPL       |

::right::
| 64bit | 32bit | 16bit | 8bit (高) | 8bit (低) |
|-------|-------|-------|-----------|-----------|
| R8    | R8D   | R8W   | —         | R8B       |
| R9    | R9D   | R9W   | —         | R9B       |
| R10   | R10D  | R10W  | —         | R10B      |
| R11   | R11D  | R11W  | —         | R11B      |
| R12   | R12D  | R12W  | —         | R12B      |
| R13   | R13D  | R13W  | —         | R13B      |
| R14   | R14D  | R14W  | —         | R14B      |
| R15   | R15D  | R15W  | —         | R15B      |

---

# 通用寄存器（General Registers）
一个通用寄存器的结构示例

用 C 语言的 union 类比一下（[reg.c](vscode://file/home/jeb/tmp/demos/Lab0/reg.c)）：

```c
struct {
  union {
    uint64_t rax;
    union {
      uint32_t eax;
      union {
        uint16_t ax;
        struct { uint8_t ah; uint8_t al; };
      };
    };
  };
} reg;
```

![20261011-0d7bd7739b6e12ec.png](/20261011-0d7bd7739b6e12ec.png){width=350px class='mx-auto block'}

---

# 汇编代码语法

计算机 “看到” 的指令长什么样，以 Intel 语法为例.

```asm
add eax, 0xdeadbeef
```

<div class="absolute top-[131px] left-[61px] w-[27px] h-[32px] border border-dashed border-red-400 rounded"></div>

<div class="absolute top-[131px] left-[90px] w-[25px] h-[32px] border border-dashed border-green-400 rounded"></div>

<div class="absolute top-[131px] left-[127px] w-[75px] h-[32px] border border-dashed border-green-400 rounded"></div>

- [Opcode]{color=red}: 操作码，这条指令需要执行的操作
- [Operand]{color=green}: 操作数（或称操作对象）
  - Immediate Operands 立即数操作数
  - Register Operands 寄存器操作数
  - Memory Operands 内存操作数

简要一提，真实的指令其实很复杂 ↓

> The information encoded in an 80386 instruction includes a specification of
> the operation to be performed, the type of the operands to be manipulated,
> and the location of these operands. If an operand is located in memory, the
> instruction must also select, explicitly or implicitly, which of the
> currently addressable segments contains the operand.  
> —— I386 Manual

---
layout: two-cols-header
---

## 一个简单的 [C 程序](https://godbolt.org/z/5KbdohKfG)

各种形式的程序，C -> 汇编 -> 二进制。根据我们以往的 C 的学习，知道有栈、堆的概念，由此引出内存的概念——于是得到一个基本的模型，程序的执行发生在内存上，数据在内存上被计算、产生。

::left::

```asm{*}{lines:true,maxHeight:'350px'}
"n":
        .zero   4
"m":
        .long   114514
.LC0:
        .string "Hello World."
.LC1:
        .string "c = %d\n"
"main":
        push    rbp
        mov     rbp, rsp
        sub     rsp, 16
        mov     edi, 4
        call    "malloc"
        mov     QWORD PTR [rbp-8], rax
        mov     rax, QWORD PTR [rbp-8]
        mov     DWORD PTR [rax], 6
        mov     DWORD PTR "n"[rip], 2
        mov     edi, OFFSET FLAT:.LC0
        call    "puts"
        mov     rax, QWORD PTR [rbp-8]
        mov     edx, DWORD PTR [rax]
        mov     eax, DWORD PTR "m"[rip]
        imul    edx, eax
        mov     eax, DWORD PTR "n"[rip]
        imul    eax, edx
        mov     DWORD PTR [rbp-12], eax
        mov     eax, DWORD PTR [rbp-12]
        mov     esi, eax
        mov     edi, OFFSET FLAT:.LC1
        mov     eax, 0
        call    "printf"
        mov     rax, QWORD PTR [rbp-8]
        mov     rdi, rax
        call    "free"
        mov     eax, 0
        leave
        ret
```

::right::

```c {*}{lines:true}
int n, m = 114514;
int main() {
  int *a = malloc(4);
  *a = 6;
  n = 2;
  printf("Hello World.\n");

  int c = *a * m * n;
  printf("c = %d\n", c);

  free(a);
  return 0;
}
```

![20261011-298da11bdf6a7eea.png](/20261011-298da11bdf6a7eea.png){width:10px}

<style>
.slidev-layout.two-cols-header {
  column-gap: 1rem;
}
</style>

<!--
这是我们今天需要研究的程序，一个很简单的 C 程序。当我们敲完一个 HelloWorld，再敲完一个 gcc 编译命令，按下回车的那一刻，我们的程序其实经历了好几次变换，最终成为了右下角一个神秘的二进制文件。

这里列出了程序的几个比较重要的，“状态”，我们看到源代码、汇编代码，和二进制文件。我们首先从源代码开始。

在《高级程序语言设计》课程上，相信大家对 C 都已经不陌生了，大家应该都了解过栈、堆的内存概念，程序进入一个函数之后又栈帧，栈帧里保存了局部变量...

这些东西都在内存里面，程序运行的所有中间数据都保存在内存中，然后再将结果通过IO 操作输出给用户。

没有内存就没有在系统中运行的进程. 那么进程是什么？
-->

---
layout: two-cols-header
---

## 一个简单的 C 程序

我们可以大致地将汇编与 C 对应起来

::left::

```asm{*|1-8|10-12|13-15|16,17|18|19-20|21-27|28-32|33-35|36-38}{lines:true,maxHeight:'350px'}
"n":
        .zero   4
"m":
        .long   114514
.LC0:
        .string "Hello World."
.LC1:
        .string "c = %d\n"
"main":
        push    rbp
        mov     rbp, rsp
        sub     rsp, 16
        mov     edi, 4
        call    "malloc"
        mov     QWORD PTR [rbp-8], rax
        mov     rax, QWORD PTR [rbp-8]
        mov     DWORD PTR [rax], 6
        mov     DWORD PTR "n"[rip], 2
        mov     edi, OFFSET FLAT:.LC0
        call    "puts"
        mov     rax, QWORD PTR [rbp-8]
        mov     edx, DWORD PTR [rax]
        mov     eax, DWORD PTR "m"[rip]
        imul    edx, eax
        mov     eax, DWORD PTR "n"[rip]
        imul    eax, edx
        mov     DWORD PTR [rbp-12], eax
        mov     eax, DWORD PTR [rbp-12]
        mov     esi, eax
        mov     edi, OFFSET FLAT:.LC1
        mov     eax, 0
        call    "printf"
        mov     rax, QWORD PTR [rbp-8]
        mov     rdi, rax
        call    "free"
        mov     eax, 0
        leave
        ret
```

::right::

```c {*|1|2|3|4|5|6|8|9|11|12}{lines:true,at:1}
int n, m = 114514;
int main() {
  int *a = malloc(4);
  *a = 6;
  n = 2;
  printf("Hello World.\n");

  int c = *a * m * n;
  printf("c = %d\n", c);

  free(a);
  return 0;
}
```

<style>
.slidev-layout.two-cols-header {
  column-gap: 1rem;
}
</style>


---
layout: two-cols
---

# 进程的加载
从硬盘到内存

我们前面在内存空间里面看到了“程序本体”，也就是说原本放在硬盘里面的程序被加载到了内存里面。

依旧把把计算机比作人，我们如果拿到了一份行动指南，那么把这份指南背到脑子里就是程序加载的过程。

- 背书的过程中我们还可能根据上下文重新排列一下顺序，比如写在最后的注意事项可能会和前文的某个段落联系到一起，因此**程序应该会告诉计算机怎么把自己放到内存里**；
- 开始行动的时候我们会首先找到脑子里行动指南的开始的位置，然后做一条、执行一条，一直执行下去，因此**程序应该告诉计算机从哪里开始执行**；

::right::

<div class="absolute right-20px top-1/2 -translate-y-1/2">
<img src="/20261011-b263d13001c8f005.png" width=450px/>
</div>

---

# 进程的加载
真实的加载过程

实际上，计算机也正是这样做的！

![20261011-c3f3302b6160fc19.png](/20261011-c3f3302b6160fc19.png){width=750px class="mx-auto block"}

---
layout: cover
background: #ffffff
---

# Q & A

---
layout: end
---

# 谢谢

迈出第一步最重要的，**莫过于坚信所有的问题都能得到满意的解答，然后去花时间理解其中的来龙去脉**。如果你感到恐惧，请记住：坚持住，进入未知领域，**从简单的、能理解的东西试起，投入时间，就有收获**。  
—— jyy
