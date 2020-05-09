---
layout: post
title: Complex Fixed-points in ANSI C
author: 史蛋利九的部落格
tags:
- SystemC
- 科技先知
---

As I mentioned before, SystemC provides a series well-define classes for fixed-point. For more details I will summarize them and make a short intro in these days. Here, I'll show you another way, in ANSI C, to write for my own fixed-point simulation. And it's fully compatiable with gcc.
Here is my cmplx_fix.h (header file for complex fixed-point)

```c++
//+FHDR------------------------------------------------
// (C) Copyright Company NTHU.EE VLSI Comm Lab.2009
// All Right Reserved
//-----------------------------------------------------
// FILE NAME: cmplx_fix.h
// AUTHOR: stanlly9
// CONTACT INFORMATION: stanlly9.blogspot.com
//-----------------------------------------------------
// RELEASE VERSION: V 1.0
// VERSION DESCRIPTION:
// 1.0 First release
//-----------------------------------------------------
// RELEASE DATE: Mar-25-2009
//-----------------------------------------------------
// PURPOSE: Complex fixed point
//-FHDR------------------------------------------------

#ifndef _CMPLX_FX_HDR
#define _CMPLX_FX_HDR

#define IWL 7//integer word-length
#define DWL 9 //decimal fraction word-length
//IWL+DWL=sizeof(short int)*2=16
typedef struct {
  short int re;
  short int im;
} cmplx_fix;
//check negaitve
int is_neg(short int);
//cmplx_fix fcns
void cf_print(cmplx_fix);//printer
void cf_seti_re(cmplx_fix*, int);//set rel part by integer values
void cf_seti_im(cmplx_fix*, int);//set img part by integer values
void cf_setf_re(cmplx_fix*, float);//set rel part by float values
void cf_setf_im(cmplx_fix*, float);//set img part by float values

//--cmplx_fix operator fcns--
//----cmplx_fix to cmplx_fix----
cmplx_fix cf_add(cmplx_fix, cmplx_fix);// +
cmplx_fix cf_sub(cmplx_fix, cmplx_fix);// -
cmplx_fix cf_mul(cmplx_fix, cmplx_fix);// *
cmplx_fix cf_div(cmplx_fix, cmplx_fix);// /
//----cmplx_fix to integer values----
cmplx_fix cf_add_re(cmplx_fix, int); // + real
cmplx_fix cf_add_im(cmplx_fix, int); // + imag
//cmplx_fix cf_sub_re(cmplx_fix, int); // - real as _add_re(-int)
//cmplx_fix cf_sub_im(cmplx_fix, int); // - imag as _add_im(-int)
cmplx_fix cf_mul_re(cmplx_fix, int); // * real
cmplx_fix cf_mul_im(cmplx_fix, int); // * imag
cmplx_fix cf_div_re(cmplx_fix, int); // / real
cmplx_fix cf_div_im(cmplx_fix, int); // / imag
#endif
```

In ANSI C, we don't have much useful programming shortcuts,  
**no classes, no functional overridding, no operator overridding, etc**  
All things we can do is function calls, such as the function:  
**cf_print()** is self-made print function.  
**cf_add()** is the func for my cmplx_fix addition.  

For the cmplx_fix structure contains two members:  
**re** is the real part  
**im** is the imalge part  
They are in a short int datatypes(signed 16bits each) for reducing memory allocation.
The interger word-length is define by IWL, decimal fraction part by DWL 

In these version, I do not perform the overflow and stratuation processing.
It may be improved in the future.
The cmplx_fix addition function cf_add() is shwon as an example here:
```c++
//cmplx_fix + cmplx_fix
cmplx_fix cf_add(cmplx_fix a, cmplx_fix b)
{
  short int real = a.re + b.re;
  short int imag = a.im + b.im;
  a.re = (short int) real;
  a.im = (short int) imag;
  return a;
}
```
