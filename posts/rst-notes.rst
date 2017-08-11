.. title: reStructuredText Notes
.. slug: reStructuredText-notes
.. date: 2017-02-12 21:06:35 UTC+08:00
.. tags: python, nikola, mathjax
.. category: notes
.. link:
.. description:
.. type: text


.. sectnum::

.. contents::

.. TEASER_END

.. class:: alert alert-info pull-right

.. admonition:: 参考

   写本文时 Nikola 版本为 7.8.3. 参考链接：

   1. `reStructuredText Markup Specification`_

   #. `reStructuredText Primer`_

   #. `reStructuredText Quick Reference`_

   #. `reStructuredText Directives`_

   #. `The Nikola Handbook`_

   #. `The Nikola Handbook Source`_



章节结构
==========

- 常用符号：

  ``= - ` : . ' " ~ ^ _ * + #``

- 所有可用符号：

  ``! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~``

Transition 
------------

Transition 符号由4个或以上 `章节结构`_ 里允许用的符号组成，都会被渲染成水平线。如下面的水平线是由 ``####`` 渲染成的。

####

Topic 结构
--------------

.. topic:: Topic Title Example

   这是 topic 第一段。

   这是 topic 的第二段。

``topic`` 结构一般用在文章开头，或某段开头，或是 transition 开始时，用于点明主题。上面这个 topic 的例子的原文为：

::

  .. topic:: Topic Title Example

     这是 topic 第一段。

     这是 topic 的第二段。

rst 常用语法
================

常见样式
------------

+----------------------------------------------------------+----------------------------------------------------------+
|  ::                                                      |                                                          |
|                                                          |                                                          |
|    *倾斜*                                                | *倾斜*                                                   |
|                                                          |                                                          |
|    **加粗**                                              | **加粗**                                                 |
|                                                          |                                                          |
|    ``inline literal``                                    | ``inline literal``                                       |
|                                                          |                                                          |
|    注释由两个点加空格起头，渲染后不会显示：              | 注释由两个点加空格起头，渲染后不会显示：                 |
|                                                          |                                                          |
|    .. 这里是注释，将不会被显示。                         | .. 这里是注释，将不会被显示。                            |
+----------------------------------------------------------+----------------------------------------------------------+
|  ::                                                      |                                                          |
|                                                          |                                                          |
|    - 直接使用网址，以http或https起头：                   | - 直接使用网址，以http或https起头：                      |
|                                                          |                                                          |
|      http://yongchen.org                                 |   http://yongchen.org                                    |
|                                                          |                                                          |
|    - 用文字表示链接 I：                                  | - 用文字表示链接 I：                                     |
|                                                          |                                                          |
|      `my site <http://yongchen.org>`_                    |   `my site <http://yongchen.org>`_                       |
|                                                          |                                                          |
|    - 用文字表示链接 II：                                 | - 用文字表示链接 II：                                    |
|                                                          |                                                          |
|      `my site`_                                          |   `my site`_                                             |
|                                                          |                                                          |
|      .. _my site: http://yongchen.org                    |   .. _my site: http://yongchen.org                       |
|                                                          |                                                          |
|    - 所有的章节标题都可以被引用：                        | - 所有的章节标题都可以被引用：                           |
|                                                          |                                                          |
|      `章节结构`_                                         |   `章节结构`_                                            |
+----------------------------------------------------------+----------------------------------------------------------+
|  ::                                                      | 文字，图片等对象的替代 (substitution) :                  |
|                                                          |                                                          |
|    The |Nikola| image is shown here.                     | The |Nikola| image is shown here.                        |
|                                                          |                                                          |
|    .. |Nikola| image:: /images/nikola.png                | .. |Nikola| image:: /images/nikola.png                   |
|                :align: middle                            |             :align: middle                               |
|                :width: 30 (网页中我们常用480)            |             :width: 30                                   |
|                                                          |                                                          |
|    ``image`` 中的 ``align`` 选项可以是 ``top``,          | ``image`` 中的 ``align`` 选项可以是 ``top``,             |
|    ``middle``, ``bottom``.                               | ``middle``, ``bottom``.                                  |
|                                                          |                                                          |
|    另外，比 ``image`` 功能更强大，``figure`` 可以包括    | 另外，比 ``image`` 功能更强大，``figure`` 可以包括       |
|    （也可省略）标题和图例。                              | （也可省略）标题和图例。                                 |
|    ``align`` 可以是 ``left``, ``center``, ``right``.     | ``align`` 可以是 ``left``, ``center``, ``right``.        |
|                                                          |                                                          |
|    .. figure:: /images/nikola.png                        | .. figure:: /images/nikola.png                           |
|       :align: center                                     |    :align: center                                        |
|       :figwidth: 300                                     |    :figwidth: 300                                        |
|                                                          |                                                          |
|       This is the caption of the figure. 标题只能有一段。|    This is the caption of the figure. 标题只能有一段。   |
|                                                          |                                                          |
|       所有出现在标题段之后的文字和其它内容都视为图例。   |    所有出现在标题段之后的文字和其它内容都视为图例。      |
|       例如这一段文字以及下面的表格：                     |    例如这一段文字以及下面的表格：                        |
|                                                          |                                                          |
|       +-----------------------+-----------------------+  |    +-----------------------+-----------------------+     |
|       | Symbol                | Meaning               |  |    | Symbol                | Meaning               |     |
|       +=======================+=======================+  |    +=======================+=======================+     |
|       | .. image:: tent.png   | Campground            |  |    | .. image:: tent.png   | Campground            |     |
|       +-----------------------+-----------------------+  |    +-----------------------+-----------------------+     |
|       | .. image:: waves.png  | Lake                  |  |    | .. image:: waves.png  | Lake                  |     |
|       +-----------------------+-----------------------+  |    +-----------------------+-----------------------+     |
|       | .. image:: peak.png   | Mountain              |  |    | .. image:: peak.png   | Mountain              |     |
|       +-----------------------+-----------------------+  |    +-----------------------+-----------------------+     |
+----------------------------------------------------------+----------------------------------------------------------+
|  ::                                                      | 脚标，下面的例子中也可以使用 # 自动计数                  |
|                                                          |                                                          |
|    footnote reference [1]_                               | footnote reference [1]_                                  |
|                                                          |                                                          |
|    .. [1] A footnote example linked to [1].              | .. [1] A footnote example linked to [1].                 |
+----------------------------------------------------------+----------------------------------------------------------+
|  ::                                                      | 文献引用，和脚标用法类似。                               |
|                                                          |                                                          |
|    citation reference [CIT2002]_                         | citation reference [CIT2002]_                            |
|                                                          |                                                          |
|    .. [CIT2002] A citation example.                      | .. [CIT2002] A citation example.                         |
+----------------------------------------------------------+----------------------------------------------------------+
|  ::                                                      | 使用 backslash 显示那些特殊字符。                        |
|                                                          |                                                          |
|    - \*星号*                                             | - \*星号*                                                |
|                                                          |                                                          |
|    - \``代码符号``                                       | - \``代码符号``                                          |
|                                                          |                                                          |
|    - 反斜杠 \\                                           | - 反斜杠 \\                                              |
+----------------------------------------------------------+----------------------------------------------------------+
|  ::                                                      |                                                          |
|                                                          |                                                          |
|    Lists:                                                | Lists:                                                   |
|                                                          |                                                          |
|    - item 1. 第一项前和最后一项后必须各留出一空行.       | - item 1. 第一项前和最后一项后必须各留出一空行.          |
|    - item 2. List 由 "*", "+", "-" 等符号引导。          | - item 2. List 由 "*", "+", "-" 等符号引导。             |
|                                                          |                                                          |
|    - item 3. 中间各项之间可留空行也可省略.               | - item 3. 中间各项之间可留空行也可省略.                  |
|                                                          |                                                          |
|      1. nested item 1. 此前又须留出一空行。数字型的list接|   1. nested item 1. 此前又须留出一空行。数字型接         |
|         受这几种格式：                                   |      受这几种格式：                                      |
|                                                          |                                                          |
|         a. 阿拉伯数字 1, 2, 3 ...                        |      a. 阿拉伯数字 1, 2, 3 ...                           |
|         #. 大写或小写字母 A, B, ..., Z. a, b, ..., z.    |      #. 大写或小写字母 A, B, ..., Z. a, b, ..., z.       |
|         #. 大写或小写罗马数字 I, II, ... 或 i, ii, ...   |      #. 大写或小写罗马数字 I, II, ... 或 i, ii, ...      |
|                                                          |                                                          |
|    Definition Lists: 词或变量                            | Definition Lists: 词或变量                               |
|                                                          |                                                          |
|    what                                                  | what                                                     |
|        Definition lists associate a term with a          |     Definition lists associate a term with a             |
|        definition.                                       |     definition.                                          |
|                                                          |                                                          |
|    lines : string                                        | lines : string                                           |
|        List of one-line strings without newlines.        |     List of one-line strings without newlines.           |
|                                                          |                                                          |
|    Field Lists:                                          | Field Lists:                                             |
|                                                          |                                                          |
|    :Authors:                                             | :Authors:                                                |
|        Tony J. (Tibs) Ibbs,                              |     Tony J. (Tibs) Ibbs,                                 |
|        David Goodger                                     |     David Goodger                                        |
|                                                          |                                                          |
|        (and sundry other good-natured folks)             |     (and sundry other good-natured folks)                |
|                                                          |                                                          |
|    :Version: 1.0 of 2001/08/08                           | :Version: 1.0 of 2001/08/08                              |
|                                                          |                                                          |
|    :Dedication: To my father.                            | :Dedication: To my father.                               |
|                                                          |                                                          |
|    Option Lists:                                         | Option Lists:                                            |
|                                                          |                                                          |
|    -a file    command-line option "a"                    | -a file    command-line option "a"                       |
|    --input=file    long options can also have arguments  | --input=file    long options can also have arguments     |
|    /V    DOS/VMS-style options too                       | /V    DOS/VMS-style options too                          |
+----------------------------------------------------------+----------------------------------------------------------+
| ::                                                       | **code**: 可选参数 ``number-lines : [start line number]``|
|                                                          | Nikola 现在已使用 rst 的 ``code`` 代替以前 Nikola 使用的 |
|                                                          | ``code-block`` 语法. 另外引用整个文件可以用 `listing`_.  |
|                                                          |                                                          |
|   .. code:: python                                       | .. code:: python                                         |
|                                                          |                                                          |
|      def my_function():                                  |    def my_function():                                    |
|          "just a test"                                   |        "just a test"                                     |
|          print 8/2                                       |        print 8/2                                         |
|                                                          |                                                          |
|                                                          | **gist**: 引用 GitHub 的 gist (效果略).                  | 
|                                                          |                                                          |
|   .. gist:: 2395284                                      |                                                          |
+----------------------------------------------------------+----------------------------------------------------------+
|  ::                                                      |                                                          |
|                                                          |                                                          |
|    Literal Blocks:                                       | Literal Blocks:                                          |
|                                                          |                                                          |
|    ::                                                    | ::                                                       |
|                                                          |                                                          |
|      Whitespace, newlines, blank lines, and all kinds of |   Whitespace, newlines, blank lines, and all kinds of    |
|      markup is preserved by literal blocks.              |   markup is preserved by literal blocks.                 |
|                                                          |                                                          |
|    Per-line quoting can also be used on unindented       | Per-line quoting can also be used on unindented          |
|    literal blocks (顶格写时每行的 ``>`` 符号不可少)::    | literal blocks (顶格写时每行的 ``>`` 符号不可少)::       |
|                                                          |                                                          |
|    > Useful for quotes from email and                    | > Useful for quotes from email and                       |
|    > for Haskell literate programming.                   | > for Haskell literate programming.                      |
|                                                          |                                                          |
|    Block Quotes:                                         | Block Quotes:                                            |
|                                                          |                                                          |
|    Block quotes 格式为相对前一行进行缩进，               | Block quotes 格式为相对前一行进行缩进，                  |
|                                                          |                                                          |
|        Block quotes 仅仅是缩进，并不会像 literal blocks  |     Block quotes 仅仅是缩进，并不会像 literal blocks     |
|        或是 line blocks 那样完全照搬格式。例如这一段在渲 |     或是 line blocks 那样完全照搬格式。例如这一段在渲    |
|        染后的排版断行不会完全和原文一模一样。            |     染后的排版断行不会完全和原文一模一样。               |
|                                                          |                                                          |
|            Nested block quotes.                          |         Nested block quotes.                             |
|                                                          |                                                          |
|    Line Blocks: （注意渲染后的样式与普通文字一样）       | Line Blocks: （注意渲染后的样式与普通文字一样）          |
|                                                          |                                                          |
|    | Line blocks are useful for addresses,               | | Line blocks are useful for addresses,                  |
|    | verse, and adornment-free lists.                    | | verse, and adornment-free lists.                       |
|                                                          |                                                          |
|    | Each new line begins with a                         | | Each new line begins with a                            |
|    | vertical bar ("|").                                 | | vertical bar ("|").                                    |
|    |     Line breaks and initial indents                 | |     Line breaks and initial indents                    |
|    |     are preserved.                                  | |     are preserved.                                     |
|    | Continuation lines are wrapped                      | | Continuation lines are wrapped                         |
|      portions of long lines; they begin                  |   portions of long lines; they begin                     |
|      with spaces in place of vertical bars.              |   with spaces in place of vertical bars.                 |
|                                                          |                                                          |
|    Doctest Blocks: 以 ``<<<`` 打头                       | Doctest Blocks: 以 ``<<<`` 打头                          |
|                                                          |                                                          |
|    >>> print "This is a doctest block."                  | >>> print "This is a doctest block."                     |
|    This is a doctest block.                              | This is a doctest block.                                 |
+----------------------------------------------------------+----------------------------------------------------------+
| ::                                                       |                                                          |
|                                                          |                                                          |
|   **Admonitions**: 包括 "attention", "caution", "danger",| **Admonitions**: 包括 "attention", "caution", "danger",  |
|    "error", "hint", "important", "note", "tip", "warning"| "error", "hint", "important", "note", "tip", "warning"   |
|    以及一般性的 "admonition"                             | 以及一般性的 "admonition" (参考 `Admonitions`_)          |
|                                                          |                                                          |
|   .. DANGER::                                            | .. DANGER::                                              |
|      Beware killer rabbits!                              |    Beware killer rabbits!                                |
|                                                          |                                                          |
|   .. admonition:: And, by the way...                     | .. admonition:: And, by the way...                       |
|                                                          |                                                          |
|      You can make up your own admonition too.            |    You can make up your own admonition too.              |
+----------------------------------------------------------+----------------------------------------------------------+
| ::                                                       |   表格：                                                 |
|                                                          |                                                          |
|   +------------+------------+-----------+                |   +------------+------------+-----------+                |
|   | Header 1   | Header 2   | Header 3  |                |   | Header 1   | Header 2   | Header 3  |                |
|   +============+============+===========+                |   +============+============+===========+                |
|   | body row 1 | column 2   | column 3  |                |   | body row 1 | column 2   | column 3  |                |
|   +------------+------------+-----------+                |   +------------+------------+-----------+                |
|   | body row 2 | Cells may span columns.|                |   | body row 2 | Cells may span columns.|                |
|   +------------+------------+-----------+                |   +------------+------------+-----------+                |
|   | body row 3 | Cells may  | - Cells   |                |   | body row 3 | Cells may  | - Cells   |                |
|   +------------+ span rows. | - contain |                |   +------------+ span rows. | - contain |                |
|   | body row 4 |            | - blocks. |                |   | body row 4 |            | - blocks. |                |
|   +------------+------------+-----------+                |   +------------+------------+-----------+                |
|                                                          |                                                          |
|   =====  =====  ======                                   |   =====  =====  ======                                   |
|      Inputs     Output                                   |      Inputs     Output                                   |
|   ------------  ------                                   |   ------------  ------                                   |
|     A      B    A or B                                   |     A      B    A or B                                   |
|   =====  =====  ======                                   |   =====  =====  ======                                   |
|   False  False  False                                    |   False  False  False                                    |
|   True   False  True                                     |   True   False  True                                     |
|   False  True   True                                     |   False  True   True                                     |
|   True   True   True                                     |   True   True   True                                     |
|   =====  =====  ======                                   |   =====  =====  ======                                   |
+----------------------------------------------------------+----------------------------------------------------------+
| ::                                                       | **csv-table** (`CSV Table`_):                            |
|                                                          |                                                          |
|   .. csv-table:: Frozen Delights!                        | .. csv-table:: Frozen Delights!                          |
|      :header: "Treat", "Quantity", "Description"         |    :header: "Treat", "Quantity", "Description"           |
|      :widths: auto                                       |    :widths: auto                                         |
|      :align: center                                      |    :align: center                                        |
|                                                          |                                                          |
|      "Albatross", 2.99, "On a stick!"                    |    "Albatross", 2.99, "On a stick!"                      |
|      "Crunchy Frog", 1.49, "If we took the bones         |    "Crunchy Frog", 1.49, "If we took the bones           |
|      out, it wouldn't be crunchy, now would it?"         |    out, it wouldn't be crunchy, now would it?"           |
|      "Gannet Ripple", 1.99, "On a stick!"                |    "Gannet Ripple", 1.99, "On a stick!"                  |
|                                                          |                                                          |
|                                                          | **list-table** (`List Table`_):                          |
|                                                          |                                                          |
|   .. list-table:: Frozen Delights!                       | .. list-table:: Frozen Delights!                         |
|      :widths: auto                                       |    :widths: auto                                         |
|      :header-rows: 1                                     |    :header-rows: 1                                       |
|      :stub-columns: 0                                    |    :stub-columns: 0                                      |
|      :align: center                                      |    :align: center                                        |
|                                                          |                                                          |
|      * - Treat                                           |    * - Treat                                             |
|        - Quantity                                        |      - Quantity                                          |
|        - Description                                     |      - Description                                       |
|      * - Albatross                                       |    * - Albatross                                         |
|        - 2.99                                            |      - 2.99                                              |
|        - On a stick!                                     |      - On a stick!                                       |
|      * - Crunchy Frog                                    |    * - Crunchy Frog                                      |
|        - 1.49                                            |      - 1.49                                              |
|        - If we took the bones out, it wouldn't be        |      - If we took the bones out, it wouldn't be          |
|          crunchy, now would it?                          |        crunchy, now would it?                            |
|      * - Gannet Ripple                                   |    * - Gannet Ripple                                     |
|        - 1.99                                            |      - 1.99                                              |
|        - On a stick!                                     |      - On a stick!                                       |
|                                                          |                                                          |
|                                                          |                                                          |
|                                                          |                                                          |
+----------------------------------------------------------+----------------------------------------------------------+

