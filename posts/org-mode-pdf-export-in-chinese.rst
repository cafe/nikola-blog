.. title: Org-Mode PDF Export in Chinese
.. slug: org-mode-pdf-export-in-chinese
.. date: 2016-04-25 12:24:11 UTC+08:00
.. tags: org-mode, emacs
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

Simple solution
===============

Refer to http://www.xuebuyuan.com/2136832.html

Add the following to ``dotspacemacs/user-config()`` block of
``.spacemacs`` file:

.. TEASER_END

.. code:: clojure

        (setq org-latex-pdf-process '("xelatex -interaction nonstopmode %f"
                                      "xelatex -interaction nonstopmode %f"))

When your org file has Chinese characters, just put

.. code::

        #+LATEX_HEADER: \usepackage{xeCJK}
        #+LATEX_HEADER: \setCJKmainfont{SimSun}

at the head of your ``.org`` file.

Note
====

Other methods on the internet require lots of tweaks like style
customization of code blocks, which are not needed here.

