.. title: Build Github Pages with Nikola
.. slug: build-github-pages-with-nikola
.. date: 2016-04-26 12:56:35 UTC+08:00
.. tags: github, python, nikola, web
.. category: notes
.. link:
.. description:
.. type: text
.. author: YONG

Introduction
============

静态网站生成工具(static site generator)非常多,
在\ `这里 <https://www.staticgen.com/>`__
就可以看到开源的众多静态网站生成工具. 不少工具都有它们各自的特点,
比如Hugo用golang编写, 在编译网页时速度比其它框架更快, 但缺点也比较明显,
做个性化扩展比较麻烦. 这里选择Nikola是考虑到它是由Python编写,
编译速度也比常见的Jekyll等要快不少, 且开发活跃,
被很多科研人员选作博客工具. 我比较看重的Nikola特性有:

.. TEASER_END

-  支持LaTeX数学公式(via MathJax)
-  原生支持多种文档类型, 包括:

   -  reStructuredText (``.rst``, ``.txt``, 此为默认格式, 故 ``.txt``
      文件也是以reStructuredText格式来读取的)
   -  markdown (``.md``)
   -  Jupyter/IPython Notebook (``.ipynb``)
   -  HTML (``.html``)
   -  PHP (``.php``)
   -  Pandoc支持的格式, 如Textile, LaTeX, Emacs Org-Mode, MS Word等
      (Pandoc需要手动开启支持, 默认关闭因可能会与已有格式冲突)

-  能过插件支持更多类型文档, 例如 Emacs Org-Mode, reST with HTML 5
   output 等

除此之外, 它还有很多其它特点, 比如提供image gallery, image slideshow
模板, 以及个性化的输出路径定制等.

配置参考\ `官方指导 <https://getnikola.com/getting-started.html>`__\ 和\ `手册 <https://getnikola.com/handbook.html>`__,
本文针对Windows和Anaconda作更详细的说明.

安装Nikola
==========

-  选择一: 直接安装Python

   -  安装Python3: 打开Python官网安装32位python3.
      (即使是64位系统也推荐使用兼容性较好的32位python). 安装完后
      ``python --version`` 查看版本信息.
   -  安装 ``virtualenv``: 进入到python安装目录
      ``AppData\Local\Programs\Python\Python35-32``,
      ``python -m pip install virtualenv``
   -  新建一个虚拟环境用于安装nikola(当然也可以省掉这步,
      直接把nikola安装在global环境下)

      .. code:: shell

          virtualenv nikola
          cd nikola/Scripts
          activate.bat

      说明: 创建一个叫做nikola的虚拟环境. 这里视情况不同,
      如果提示命令失败可以尝试使用 ``virtualenv3``, ``virtualenv-3.x``
      (其中x为python版本), 或者 ``virtualenv -p /usr/bin/python3``.
      因win下没有source命令, 故使用.bat文件进行激活这个虚似环境.
      Linux下使用 ``source bin/activate`` 命令. 执行完上面命令,
      此时命令行左侧会出现 ``(nikola)``,
      表明当前的命令将会在这个虚拟环境下执行.

   -  在 ``(nikola)`` 环境下安装 ``lxml`` 与 ``Pillow``:
      下载好这两个whl文件后, 把它们复制到python安装目录
      ``AppData\Local\Programs\Python\Python35-32`` 下方便操作,
      并在该目录下执行(如果出错提示, 则需要先安装wheel,
      再通过wheel安装它们):

      .. code:: shell

          python -m pip install Pillow-3.2.0-cp35-cp35m-win32.whl
          python -m pip install lxml-3.6.0-cp35-cp35m-win32.whl
          cd .. # back to nikola directory
          pip install --upgrade "Nikola[extras]"

