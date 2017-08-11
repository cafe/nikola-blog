.. title: Build Github Pages with Cryogen
.. slug: build-github-pages-with-cryogen
.. date: 2016-04-25 12:22:27 UTC+08:00
.. tags: clojure, github, web
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

Why Cryogen?
============

Cryogen是用Clojure写的一个static site generator. 它的优点在于:
markdown支持良好(包括Clojure语法高亮, 也支持AsciiDoc), 支持RSS, toc,
Disqus, Sitemap, 可以使用tags, 移动网页友好, 易上手等.
最主要是我自己比较喜欢Clojure, 因此就没有考虑使用其它框架.

.. TEASER_END

创建过程
========

首先参考Cryogen官方指导熟悉创建新页面的流程和设置: `Getting
Started <http://cryogenweb.org/docs/getting-started.html>`__

下来准备在Github上搭建一个静态博客:

-  在Github上创建两个空的repo, 名字分别叫 ``cryogen-blog`` 和
   ``defnil.github.io``, 其中 ``defnil`` 是我Github的用户ID,
   使用时需要换成你自己的ID. 注意不要包含readme或gitignore等文件.

-  打开命令行, ``cd`` 到你想要创建项目的位置, 如 ``C:/home``,
   下面语句将创建一个 ``C:/home/my-blog`` 的项目:

   .. code:: shell

       cd C:/home
       lein new cryogen my-blog

-  运行server, 它会在发任何变化后重新编译

   .. code:: shell

       cd my-blog
       lein ring server

-  编辑配置文件 ``my-blog/resources/templates/config.edn``,
   修改以下几项, 其余可以保持默认值:

   -  :site-url “https://defnil.github.io”
   -  :blog-prefix “”
   -  :site-title “My Awesome Blog”
   -  :author “defnil”
   -  :description “Nothing yet”

-  打开一个新的terminal, 运行:

   .. code:: shell

       cd C:/home/my-blog
       git init
       git add .
       git commit -m "first commit"
       git remote add origin git@github.com:defnil/cryogen-blog.git
       git push -u origin master

-  上面这些命令只是push到 ``cryogen-blog`` 这个repo里, 并没有创建blog.
   因此再运行下面命令将博客内容push到我们的blog site里, 即
   ``defnil.github.io`` 这个repo.

   .. code:: shell

       cd resources/public
       git init
       git add .
       git commit -m "first blog commit"
       git remote add origin git@github.com:defnil/defnil.github.io.git
       git push -u origin master

-  如果顺利的话, 现在使用流览器访问 ``defnil.github.io``
   就会出现建好的blog了.

编辑blog
========

关于如何写post请查看 `Writing
Posts <http://cryogenweb.org/docs/writing-posts.html>`__,
发布前可以通过访问 ``localhost:3000`` 查看效果.

发布更新
========

每次更新blog后, 运行以下命令:

.. code:: shell

    cd C:/home/my-blog
    lein ring server
    git add . && git commit -am "WIP" && git push
    cd resources/public && git add . && git commit -am "WIP" && git push && cd ../../

MathJax 支持
============

将下面代码

.. code:: html

    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']],
                           displayMath: [['\\[','\\]'], ['$$','$$']]}});
    </script>
    <script type="text/javascript"
          src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
    </script>

直接嵌入到模板文件中, 比如如果使用的是blue主题(默认主题), 则修改
``templates/themes/blue/html/base.html`` 内容, 将上面内容放在该文件
``head`` 部分即可. 参考
`issue59 <https://github.com/cryogen-project/cryogen/issues/59>`__

Read More
=========

-  `Referred
   Post <http://firesofmay.com/posts/2015-08-26-setup-cryogen.html>`__
-  To setup custom domain name with namecheap check this
   `link <http://davidensinger.com/2013/03/setting-the-dns-for-github-pages-on-namecheap/>`__.
-  If you do add custom domain name make sure you add CNAME to
   :keep-files otherwise it’ll get deleted.