代码高亮
------------

Nikola 中的代码高亮都是借用 ``Pygments`` 实现的。其支持的语言及简写参见 `Available lexers`_. 常用的有以下几种：

.. list-table:: 常见编程语言及简写
   :widths: auto
   :header-rows: 1
   :stub-columns: 1
   :align: left

   * - Programming language
     - Short names
     - Filenames
   * - C
     - c
     - \*.c, \*.h, \*.idc
   * - C++
     - cpp, c++
     - \*.cpp, \*.hpp, \*.c++, \*.h++, \*.cc, \*.hh, \*.cxx, \*.hxx, \*.C, \*.H, \*.cp, \*.CPP
   * - C#
     - csharp, c#
     - \*.cs
   * - Mathematica
     - mathematica, mma, nb
     - \*.nb, \*.cdf, \*.nbp, \*.ma
   * - CSS
     - css
     - \*.css
   * - Json
     - json
     - \*.json
   * - HTML
     - html
     - \*.html, \*.htm, \*.xhtml, \*.xslt
   * - XML
     - xml
     - \*.xml, \*.xsl, \*.rss, \*.xslt, \*.xsd, \*.wsdl, \*.wsf
   * - JavaScript
     - js, javascript
     - \*.js, \*.jsm
   * - Julia
     - julia, jl
     - \*.jl
   * - Julia Console
     - jlcon
     - None
   * - Java
     - java
     - \*.java
   * - LaTeX
     - tex, latex
     - \*.tex, \*.aux, \*.toc
   * - Matlab
     - matlab
     - \*.m
   * - Python
     - python, py, sage
     - \*.py, \*.pyw, \*.sc, SConstruct, SConscript, \*.tac, \*.sage
   * - Python Console
     - pycon
     - None
   * - Bash
     - bash, sh, ksh, zsh, shell
     - \*.sh, \*.ksh, \*.bash, \*.ebuild, \*.eclass, \*.exheres-0, \*.exlib, \*.zsh, .bashrc, bashrc, .bash\*, bash\*, zshrc, .zshrc, PKGBUILD
   * - Console
     - console, shell-session
     - \*.sh-session, \*.shell-session
   * - Batch
     - bat, batch, dosbatch, winbatch
     - \*.bat, \*.cmd
   * - MSDOS Session
     - doscon
     - None
   * - PowerShell Session
     - ps1con
     - None


