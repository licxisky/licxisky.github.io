---
title: Chrome 下如何实现免预览打印
urlname: Preview-free-printing
date: 2018-03-23 13:05:23
tags:
- Chrome
- Printer
---
说明
==

突然入手一个小项目，要求在网页上点击打印按钮打印机就出打印好的纸，思前想后，找了好多资料，终于找到一个比较通用的方法


<!--more-->


方法
==

1.  在地址栏敲: about:flags ,打开设置界面:  
    停用:Enable Print Preview Registration Promos Windows, Linux, Chrome OS  
    ![ChromePrintPreview.png](/uploads/ChromePrintPreview.png "ChromePrintPreview.png")
2.  Chrome快捷方式增加: --kiosk-printing  
    ![ChromePrintKiosk.png](/uploads/ChromePrintKiosk.png "ChromePrintKiosk.png")

其他
==

其他还有一些比如使用插件之类的方法一般而言都有限制，总结而来，这种方案快捷方便