.. title: 小米手机连接电脑
.. slug: xiao-mi-shou-ji-lian-jie-dian-nao
.. date: 2017-02-09 14:51:43 UTC+08:00
.. tags: 手机
.. category: OS
.. link:
.. description:
.. type: text

我们要将手机连接到电脑上，并用电脑访问手机上的文件，如复制、删除歌曲及图片文件等。
但小米助手目前几乎被官方放弃，只支持安卓5.0及以前的系统。

使用手机：小米Max，安卓版本：7.0， 国际版。

下面我们用安卓的USB调试模式连接。

.. TEASER_END

步骤
=====

1. 若尚未开启USB调试功能，需要解锁开发者选项

   a) ``Settings`` > ``About phone`` (图中1)

      |About phone|

   b) 多次点击 ``MIUI version`` 一项 (图中2)

      |MIUI version|

   c) ``Settings`` > ``Additional settings`` > ``Developer options`` (图中3)

      |Developer options|

   d) 分别开启 ``Developer options`` 与 ``USB debugging`` 选项 (图中4与5)

      |USB debugging|

2. ``Developer options`` > ``Select USB Configuration`` > ``MTP (Media Transfer Protocol)``
   (图中7) 这时插上电脑一般就可以当作U盘使用了。但有时还是发现在电脑上查看时，手机盘里什么内容都看不到的情况。
   这时只要重新在 ``Select USB Configuration`` 中先切换到别的模式，如充电模式，再切回MTP模式就可以了。有时插上USB或切换模式后会在顶栏出现
   提示 (图中6) 只要再确认一下MTP模式即可 (图中8)。这时就可以在电脑上看到文件了。

   |MTP mode|
   |Choose mode|

.. |About Phone| image:: /images/MiMax-USB-1-AboutPhone.png
                 :width: 480
.. |MIUI version| image:: /images/MiMax-USB-2-UnlockDeveloperOptions.png
                  :width: 480
.. |Developer options| image:: /images/MiMax-USB-3-DeveloperOptions.png
                       :width: 480
.. |USB debugging| image:: /images/MiMax-USB-4-5-DebuggingMode.png
                   :width: 480
.. |MTP mode| image:: /images/MiMax-USB-6-7-USBConfigInterface.png
              :width: 480
.. |Choose mode| image:: /images/MiMax-USB-8-ChooseMode.png
                 :width: 480