目录结构
-----------

目录用 ``contents`` 生成。参考 `The Nikola Handbook Source`_ 中的写法：

::

  .. class:: alert alert-info pull-right

  .. contents::


章节自动编号
---------------  

在文章开始前使用 `sectnum`_ 使章节结构标题自动编号，编号在 **contents** 目录里也会显示。

::

  .. sectnum::


侧边栏
-------------

.. sidebar:: Sidebar Title
   :subtitle: Optional Sidebar Subtitle

   Subsequent indented lines comprise
   the body of the sidebar, and are
   interpreted as body elements.

侧边栏由 ``sidebar`` 实现。右侧的侧边栏代码为：

::

  .. sidebar:: Sidebar Title
    :subtitle: Optional Sidebar Subtitle

    Subsequent indented lines comprise
    the body of the sidebar, and are
    interpreted as body elements.

####

Nikola 常用语法
==================

+----------------------------------------------------------+----------------------------------------------------------+
| ::                                                       |                                                          |
|                                                          |                                                          |
|   **Math**: 在 ``tags`` 中添加 ``mathjax`` 启用 LaTeX.   | **Math**: 在 ``tags`` 中添加 ``mathjax`` 启用 LaTeX.     |
|                                                          |                                                          |
|   - inline math:                                         | - inline math:                                           |
|                                                          |                                                          |
|     Euler’s formula: :math:`e^{ix} = \cos x + i\sin x`   |   Euler’s formula: :math:`e^{ix} = \cos x + i\sin x`     |
|                                                          |                                                          |
|   - displayed math:                                      | - displayed math:                                        |
|                                                          |                                                          |
|     .. math::                                            |   .. math::                                              |
|                                                          |                                                          |
|        \int \frac{dx}{1+ax}=\frac{1}{a}\ln(1+ax)+C       |      \int \frac{dx}{1+ax}=\frac{1}{a}\ln(1+ax)+C         |
+----------------------------------------------------------+----------------------------------------------------------+
| ::                                                       |                                                          |
|                                                          |                                                          |
|   **Media**: 可直接插入Vimeo, Youtute, Soundcloud.       | **Media**: 可直接插入Vimeo, Youtute, Soundcloud.         |
|                                                          |                                                          |
|   .. youtube:: 8N_tupPBtWQ                               | .. youtube:: 8N_tupPBtWQ                                 |
|      :align: center                                      |    :align: center                                        |
|                                                          |                                                          |
|   .. vimeo:: 20241459                                    | .. vimeo:: 20241459                                      |
|      :height: 240                                        |    :height: 240                                          |
|      :width: 320                                         |    :width: 320                                           |
|                                                          |                                                          |
|   .. soundcloud:: 78131362                               | .. soundcloud:: 78131362                                 |
+----------------------------------------------------------+----------------------------------------------------------+




.. _reStructuredText Markup Specification: http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html
.. _reStructuredText Primer: http://www.sphinx-doc.org/en/stable/rest.html
.. _reStructuredText Quick Reference: http://docutils.sourceforge.net/docs/user/rst/quickref.html
.. _reStructuredText Directives: http://docutils.sourceforge.net/docs/ref/rst/directives.html
.. _The Nikola Handbook: https://getnikola.com/handbook.html
.. _The Nikola Handbook Source: https://getnikola.com/handbook.txt

.. _CSV Table: http://docutils.sourceforge.net/docs/ref/rst/directives.html#id4
.. _List Table: http://docutils.sourceforge.net/docs/ref/rst/directives.html#list-table
.. _Available lexers: http://pygments.org/docs/lexers/
.. _sectnum: http://docutils.sourceforge.net/docs/ref/rst/directives.html#automatic-section-numbering
.. _listing: https://getnikola.com/handbook.html#listing
.. _Admonitions: http://docutils.sourceforge.net/docs/ref/rst/directives.html#admonitions