---
layout: post
title: iOS StoryBoard统一修改字体颜色,字号
date: 2018-06-15  
toc: true
tags: iOS
---

当版本迭代时,UI让统一修改字体颜色或者字号.如果纯代码,肯定是先定义宏,直接修改宏,so easy. 但是,如果用storyboard让你修改字体颜色或者字号,难道要一个页面也个页面改?那得改到猴年马月?
我也遇到了这个问题,别慌,本质storyboard也是xml文件.当然是打开源码开始改咯


![屏幕快照 2017-10-18 下午2.24.15.png](http://upload-images.jianshu.io/upload_images/2835144-63230ecf566cdae6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![屏幕快照 2017-10-18 下午2.24.02.png](http://upload-images.jianshu.io/upload_images/2835144-7a91d1d27002d67b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

搜索对应颜色,然后把色值换为对应的色值,比如(20,20,20), 在storyboard中
20/255. = 0.0784313725, 反正保留对应的小数精确到的数位越小,色值越精确.就像(159.999,159.999,159.999)和(160.0,160.0,160.0)转换成颜色之后,肉眼根本看不出来色值差别  然后替换
red="0.0784313725" green="0.0784313725" blue="0.0784313725"
如果想改字体,或者其他的,在源码中改其他的就行了
希望对你们有帮助,不放弃storyboard!!!


总阅读(<span id="busuanzi_value_page_pv"></span>)