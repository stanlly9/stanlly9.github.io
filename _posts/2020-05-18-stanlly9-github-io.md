---
layout: post
title: 用markdown搭配Jekyll改寫史蛋利九的部落格!
author: 史蛋利九的部落格
tags:
- 科技先知
- 呢喃的細雨
---

# 動機
原本就覺得blogspot佈景主題更換不容易，幾乎每篇文章都得重新調整css(堆疊太厚)，前幾年開始使用dsadStackEdit這種網站，改寫markdown格式來發布文章。但最近(2020/04)發現StackEdit網站透過GoogleDrive備份檔案的通訊協定不被Google認可，等於寫好markdown的東西無法發布於blogpost。於是開始想從blogspot跳槽至他處。為此查了一下資料，覺得GitHub pages + Jekyll這個選項不錯。
# Jekyll安裝
[Jekyll搭建個人博客](https://www.youtube.com/playlist?list=PLK2w-tGRdrj7vzX7Y-GqKPb2QPrHCYZY1)  
主要看這一段教學影片。這篇教學是建議要在local完全調整完成之後再上傳至git hub，會需要安裝Ruby/gem甚至git環境。
# Docker for Windows
不過我是M$ Windows 10，預設的cmd line其實沒有Ruby/gem套件。為此本想安裝Docker for Windows，不過根據Docker說明，在Windows 10能跑Docker前提是一定要開啟Hyper-V服務，無奈我嘗試了一整天，始終碰到Windows回報無法啟動Hyper-V服務，大概情況即可能解法如下：
[https://windowsreport.com/cant-install-hyper-v-windows-10/](https://windowsreport.com/cant-install-hyper-v-windows-10/)  
但對我來說都沒效，最終放棄Docker，犯不著為了Jekyll搞到重灌OS。
# Ruby+Gem+git on Windows
[https://jekyllrb.com/docs/installation/windows/](https://jekyllrb.com/docs/installation/windows/)  
[https://git-scm.com/download/win](https://git-scm.com/download/win)  
找到這兩篇教學，照做就對了，原先想要用Docker來玩Ruby, git似乎有點太超過了。
安裝git for windows時，意外發現有個git bash可以用，打算以作法取代Windows prompt跟PowerShell。
# Blogspot搬遷至Jekyll
最主要的原則是從blogspot將先前的文章備份為xml，再利用jekyll import轉成一篇篇html。不過實驗之後發現轉出來的效果不慎理想，且文章並非以markdown方式存放，等同於先前文章無法更換佈景主題。
# Blogspot XML to Jekyll markdown
考慮將xml或者html轉為.md(markdown)的工具，這個功能從Google search似乎沒找到，不過用github倒是找到不少類似的轉檔script。以下嘗試了幾個scripts
## https://github.com/palaniraja/blog2md 
這篇是用JavaScript編寫，按照說明必須要裝node.js，幸好目前官網直接就有Windos x64版本可以裝，然後git clone下來之後用npm install搞定補充套件之後，目前可以成功轉檔。
不過blog2md轉出來的是hugo套件的markdown語法，不確定與Jekyll的.md是否有所出入。目前blog2md轉出來的檔案似乎偏少，我在blogspot上的文章應該有155篇已發布+4篇草稿，不過目前blog2md轉出來的檔案只看到85個檔案，而且並沒有依照jekyll的規則以日期來命名.md。
## https://github.com/kennym/Blogger-to-Jekyll
使用Ruby編寫，但是其中feedzirra的library已經改名為feedjira。然後有不少API也改掉了，必須導入HTTParty library才能網路上抓xml。經過一番修改之後，終於可以轉檔成功。雖然說明文件是寫會轉成markdown，但終究功虧一簣，因為轉出來的檔案完全是html。
## https://github.com/arnaldorusso/blogger2md
使用python，有支援線上轉換，但是幾個線上的網址都已經失效。待確認
python scripts老舊，有太多encoding UTF-8問題，最終的錯誤訊息是：
UnicodeDecodeError: 'cp950' codec can't decode byte 0xe5 in position 488: illegal multibyte sequence
已經使用ConvertZ將xml轉換但似乎原本檔案就已經是UTF-8
## 心得
放棄！從2020/04/24到4/28這幾天，陸續嘗試過上述解決方案，但是大多數xml轉markdown工具都有些功能不符合我的需求，考慮過後放棄繼續嘗試。打算先使用jekyll預設轉好的html當作起點，自己一篇一篇慢慢轉檔，順便練習md語法。
# Markdown語法與編輯器
目前發現.md裡面的文字，可能因為M$ Windows的關係都是BIG5編碼，用vim打開之後基本上一堆亂碼，保險起見，針對.md檔案可能得另外專門找編輯器。在Youtube上隨便找一些markdown教學之後，發現有個vscode似乎不錯用
[http://remotemanifesto.com/jekyll-specific-css-and-web-fonts-for-latest-posts-on-homepage/](http://remotemanifesto.com/jekyll-specific-css-and-web-fonts-for-latest-posts-on-homepage/)  
[https://mmistakes.github.io/minimal-mistakes/docs/layouts/#home-page](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#home-page)
# stanlly9.github.io重生
從4月底開始陸續改寫.html，轉為.md，終於在2020-05-18完成所有html轉檔！
總計約155篇文章，順便回顧了歷年以來寫部落格文章的心路歷程。
在blogspot的[史蛋利九部落格](https://stanlly9.blogspot.com/)將會關閉，原則上會研究如何將網域轉往stanlly9.github.io

