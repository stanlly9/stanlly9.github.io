---
layout: post
title: 新增更多Anaconda Prompt字型
author: 史蛋利九的部落格
tags:
- 網路資源
- 科技先知
---

# More Fonts for Your Anaconda Prompt

使用Windows+Anaconda套件的中文語系使用者，多半都會發現anaconda prompt的字型實在是有點糟糕，但更換字型的時候絕大多數會看到下列畫面：
![windows prompt fonts in BIG-5](/img/in-post/cmd-prompt-in-big-5.png)

沒錯！可以選的字型超級少，經過一番搜尋之後發現，其實主要因素是Anaconda Prompt (M$ Windows版本)會去呼叫cmd.exe，而這個prompt(命令提示字元)，在絕大多數中文語系環境底下，cmd.exe帶起來的視窗字集預設都是Big5或者GB2312之類的東西，而相對應的100% true type font其實不多。如果不是很確定字集為何，可在prompt執行chcp看看預設字集是什麼，如下：
```shell
C:\Users\XXX\> chcp
使用中的字碼頁: 950
```
然後，可以到 [這裡](http://www.aivosto.com/articles/charsets-codepages.html)查詢，例如我的環境是950，為BIG5(台灣地區繁體中文)。

# 換Anaconda Prompt字型
想換任何基於cmd.exe視窗字型，其實可以單純的利用chcp 65001把字集換成UTF-8，如此一來可以選擇的字型就一瞬間大幅提升。不過如果純粹只想換Anaconda Prompt的字型，建議可以利用文字編輯器修改下列檔案

```shell
 C:\Users\{USER_NAME}\Anaconda3\Library\bin\conda.bat
```
請找個合適的地方加入一行chcp 65001，例如我是在**:DO_ACTIVATE**要跳回去**@GOTO :End**之前加入
```shell
:DO_ACTIVATE
...略
...略
chcp 65001
@GOTO :End
```
之後只要開啟Anaconda Prompt，會出現code page更改的訊息，同時也可以發現字型選單裡面多出裡面很多字型可以選擇，個人寫程式都偏好使用等字距(mono)類型的字型。
![windows prompt fonts in UTF-8](/img/in-post/cmd-prompt-in-UTF-8.png)


