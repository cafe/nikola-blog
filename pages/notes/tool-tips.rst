.. title: Tool Tips
.. slug: tool-tips
.. date: 2016-07-24 14:11:59 UTC+08:00
.. tags: algorithm, software, web
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

中国可备案的域名后缀(gTLD)
=====================================
访问 http://www.miitbeian.gov.cn/publish/query/indexFirst.action 页面"域名类型"一栏可以查看可以备案的通用域名, 目前(2016.8.8)可备案的gTLD如下:
com, net, org, edu, gov, biz, info, name, aero, arpa, asia, cat, coop, int, jobs, mil, mobi, museum, pro, tel, travel, wang, citic, ren, top, sohu, xin

Capitalize The First Letter
=======================================
将一个句子里所有单词首字母大写, 使用Excel中的 ``PROPER()`` 函数即可.

视频只听声音不看画面(禁止画面播放)
======================================
使用VLC, Video->Video Track->Disable, 并且 Tools->Preferences->Video->Disable "Enable Video" option. 这样就可以听视频了.

拼音转汉字(批量)
=======================
大多数输入法可以做到单个拼音转汉字. 批量转换可借助爱词霸翻译 http://fy.iciba.com/ 等在线转换, 这种方法可以用于区别域名中的自然双拼. 后来尝试过其它几个在线翻译, 发现还是Google翻译最好用. 只用选择Chinese->Chinese就可以了. 因为Google翻译后的结果会粘成一行, 为了使结果按行排列, 可以在每个拼音后加上斜杠 ``/`` 或反斜杠符号(或逗号等其它标点符号)再回车.

Mathematica提高精度
===========================
一些算法如NMinimize, FindRoot都会受WorkingPrecision的影响. 可以在这些算法当中单独指定WorkingPrecision的值. 如果想要指定一个全局的工作精度值, 可以使用下面的方法(来自http://mathematica.stackexchange.com/questions/38114/how-to-set-the-working-precision-globally-minprecision-does-not-work):

.. Code::
    
    $PreRead = (# /. 
     s_String /; 
       StringMatchQ[s, NumberString] && 
        Precision@ToExpression@s == MachinePrecision :> 
      s <> "`50." &);


这样设置后, 之后的所有计算都会是指定的50位精度.

测试网站是否被墙
=============================
测试网站是否可以被中国用户访问, 可以使用360奇云测 http://ce.cloud.360.cn, 如果网速为0的地区就说明那个地方不能访问. 如果中国大部分地区都没有速度, 就极可能是被墙了.