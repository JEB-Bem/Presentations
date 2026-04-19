---
# try also 'default' to start simple
theme: ../seriph-theme
fonts:
  sans: 'PT Serif, Noto Color Emoji'
  serif: 'PT Serif, Noto Color Emoji'
background: /Web02-bg.png
title: Crypto - DES
info: |
  Introduction to DES

# apply UnoCSS classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# duration of the presentation
duration: 40min
# 允许下载
---

# D[*ata*]{style="color:#c4c4c4fa"} E[*ncryption*]{style="color:#c4c4c4fa"} S[*tandard*]{style="color:#c4c4c4fa"}
## Introduction and Simple Implementation

Blue-Whale Fresher & Cyber Space Security Class Training

---

# DES 加密算法
工作模式简介

一般来说，以 DES、AES 为代表的分组对称加密算法会按照下面流程工作：

1. 将明文按照固定的长度分组
2. 将每个分组按照不同工作模式进行加密
3. 将分组拼接起来，然后返回

---
layout: two-cols
---

# DES 加密算法
工作模式简介

- <span v-mark="{at: 1, type: 'crossed-off', color: 'red'}">ECB(Electronic CodeBook)</span>
- CBC(Cipher Block Chaining)
- CTR(Counter)
- CFB(Cipher FeedBack)
- OFB(Output FeedBack)

<Arrow x1="292.9047138872136" y1="145.8238841978287" x2="486.0048345144753" y2="166.46562123039809" />
<Arrow x1="304.8902386158022" y1="178.45114595898679" x2="479.98794669782876" y2="314.20265379975876" />

图中的加密过程皆以 DES 为例。

::right::

![ECB-Mode](/ECB-Mode.png)

![CBC-Mode](/CBC-Mode.png)

---
layout: image
image: /ECB-Mode.png
backgroundSize: 70%
---

# <span class="text-color-lime">ECB Mode</span>

---
layout: image
image: /CBC-Mode.png
backgroundSize: 80%
---

# <span class="text-color-lime">CBC Mode</span>
以及 [Paddding](https://en.wikipedia.org/wiki/Padding_(cryptography)#PKCS#5_and_PKCS#7)

---

# Encrypt with $k$
首先讲讲 encrypt

1. 64-bit Message Block 通过 $IP$ 表进行置换[（不会提高密码  
   安全性）]{style="color:grey"}
2. 将 64-bit Block 分成左、右两部分，记为 $L_1, R_1$
3. 根据公式 $L_i = R_{i-1}, R_i = L_{i-1} \oplus f(R_{i-1}, k_{i-1})$ 迭代  
   计算 16 轮
4. 按照 $R_{16} || L_{16}$ 拼接并使用 $IP^{-1}$ 表进行逆置换得到最终的  
   Encrypted Block

<br/>

- $f$ 称为 Feistel (F) function
- Left Block 和 Right Block 都是 32 bits
- Feistel Network 是可逆的

<div class="absolute right-40px bottom-20px">
<img src="/20260419-6b3208553e028ba9.png" width=390px/>
</div>

---

# Encrypt with $k$
首先讲讲 encrypt

Feistel function 是 DES 的核心，分为 E-box、 S-box 和 P-box.

- E-box 将 $R_i$ 扩展为 48 位，方便之后的异或，这是一个线性  
  变换
- 扩展后的 48 位 Block 与轮密钥 $K_i$ 进行异或，这同样是一个  
  线性变换
- 最后将异或得到的 48 位 Block 丢进 S-box，做[非线性变换]{style="color:#ee6666"}！
- S-box 得到的 32 位 Block 再经过 P-box 的置换，就完成了  
  F Function 的整个工作流程

<br/>

<div class="absolute right-20px bottom-35px">
<img src="/20260419-bce94118703c0920.png" width=400px/>
</div>

---

# Encrypt with $k$
再来讲讲 $k$

我们要将用户输入的主密钥 $key$ 经过扩展得到 16 个 48 bits 的轮密钥$Round Key_i$.  
其过程如图所示，需要用到 PC-1、PC-2 置换和一个旋转位数表.

从图中可以看出，尽管用户输入是 64-bit $key$，但实际上被用到的只有 56 bits.

<div class="absolute right-20px bottom-35px">
<img src="/20260419-9f5a1ad0efc8575e.png" width=400px/>
</div>

---

# Practice

尝试实现 DES！

作业仓库在[这里](https://github.com/JEB-Bem/DES-CBC). 你可以根据 PPT 的讲解思路来逐个实现每个函数，也可以根据你自己的理解来逐步实现每个函数，每次实现完一个函数，你可以去 `tests.py` 中寻找对应的测试，然后下面的运行来运行匹配到的多个测试。

```bash
uv run python -m unittest -k <部分测试函数名>
```

比如：

```bash
uv run python -m unittest -k init
```

将会运行下面这 3 个测试：

- `test_init_invalid_hex`
- `test_init_invalid_length`
- `test_init_valid`

(另外蓝桥杯要开始了，去年报名的同学记得好好准备😉)

---

# References
7a m3n j1an9 de 6i w0 ha0

\[1\] OUC 现代密码学课程  
\[2\] [Wikipedia-DES](https://en.wikipedia.org/wiki/Data_Encryption_Standard)  
\[2\] [Wikipedia-DES-Appendix](https://en.wikipedia.org/wiki/DES_supplementary_material)  

---

<SlidevVideo controls>
  <!-- Anything that can go in an HTML video element. -->
  <source src="/BlueWhale培训-DMS.mp4" type="video/mp4" />
  <p>
    Your browser does not support videos. You may download it
    <a href="/BlueWhale培训-DMS.mp4">here</a>.
  </p>
</SlidevVideo>
