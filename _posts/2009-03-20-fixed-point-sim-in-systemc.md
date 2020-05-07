---
layout: post
title: How to perform fixed-point simulation in SystemC
author: 史蛋利九的部落格
tags:
- SystemC
-  科技先知
---

When you need to converts a floating-point digital signal processing program written in C or C++ language to a fixed-point program automatically. Maybe the following tips will help.

![systemc_logo](/img/in-post/logo_systemc.gif)

Recently, I have tried to using SystemC to perform a fixed-point simulation for my DSP program. There are lots of built-in C++ classes [datatypes] for fixed-point representations, which are also very useful. For examples, the support of operator overridding were compeletly done by OSCI. Program designers can multiply the real values they want without considering the representations for integer part and the decimal part. All the rest jobs like scalling, signed extension, rounding are automatically performed by default.


SystemC support many datatypes for fixed-point representations, such as :

```c
sc_fix //signed values
sc_ufix //unsigned values
sc_fixed //signed values, fixed word-length
sc_ufixed //unsigned values, fixed word-length
```

The difference between **sc_fix** and ***sc_fixed*** is that the **sc_fixed** version could only have a specificaly fixed word-length while compiling. It also means that the **sc_fix** version can perform the ***dynamic fixed-point precision*** in run-time(you may change the word-length in some place if you want).

![image](/img/in-post/DSC_111_m.jpg)

Besides, there are *_fast* versions for above 4 datatypes, the *_fast* version's precisions are limitted to a maximun length for 53-bits in order to speed up the simulation task. I think the *_fast* version will be a help. Since there is no need for high persions while perfoming fixed-point simulations.

If you want to know the quatization noise effect on your application, I think the **sc_fixed_fast** and **sc_fixed** might be the most useful datatypes.

Here are some usage about **sc_fixed_fast**:

```c
#define SC_INCLUDE_FX
sc_fixed_fast<8,3> x;
```

First of all, the definition of *SC_INCLUDE_FX* enables the SystemC bulit-in library for fixed-point datatpyes. Without this definition, the library will not reconize the **sc_fix** datatypes. You may see the release notes in the SystemC download resources.

The <8,3> represents the total word-length and the integer word-length.
It follows the format as:

> , where WL is the word-length and IWL is the integer word-length.

You may see the x variable as "saa.bbbbb" in which the 'saa' are the signed bit and the integer bits. And the 5-bits 'bbbbb' are the decimal fraction part.  

If you want to assign a real value '2.333' to x, you just use:
x=2.333; The rounding result for x will be 2.3125. Here is an example for FIR filter...

![img](/img/in-post/qw.gif)