-  选择二: 通过Anaconda安装 (本文选择此方法)

   -  安装Anaconda, 如果系统已有, 先升级Anaconda (在Anaconda prompt中使用 ``conda update --all`` 命令升级所有package.)
   -  查看python版本, 使用anaconda prompt命令行工具:

      .. code:: shell

          [Anaconda3] C:\home>python --version
          Python 3.5.1 :: Anaconda 4.0.0 (64-bit)

      创建一个叫myblog虚拟环境:

      .. code:: shell

          [Anaconda3] C:\home>conda create -n myblog python=3.x anaconda (where x is your python version. 也可以不创建新的environment直接安装)
          [Anaconda3] C:\home>activate myblog # use "source activate myblog" on linux
          [myblog] C:\home>pip install "Nikola[extras]"

      升级nikola时, 先升级Anaconda, 再按照上面步骤, 最后一步使用 ``pip install --upgrade "Nikola[extras]``. 我在升级7.7.9时报错, 于是直接先删除了Nikola再重新安装新版. 即 ``pip uninstall "Nikola[extras]"``, 之后再使用 ``pip install "Nikola[extras]"`` 安装.

创建项目
========

-  新建项目 新建一个目录 ``C:/home/mynikolasite`` 用于存放新建的项目:

   .. code:: shell

       [myblog] C:\home>nikola init --demo mynikolasite # create an empty project without "--demo" option

   这里nikola会问几个问题, 其中一个问到语言, 我们选择英文, 即输入
   ``en``, 其余的可视情况填写, 这些设置以后还可以在配置文件 ``conf.py``
   中更改.

-  主题 在 https://themes.getnikola.com/ 可以找到nikola的各种主题,
   安装主题 ``bootstrap3``, 为使主题生效, 需要另外在 ``conf.py`` 中设置
   ``THEME`` 变量:

   .. code:: shell

       [myblog] C:\home>cd mynikolasite
       [myblog] C:\home\mynikolasite>nikola install_theme bootstrap3

-  配置 ``conf.py`` 文件

   -  这里我们可以编辑刚才创建时选项, 如 ``SITE_URL`` 设置为
      “https://defnil.github.io/” (为方便发布到Github, 注意要以 ``/``
      结尾).
   -  排名第一位的格式是默认格式。如下面的 ``.rst`` 格式，用户也可以将自己
      偏好的格式移到第一位。
   -  如果页面要使用markdown和ipython notebook, 需要设置 ``POSTS`` 与
      ``PAGES`` 项(下面各增加了后几项,
      顺便吐槽以前在nikola中page居然被叫做story!!!):

      .. code:: python

          POSTS = (
              ("posts/*.rst", "posts", "post.tmpl"),
              ("posts/*.txt", "posts", "post.tmpl"),
              ("posts/*.html", "posts", "post.tmpl"),
              ("posts/*.md", "posts", "post.tmpl"),
              ("posts/*.ipynb", "posts", "post.tmpl"),
              ("posts/*.org", "posts", "post.tmpl"),
          )
          PAGES = (
              ("pages/*.rst", "pages", "story.tmpl"),
              ("pages/*.txt", "pages", "story.tmpl"),
              ("pages/*.html", "pages", "story.tmpl"),
              ("pages/*.md", "pages", "story.tmpl"),
              ("pages/*.ipynb", "pages", "story.tmpl"),
              ("pages/*.org", "pages", "story.tmpl"),
          )

   -  ``INDEX_TEASERS`` 设为 ``True`` 可以启用teaser.
      这时只需在每个post中加入 ``.. TEASER_END`` (reST文件)或
      ``<!--TEASER_END-->`` (markdown), 就可以使index
      page只显示post的第一部分, 而对于org-mode, 需要
      ``#+HTML: <!--TEASER_END-->`` 或者

      .. code:: python

          #+BEGIN_HTML
          <!--TEASER_END-->
          #+END_HTML

      另外,

      .. code:: python

          INDEX_READ_MORE_LINK = ""
          FEED_READ_MORE_LINK = ""

      可以禁止掉 “Reader more…”. 个人感觉没有必要,
      因为禁掉后读者不能分清楚是否文章在这里真的已经完结还是只是摘要部分.

   -  ``USE_BUNDLES`` 设为 ``True`` 可以启用webassets
      (前提是你已经安装了它), 这样可以获得速度上的提升.
   -  禁止评论功能:

      .. code:: python

          COMMENT_SYSTEM = ""

      也可以选择启用其它的评论支持, 如disqus, facebook等.
   -  ``GENERATE_RSS`` 设为 ``True`` 默认支持RSS, 如果设为 ``False``,
      则会关闭任何与RSS相关的功能. 同时还需要在 ``NAVIGATION_LINKS``
      把和RSS相关的页面去掉
   -  去掉Source links, 页面上将不会显示页面源代码的链接

      .. code:: python

          SHOW_SOURCELINK = False
          COPY_SOURCES = False

