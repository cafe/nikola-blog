.. title: LyX Settins on Windows
.. slug: lyx-settins-on-windows
.. date: 2016-04-25 12:22:49 UTC+08:00
.. tags: latex
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

Main settings
=============

Refer to
http://andnot.farbox.com/post/ke-yan-bi-ji/lyxzhong-wen-pei-zhi-tips

Document->Settings…

.. TEASER_END

-  ->Document Class->Document class: Chinese Article (CTeX), ->Custom:
   UTF8

-  ->Language->Encoding->Other: Unicode (XeTeX) (utf8)

-  ->Output->Output Format->Default Output Format: PDF(XeTeX)

-  ->LaTeX Preamble:
   ``\DeclareRobustCommand\nobreakspace{\leavevmode\nobreak\ } % redefine nobreakspace to avoid XeTeX errors``

-  ->PDF Properties: check Use Hyperrref Support, ->Bookmarks: check
   Generate Bookmarks (ToC), Numbered bookmarks, Open bookmark tree

To aligh the section title in CTeX
==================================

Document->Settings…->LaTeX Preamble:

.. code:: latex

        \makeatletter

        \g@addto@macro{\CTEX@section@format}{\raggedright}

        \makeatother

