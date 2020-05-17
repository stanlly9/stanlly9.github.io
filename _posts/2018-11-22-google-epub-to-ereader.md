---
layout: post
title: 從Google圖書到可攜式epub
author: 史蛋利九的部落格
tags:
- 網路資源
- 科技先知
---
# 前語

很多買了電子閱讀器的人，可能會發現從《Google圖書》花錢買下來的電子書籍，下載之後，居然無法在電子閱讀器底下開啟。這其實是因為這些電子書商對於保護著作財產權的一種防範措施，避免單一消費者任意散布檔案給其他未付費的讀者。目前(2018)較慣用的做法多半是為這些下載下來的檔案附加上DRM(Digital Restrictions Management)屬性，而循規蹈矩的電子閱讀器基本上就無法任意開啟受DRM保護的電子書籍檔案(即便那是你花錢買來的)。可是這可能對於以購買的消費者帶來一定程度的不便，畢竟買這類eReader有很大一部分原因就是不想看較為刺眼的電腦/手機螢幕，但購書管道又不想侷限於單一平台。畢竟貨比三家不吃虧，電子書購買平台本來就不應侷限於電子閱讀器上面的那款。以下文章提供一些簡單的做法來移除這些惱人的DRM屬性。

# 購買線上書籍並下載為acsm檔案
我個人就覺得Google圖書是個便利性高的電子書平台，畢竟只要登入Google帳戶，就可以在不同電腦/手機上開啟已經購買過的同一本電子書籍。以下範例都是以Google圖書為起點來說明步驟。
![get-a-book-from-google](/img/in-post/google-book-read.png)
購買步驟便不多做贅述，購買後，只要到[我的書籍]底下，選取書籍並下載為PDF或者ePUB檔案，便可將書籍抓到本地端(建議用電腦操作)。
![only-pdf-download-is-allowed](/img/in-post/google-book-download-pdf.png)
![download-book-as-epub](/img/in-post/google-book-download-epub.png)
不過，雖然你可能點了[下載ePub/PDF版]，就自然而然的以為下載的檔案是PDF/ePub檔案，但其實仔細看所下載來的檔案格式，其實副檔名還是acsm檔案。
![still-acsm-when-download-from-google-book](/img/in-post/google-book-acsm.png)

# 利用Adobe Digital Editions轉為PDF/ePub
此時我們需要透過Adobe Digital Editions(以下簡稱ADE)將acsm檔案轉換成一般PDF或者ePub檔案。
![Adobe-Digital-Editions](/img/in-post/adobe-digital-editions.png)
請到[Adobe官方下載ADE頁面](https://www.adobe.com/tw/solutions/ebook/digital-editions/download.html)，這套是免費軟體。安裝ADE之後，理論上就可以開啟.acsm檔案，如下：
![open-acsm-with-ADE](/img/in-post/open-acsm-with-ADE.png)
接著，有趣的事情發生了！一旦成功使用ADE開啟acsm檔案之後，這套軟體其實已經在背後幫忙把acsm轉為PDF/ePub。此時需要去把這些檔案找出來，以M$ Windows來說，一般來說都是放在：
**文件/My Digital Editions** 這個資料夾底下。

註：不確定從M$ Windows哪個版本開始，[我的文件]已經改名為[文件]
![find-ADE-export-directory](/img/in-post/use-ADE-convert-as-pdf.png)
# 移除PDF/ePub檔案的DRM屬性
雖然成功將acsm檔案轉換完成，但此時這些PDF/ePub檔案其實還是受保護狀態，無法任意轉移到其他裝置上使用。舉例來說，如果這時候就直接將檔案丟到你的eReader上面，極有可能會看到下列錯誤訊息：
![ereader-can-not-open-protected-file](/img/in-post/drm-protected.jpg)
接著，我們就可以設法使用專門軟體來移除DRM(Digital Restrictions Management)屬性，如[Epubsoft](https://www.epubsoft.com/)推出的Adobe PDF ePub DRM Removal，但畢竟試用版功能有限。此時，建議可以Google看看是否有其他不用花錢的做法。此次而言，我是到github上面找到一套open source tools具備這個功能, [Codex](https://github.com/jscholes/codex)；而且，2018的當下，看起來作者還有在維護(使用github搜尋可以觀察最後一次更新程式的時間)。
如對原始碼沒啥興趣可以直接到下列網址下載安裝檔：http://jscholes.net/project/codex/
Windows版本的Codex畫面如下
![Codex-window](/img/in-post/codex-window.png)
此時可以按[Add files ...]選擇 [**剛才透過ADE幫忙轉換成PDF/ePub的檔案**] (重點：Codex不支援選acsm，但先前已利用ADE轉回較通用的PDF/ePub檔案)。
然後按下 [Remove DRM] 按鈕，此時應該會出現轉換畫面如下：
![removing-drm](/img/in-post/removing-drm.png)
轉換完成後，Codex大致上會顯示轉換成果，下列畫面是同時移除2個檔案的DRM的範例：
![drm-removed-processed-files](/img/in-post/processed-file-drm-removed.png)
Codex預設會去查詢這份檔案的作者，並為其建立資料夾，然後把移除DRM後的檔案放到這個資料夾裡面，當Codex無法讀出作者的時候，通常會顯示Unknown。
我自己的使用經驗來說，Codex預設應該是把輸出檔案資料夾放在下列資料夾：
**文件/eBooks/{Author}/xxx**
此時基本上已經大功告成了！
# 將PDF轉為epub
如果你的eReader不支援PDF格式，也可以利用Codex將PDF轉成較為通用的epub格式。作法很類似Remove DRM，就是選好Output format為ePub，然後按下 [**Convert**] 就可以了。
![converting-pdf-to-epub](/img/in-post/convert-epub-remove-drm.png)
轉完之後，一樣是到 [文件/eBooks/]底下找檔案。
移除DRM之後，eReader就可以正常開啟檔案了。
![ereader-can-open-file-that-drm-was-removed](/img/in-post/drm-unlocked.jpg)

