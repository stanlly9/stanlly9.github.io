---
layout: post
title: 字型的深度學習(2)
author: 史蛋利九的部落格
tags:
- AI
- deep learning
- 網路資源
- 科技先知
---

發現一個有趣的東西：

### zi2zi: Master Chinese Calligraphy with Conditional Adversarial Networks
![zi-to-zi](/img/in-post/zi2zi.gif)  
https://github.com/kaonashi-tyc/zi2zi  
這個github上面的zi2zi(字到字)專案，跟我之前想到的人工智慧字型學習的概念相當雷同！

稍加研究之後，簡單而言，style transfer的一種AI應用方式，就我初步的理解，這一類的應用主要是在training的時候，給定一組已知input stream，以及他相對應型別轉換後的output stream。講白話一點，如果我的style transfer叫做『灰階化』，那麼這一對已知的input就可以是彩色圖片，而對應的output便是灰階處理過的圖片。下圖是一個風格化的例子
![style-transfer](/img/in-post/style-transfer.jpg) https://www.techleer.com/articles/466-insight-into-fast-style-transfer-in-tensorflow/
如果對style transfer有興趣，可以搜尋prisma這個app看看他們的厲害之處

![prisma](/img/in-post/prisma.png) https://prisma-ai.com/

# 以下是目前對zi2zi初步理解：

zi2zi利用這個style transfer的基本做法(之一)，大致如下：

## training的時候…

先用字型A產生特定中文字的圖像當作training input stream，接著找另外一個字型B產生同樣的相同中文字的圖像來當作training output stream。

## inference的時候…

當deep learning model已經學習完畢，如果它訓練效果很好，表示它大致上已經摸熟了字型A到字型B的微調原則，所以我們可以刻意給定另外一組不同中文字所組成的圖像當作inference input stream，讓它產生inference output stream。到這邊為止，還是zi2zi的本質。

## 但我想到的應用是：

倘若字型B是一個字數有短缺的字型，也許因為人力資源有限導致開發中斷或緩慢等等。透過這種作法我們其實可以要求這位虛擬字型學徒，透過inference的方式產生其他原先它並沒有看過的中文字。用這個特點，假設字型A是類似全字庫字型的full set，那我們可以這種做法來補足字型B的字數！

## 但有幾個潛在的問題：

1. 虛擬字型學徒可能學習效果很差
2. 虛擬字型學徒只能做圖到圖的轉換，但數位字型檔是OTF格式，中間還有一番轉換功夫

