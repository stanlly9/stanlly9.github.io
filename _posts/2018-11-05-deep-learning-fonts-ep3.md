---
layout: post
title: 字型的深度學習(3)
author: 史蛋利九的部落格
tags:
- AI
- deep learning
- 網路資源
- 科技先知
---
# Tensorflow平台選擇
跑tensorflow平台大致研究了一下, 除了用自己的PC來跑之外, 也可以使用Google Cloud Platform(GCP)或者Amazon的AWS服務, 但發現GCP收費約 USD $300/month跑不掉, 即使是可以使用小時計費的TPU感覺還是不便宜, 自己畢竟還是初學者, 先用PC研究看看吧
# zi2zi project will migrate to python 3
zi2zi project似乎還在使用比較舊的python2, 但目前大多數tensorflow app/tutorial都已經轉向python3, 有人在github上面提問後, 作者也已經回應將會將zi2zi migrate到python3
# 使用local desktop PC來跑Tensorflow
目前找到一篇教學如下:
[tensorflow-object-detection-api-tutorial.pdf](https://media.readthedocs.org/pdf/tensorflow-object-detection-api-tutorial/latest/tensorflow-object-detection-api-tutorial.pdf)  
因為我當初組電腦有裝NV的GTX 960顯示卡. 所以可以用CUDA來加速.  不過2018/11/01的當下, CUDA已經出到10.0, cuDNN則是v7.3.1;
#### 2018/11/01
跟到 1.3.2.2 Install CUDNN
#### 2018/11/05
跟到1.4.3 Adding necessary Environment Variables, 下一步是Google protobuf
#### 2018/11/06
目前跟到1.4.5 Test your Installation;  BTW, Anaconda prompt的視窗字型實在有夠糟糕, 花了一點時間研究. 根據這篇, 問題來源是cmd.exe在Windows 10底下會根據locale字集來改變字型, 如果字集限定在big5, 很不幸的事實是支援的字型少之又少, 正確做法應該是改用UTF-8, 也就是chcp 65001. 我是在
C:\Users\{YOUR_USER_NAME}\Anaconda3\Library\bin\conda.bat裡面加上一行
chcp 65001
#### 2018/11/11
跟到 3.2 Annotating images，不過需要使用labelImg tool，來幫圖片建立label(xml)檔案，不過目前還來不及準備照片跟上tag。文件建議要100張圖片，目前打算去抓別人設定好的dataset

