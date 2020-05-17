---
layout: post
title: 字型的深度學習(4)
author: 史蛋利九的部落格
tags:
- AI
- deep learning
- 字型藝術
- 科技先知
---

# 字型的深度學習里程碑
《字型的深度學習》專案，目前設定下列重要目標跟里程碑：
 1. 先學會基本tensorflow操作
 2. 跑zi2zi project範例
 3. 以自訂內容完成zi2zi project: training
 4. 以自訂內容完成zi2zi project: inference
 5. 將inference output image進行向量化
 6. 將向量化之後的文字集成字型檔

目前設定的終極目標是要能夠利用各種程式透過deep learning的方式來生成字數要有一定程度以上的中文字集字型檔案。
# 附加價值

執行《字型的深度學習》，可能順便或者說必須習得一些技能：

 1. 基本tensorflow操作
 2. Google Cloud Platform操作
 3. 理解人工智慧應用當中的style-transfer的基本原理
 4. 如何利用程式將簡單的圖形內容進行向量化
 5. 如何利用向量化的檔案來集結成字型檔
 6. 生成字型檔的基本步驟 

# Lyudmil Vladimirov

這篇教學目前停擺，暫時沒空自己蒐集圖片&貼標籤，之後有搜尋到別人的dataset再繼續跟進。

# zi2zi Experiments
## 2018/11/11
按照zi2zi git hub上面的說明，我是選新細明體當作src_font，而dst_font則是選用康熙字典體。目前做font2img跟package需要針對python2/3做微幅修改，已順利完工。不過training部分還沒把.py從python2升級到python3。

## 2018/11/12
使用tensorflow_gpu virtual environment跑的training, 目前似乎會遭遇GPU報resource不足的問題。未解，stdout message如下：

````
tensorflow.python.framework.errors_impl.ResourceExhaustedError: 
OOM when allocating tensor with shape[5,5,512,1024] and type float on 
/job:localhost/replica:0/task:0/device:GPU:0 by allocator GPU_0_bfc

Hint: If you want to see a list of allocated tensors 
when OOM happens, add report_tensor_allocations_upon_oom 
to RunOptions for current allocation info.
````

## 2018/12/04

研究了一下發現應該是zi2zi本身建立的model需要大量GPU memory, 根據作者在github上面的[回覆](https://github.com/kaonashi-tyc/zi2zi/issues/30), 大概要6GB, 而我PC上面的GTX-960只有2GB.  可能先直接試用pre-trained model來實驗後續動作. zi2zi training大概只能往免費或者費用稍微能接受的其他運算平台, 
[https://towardsdatascience.com/maximize-your-gpu-dollars-a9133f4e546a](https://towardsdatascience.com/maximize-your-gpu-dollars-a9133f4e546a)