-  编译

   .. code:: shell

       [myblog] C:\home\mynikolasite>nikola build

   因为之前我们使用了 ``--demo``,
   所以现在生成的网页已经包含了一些page在里面了. 我们可以看一看效果:

   .. code:: shell

       [myblog] C:\home\mynikolasite>nikola serve

   这时使用流览器访问 http://localhost:8000/
   可以看到本地效果(Windows下使用命令 ``nikola serve -b`` 或者
   ``nikola serve --browser`` 流览器会打开http://0.0.0.0:8000/,
   则出现无法访问. 正确地址是 http://localhost:8000/). 使用 ``Ctrl+c``
   停止服务.

发布到Github
============

方式一
------

使用git发布网站有两种方式, 一种是创建两个branch, 一个存生成的网页,
另一个branch是整个build后的项目, 在两个branch之间切换,
这也是官方指导中的方法.

-  在Github上创建一个空的repo, 名字为 ``defnil.github.io``. 我们这里推荐使用项目主页，项目名字可以随便起，如 ``sitename``
-  在mynikolasite目录下创建.gitignore文件,(可直接下载使用\ `文件 <https://github.com/getnikola/nikola/blob/master/.gitignore>`__).
-  ``conf.py`` 相关设置如下:

   .. code:: python

       GITHUB_SOURCE_BRANCH = 'source' # where your Nikola site source will be deployed. We default to master, but user pages should use src or something else.
       GITHUB_DEPLOY_BRANCH = 'gh-pages' # where Nikola-generated HTML files will be deployed. It should be gh-pages for project pages and master for user pages (user.github.io).
       GITHUB_REMOTE_NAME = 'origin'
       GITHUB_COMMIT_SOURCE = True

-  打开git bash,

   .. code:: shell

       cd C:/home/mynikolasite
       git init
       git remote add origin git@github.com:defnil/sitename.git

-  当你build满意后, 就可以执行 ``nikola github_deploy``,
   不用亲自去commit, 也不用手动建立名为source的branch,
   这一切都自动由nikola做好了. 以后每次要更新网站时只用build后使用
   ``nikola github_deploy`` 就可以完成github page的更新,
   这一切都不需要切换到git命令行.

方式二
------

另一种方案是直接用两个repo来存放:

-  在Github上创建两个空的repo, 名字分别叫 ``nikola-blog`` 和
   ``defnil.github.io``, 其中 ``defnil`` 是我Github的用户ID,
   使用时需要换成你自己的ID. 注意不要包含readme或gitignore等文件.
-  在mynikolasite目录下创建一个.gitignore文件, (可直接下载使用
   https://github.com/getnikola/nikola/blob/master/.gitignore
   它已将output目录列进了忽略表中)
-  打开一个git bash, 将所有mynikolasite内容push到 ``nikola-blog``
   这个repo里:

   .. code:: shell

       cd C:/home/mynikolasite
       git init
       git add .
       git commit -m "first commit"
       git remote add origin git@github.com:defnil/nikola-blog.git
       git push -u origin master

-  再运行下面命令将output目录下的博客内容push到我们的blog site里, 即
   ``defnil.github.io`` 这个repo.

   .. code:: shell

       cd output
       git init
       git add .
       git commit -m "first blog commit"
       git remote add origin git@github.com:defnil/defnil.github.io.git
       git push -u origin master

Use Custom Domain
-----------------

比如, 我们现在已经购买了域名 ``abc.me``,
希望能与刚才创建的Github页面关联.
假设我们用的是上述方法一来管理和发布页面的. 则先在本地的 ``files/``
目录下添加 ``CNAME`` 文件, 其内容很简单, 只有 ``abc.me``.
可以用下面的命令实现:

.. code:: shell

    cd C:/home/mynikolasite
    echo "abc.me" > files/CNAME

之后我们在完成编译后使用 ``github_deploy`` 命令, ``CNAME`` 会被拷贝到
``output/`` 目录下, 并会自动上传至 ``defnil.github.io`` 的 ``source``
branch下.

.. code:: shell

    [myblog] C:\home\mynikolasite>nikola build
    [myblog] C:\home\mynikolasite>nikola github_deploy

接下来需要去域名服务商那里绑定, 以namecheap为例, 参考
`这里 <https://www.namecheap.com/support/knowledgebase/article.aspx/9645/2208/how-do-i-link-my-domain-to-github-pages>`__.
其中第1步我们已做过了相关设置, 略过直接从第2步开始. 完成这些步骤后,
就可以直接使用 ``abc.me`` 访问刚才的 ``defnil.github.io`` 了. 当然,
这时不要忘记将 ``conf.py`` 中的 ``SITE_URL`` 设为 “http://abc.me/”.

文档编辑
========

metadata
--------

进入anaconda prompt,

.. code:: shell

    [Anaconda3] C:\home>activate myblog # enter "nikola" virtual environment
    [myblog] C:\home>cd mynikolasite
    [myblog] C:\home\mynikolasite>nikola new_post

Nikola提供这种方式生成reStructuredText文档, 并存放在posts目录下,
(markdown文档使用 ``nikola new_post -f markdown``).
每产生个文档中都含有metadata, 包括标题, 作者等信息. 支持汉字作为标题,
汉字会被自动转换为拼音作为文件名, 如:

.. code:: shell

    [myblog] C:\home\mynikolasite>nikola new_post -f markdown
    Creating New Post
    Title: markdown test 我了个去呀
    Scanning posts..........done!
    [2016-04-23T07:47:55Z] INFO: new_post: Your post's text is at: posts\markdown-test-wo-liao-ge-qu-ya.md

我们可以将一些信息(比如作者)放在 ``conf.py`` 中,
这样所有post都不用再指定作者信息了:

.. code:: python

    ADDITIONAL_METADATA = {
        'author': 'defnil'
    }

当然也可以手动在 ``posts/`` 目录下新建文档, 还可以在里面新建多层目录,
非常灵活. metadata 中比较重要的有:

-  在 ``tags`` 中可包含多个标签, 用逗号隔开.

   -  ``draft`` 表示该文不会被收入索引, 但它默认会被发布. 禁止发布带有
      ``draft`` 标签的草稿, 在设置文件 ``conf.py`` 中设置
      ``DEPLOY_DRAFTS`` 为 ``False``. 当然前提是 ``DEPLOY_COMMANDS``
      中没包含 ``nikola build``.
   -  ``tags`` 中含有 ``private`` 的post不会被收入索引, 但会被发布.
      通过网址可以直接被访问到.

-  Post Types: text and micro. 前者为普通文章, 后者为微博.
-  ``nocomments``: 设置为 ``True`` 可以禁止本文的评论
-  ``password``: 可以为文章设置密码, 访问者需要输入密码才可以打开页面.

Math
----

-  要显示latex公式, 需要在post的 ``tags`` 里加入 ``mathjax``.

-  inline math 不再支持 ``$inline$`` 形式, 而使用 ``\(inline\)``
   (有的情况下需要使用 ``\\(inline\\)``), 如

   .. code::

       Euler’s formula: \(e^{ix} = \cos x + i\sin x\)

   在reST文件中还可以使用 ``:math:`` (推荐):

   .. code::

       Euler’s formula: :math:`e^{ix} = \cos x + i\sin x`

-  display math 使用 ``\[\]``, reST中推荐下面这种形式:

   .. code::

       .. math::

          \int \frac{dx}{1+ax}=\frac{1}{a}\ln(1+ax)+C

reST中插入多种格式
------------------

media
~~~~~

.. code::

    .. media:: http://vimeo.com/72425090
    .. media:: http://www.youtube.com/watch?v=wyRpAat5oz0

YouTube, Vimeo, Soundcloud
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    .. youtube:: 8N_tupPBtWQ

    .. vimeo:: 20241459

    .. vimeo:: 20241459
       :height: 240
       :width: 320

    [soundcloud url="http://api.soundcloud.com/tracks/78131362"

    .. soundcloud:: 78131362

Code
~~~~

.. code::

    .. code-block:: python
       :number-lines:

       print("Our virtues and our failings are inseparable")

Listing
~~~~~~~

将 ``foo.py`` 文件放在 ``LISTINGS_FOLDERS`` 指定的目录下.

.. code::

    .. listing:: foo.py python

Gist
~~~~

.. code::

    .. gist:: 2395294

Thumbnails
~~~~~~~~~~

To include an image placed in the ``images`` folder (or other folders
defined in ``IMAGE_FOLDERS``), use the thumbnail directive, like
this:

.. code::

    .. thumbnail:: ../tesla.jpg

       Nikola Tesla, the man that invented the 20th century.

Slideshows
~~~~~~~~~~

.. code::

    .. slides::

       /galleries/demo/tesla_conducts_lg.jpg
       /galleries/demo/tesla_lightning2_lg.jpg
       /galleries/demo/tesla4_lg.jpg
       /galleries/demo/tesla_lightning1_lg.jpg
       /galleries/demo/tesla_tower1_lg.jpg

Chart
~~~~~

可以参考 `这里 <http://www.pygal.org/en/latest/>`__

.. code::

    .. chart:: Bar
       :title: 'Browser usage evolution (in %)'
       :x_labels: ["2002", "2003", "2004", "2005", "2006", "2007"]
       'Firefox', [None, None, 0, 16.6, 25, 31]
       'Chrome',  [None, None, None, None, None, None]
       'IE',      [85.8, 84.6, 84.7, 74.5, 66, 58.6]
       'Others',  [14.2, 15.4, 15.3, 8.9, 9, 10.4]

Doc
~~~

用于跳转到其它页面.

.. code::

    Take a look at :doc:`my other post <creating-a-theme>` about theme creating.
    Take a look at :doc:`creating-a-theme` to know how to do it.

Org-Mode
========

-  安装插件

   .. code:: shell

       [Anaconda3] C:\home>activate myblog
       [myblog] C:\home>nikola plugin -i orgmode

-  在 ``conf.py`` 中 ``COMPILERS``, ``POSTS``, ``PAGES`` 项中加入下和 ``.org`` 有关的内容 (参考本项目中的 conf.py 文件)。

-  创建org文档

   .. code:: shell

       [myblog] C:\home>cd mynikolasite
       [myblog] C:\home\mynikolasite>nikola new_post -f orgmode

-  build

   .. code:: shell

       [myblog] C:\home\mynikolasite>nikola auto -b

   会自动检查文件变化并build, ``-b`` 是打开流览器(Windows下尝试
   ``nikola auto`` 总是失败(因为内部调用的 ``epoll`` 命令在win下无效),
   还是老老实实使用 ``nikola build`` 和 ``nikola serve`` 再访问
   http:localhost:8000 吧).
   注意emacs.exe所在目录必须要添加到系统环境变量PATH中,
   否则会找不到emacs而报错.

Markdown
========

Set as Default Format
---------------------

如果要将markdown或者其它格式设置为默认格式, 只需将其放在 ``POSTS`` 和
``PAGES`` 第一个位置, 这样以后在执行 ``nikola new_post`` 时不用加参数,
会默认生成 ``.md`` 文件:

.. code:: python

    POSTS = (
        ("posts/*.md", "posts", "post.tmpl"),
        ("posts/*.rst", "posts", "post.tmpl"),
        ("posts/*.txt", "posts", "post.tmpl"),
        ("posts/*.html", "posts", "post.tmpl"),
        ("posts/*.ipynb", "posts", "post.tmpl"),
    )
    PAGES = (
        ("pages/*.md", "pages", "story.tmpl"),
        ("pages/*.rst", "pages", "story.tmpl"),
        ("pages/*.txt", "pages", "story.tmpl"),
        ("pages/*.html", "pages", "story.tmpl"),
        ("pages/*.ipynb", "pages", "story.tmpl"),
    )

Extensions
----------

nikola默认使用的python-markdown遵循standard markdown
`标准 <http://daringfireball.net/projects/markdown/>`__,
如果要使用Github Favored Markdown
(`GFM <https://help.github.com/articles/github-flavored-markdown>`__),
可以利用python-markdown中的一些
`extensions <http://pythonhosted.org/Markdown/extensions/>`__
来尽量模拟GFM格式:

-  `nl2br <http://pythonhosted.org/Markdown/extensions/nl2br.html>`__:
   newline to linebreak
-  `fenced-code <http://pythonhosted.org/Markdown/extensions/fenced_code_blocks.html>`__:
   fenced code blocks
-  `smart-strong <http://pythonhosted.org/Markdown/extensions/smart_strong.html>`__:
   do not boldify multiple underscores in words
-  `codehilite <http://pythonhosted.org/Markdown/extensions/code_hilite.html>`__:
   syntax highlighting (using `Pygments <http://pygments.org>`__)
-  `footnotes <http://pythonhosted.org/Markdown/extensions/footnotes.html>`__:
   Footnots in markdown

可以设置 ``conf.py`` 文件中的 ``MARKDOWN_EXTENSIONS``
变量来使用这些extensions, 如:

.. code:: python

    MARKDOWN_EXTENSIONS = ["nl2br", "fenced_code", "footnotes",
    "smart_strong","codehilite(linenums=True)", 'extra']

Customization
=============

Install Theme
-------------

Themes can be found `here <https://themes.getnikola.com/>`__ and
installed with ``nikola install_theme themename``. Here *bootstrap3* is
a very good choice among them, since it supports
`Bootswatch <https://bootswatch.com/>`__ schemes. For example, to use
*Superhero* scheme on this `page <https://bootswatch.com/superhero/>`__,
just run

.. code:: shell

    [myblog] C:\home\mynikolasite>nikola bootswatch_theme -n custum_theme -s superhero -p bootstrap3

after installing *bootstrap3* theme. To enable this custom scheme, you
need set ``THEME`` to “custom” in ``conf.py``.

To further tweak your theme, please refer to `Theming
Nikola <https://getnikola.com/theming.html>`__.

Author Page
-----------

如果你每篇post的作者署名不一致, nikola会判断有多个作者,
因此会自动产生一个Author Page. 当点击每个post上的Author名时,
会转向这名作者的页面. 因此需要按此
`说明 <https://getnikola.com/blog/author-pages-in-nikola-v770.html>`__
进一步设置. 即: 将 ``AUTHOR_PAGES_ARE_INDEXES`` 设为 ``False``,
然后设置每个作者的描述:

.. code:: python

    ENABLE_AUTHOR_PAGES = True
    AUTHOR_PAGES_ARE_INDEXES = False
    AUTHOR_PATH = "authors"
    AUTHOR_PAGES_DESCRIPTIONS = {
        DEFAULT_LANG: {
            "defnil": "Old posts",
            "YONG": "^_^"
        },
    }
    HIDDEN_AUTHORS = ['Guest']

*bootstrap3* 主题已将这些页面包含在内,
因此作上述设置后就可以直接看到结果了. 如果你要完全禁止这个功能,
也很简单, 将 ``ENABLE_AUTHOR_PAGES`` 设为 ``False`` 即可.

Footer
-------

这里主要是在页面下显示 “Contents 2016 authorname - Powered by Nikola”
字样. 可以在 ``CONTENT_FOOTER`` 中做修改.

Navigation Pane
---------------

可以在 ``NAVIGATION_LINKS`` 里添加要链接的页面即可. 比如新建了一个名为
``about.rst`` 的page (会被存放在 ``pages/`` 目录下),
如果要将它放在导航栏里:

.. code:: python

    NAVIGATION_LINKS = {
        DEFAULT_LANG: (
            ("/archive.html", "Archive"),
            ("/categories/", "Tags"),
            ("/pages/about/index.html", "About"), # need to be changed to /output/index.html after you set your own homepage
            ("/rss.xml", "RSS feed"),
        ),
    }

根据 `Nikola Handbook <https://getnikola.com/handbook.html>`__ 的说法,
导航栏至多支持一级子菜单 “Only one level of submenus is supported”,
可以参照说明设置带子菜单样式的导航栏.

评论功能 DISQUS
---------------

.. code:: python

    COMMENT_SYSTEM = "disqus"
    COMMENT_SYSTEM_ID = "yongch" # your disqus ID

Image Size
----------

``MAX_IMAGE_SIZE`` 可以决定图片大小,
设置一个合理的数字可以保证所有页面中的图片不至于太大.
还有其它关于image的选项可以酌情选择.

另外所有放在 ``images/`` 下面的图片都会被复制到 ``output/``
里并且会为每张图片自动生成thumbnail图片. 因此如果不想产生Thumbnail,
就直接把图片放在 ``files/images/`` 目录下.

Set Your Own Homepage
---------------------

让网页更像site而不是blog,
`这里 <https://getnikola.com/creating-a-site-not-a-blog-with-nikola.html>`__
有如何建一个site的步骤. 对于已经按blog建立的站点,
我们可以进行下面的改造.

.. code:: python

    INDEX_PATH = "posts"
    PAGES = (
        ("pages/*.rst", "", "story.tmpl"),
        ("pages/*.txt", "", "story.tmpl"),
        ("pages/*.html", "", "story.tmpl"),
        ("pages/*.md", "", "story.tmpl"),
        ("pages/*.ipynb", "", "story.tmpl"),
        ("pages/*.org", "", "story.tmpl"),
    )

然后我们可以使用 ``nikola new_page -t Home`` 创建一个名为 “Home” 的页面.
(slug 改为index). 现在我们还需要根据 ``output/``
下目录的变化重新调整导航栏, 并且把posts放到“Posts”导航栏里. 如下图：

.. code:: python

    NAVIGATION_LINKS = {
        DEFAULT_LANG: (
            ("/posts/", "Posts"),
            ("/categories/", "Tags"),
            ("/Notes/index.html", "Notes"),
            ("/archive.html", "Archive"),
            ("/rss.xml", "RSS"),
            ("/about/index.html", "About"),
        ),
    }

这时可以编辑你自己的 ``home.rst`` 了. 也可以直接用我们之前做的
``about.rst`` 链接过来做主页: ``.. include:: pages/about.rst``.
如果你正在使用基于 *bootstrap3* 的主题, 因为它基于 ``Bootstrap``,
因此任何 ``Bootstrap`` 支持的格式都可以用 ``.rst`` 来表达. 可以参考
`这里 <https://getnikola.com/creating-a-site-not-a-blog-with-nikola.html>`__
的一个例子来写主页. 更多语法上的参考还可以看
`这里 <https://github.com/rougier/bootstrap-rst>`__.
