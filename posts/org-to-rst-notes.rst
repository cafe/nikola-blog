.. title: Org to rst Notes
.. slug: org-to-rst-notes
.. date: 2016-04-25 18:43:39 UTC+08:00
.. tags: org-mode, web
.. category: tools
.. link: 
.. description: convert .org to .rst files for Nikola with Pandoc
.. type: text
.. author: YONG

I’m using ``Nikola`` for site generating, which supports various types
of input formats: ``.rst`` natively, ``.md`` partially, ``.org`` via
``orgmode`` plug-in, .., etc. No one seems perfect for me:

.. TEASER_END

-  ``.rst`` worse readability than other two, also has the worst syntax
   among the three for writing too
-  ``.md`` easy to use but there are no **standard** rules to follow:
   different parsers deliver different (even inconsistent) rendering
   styles
-  ``.org`` uniform standard and easy to write, but no perfect parser
   exists. Also it is bound to ``Emacs``, which makes it not handful
   sometimes.

Before deciding to use ``.rst`` as my primary format for ``Nikola``, I
tried several ways:

#. Use ``.md``

   Since I’m used to editing markdown files in ``Atom``, which is more
   lightweight than ``Emacs`` IMO. What makes me annoyed is that the
   rendering styles from ``Atom`` and ``Nikolas`` are not the same,
   especially when it comes to code blocks within lists. Following
   `this <https://daringfireball.net/projects/markdown/syntax>`__, it
   says markdown supports multiple paragraphs inside list items:

       List items may consist of multiple paragraphs. Each subsequent
       paragraph in a list item must be indented by either 4 spaces or
       one tab:

       #. This is a list item with two paragraphs. Lorem ipsum dolor sit
          amet, consectetuer adipiscing elit. Aliquam hendrerit mi
          posuere lectus.

          Vestibulum enim wisi, viverra nec, fringilla in, laoreet
          vitae, risus. Donec sit amet nisl. Aliquam semper ipsum sit
          amet velit.

       #. Suspendisse id sem consectetuer libero luctus adipiscing.

   There are two issues:

   #. Code blocks are not recognized anymore if you put indented code
      blocks after list items. Instead, they are treated as block quotes
      by ``Nikola``. Thus no syntax highlight for these blocks, and even
      worse, the source code in the blocks is concatenated without any
      line breaks.

   #. If you put an indented paragraph after an indented code block, the
      texts in the paragraph are also transformed into block quotes.

   IMO, this is due to Markdown’s bad design or non-uniform standards of
   different parsers (or bugs). Because sometimes texts after 4
   successive blank spaces are directly treated as block quotes or code
   blocks. This makes it ambiguous to separate them from paragraphs in
   lists, and things become more tricky if you have a nested list.

   But for ``.org`` format, the rule is clear: just align your contents
   with the list they belong to, no matter what style of your contents
   are: they can be plain texts or even code blocks.

#. Use ``.org``

   It seems reasonable to use ``.org`` files for web page generating
   thanks to the ``orgmode`` plug-in provided by ``Nikola``. It seems a
   promising solution, but wait! Once you picked a nice theme, and built
   your site, you found there might have a lot of things to tweak: You
   need to add ``.css`` files to your theme for code highlighting to
   make your site look pleasing. Also you need to be careful with the
   special syntax used by ``org-mode`` of ``Emacs``. I found there are a
   lot of weird errors on the published web page using the ``orgmode``
   plug-in. Anyway, it works but brings you lots of troubles if you are
   careless. Also, the plug-in works by calling the publish related
   functions of ``Emacs``, which makes it slower if you are holding a
   large website.

#. Use ``.rst``

   Yeah, finally it comes to the natively supported format. At first I
   am quite reluctant to choose this option because I don’t want to
   learn a new markup language since I have known ``Markdown`` and
   ``Org-mode``. But later on, I found a workaround: I edit all the
   stuff within ``Emacs`` using ``.org`` format, and use ``Pandoc`` to
   convert all the ``.org`` files to ``.rst`` files for web page
   generation. At the beginning, I was wondering whether ``Pandoc`` will
   give me satisfactory results – it turns out not that bad, though not
   perfect. I believe this can be attributed to the unified standards of
   both ``.org`` and ``.rst`` formats, which make the parser less
   error-prone. Overall, the converted file have few errors from my own
   experience. Also by writing a simple script, I can convert all
   existing files to ``.rst`` files with ``Pandoc`` in batch. Thus I
   don’t need to worry the formats when I’m writing in ``org-mode`` from
   now on.

Several points to note after converting:

-  Images in ``.org`` files are like ``./images/pic.png``, while in
   resulted ``.rst`` files you need to change them to
   ``/images/pic.png`` manually.
-  Literal examples (``BEGIN_EXAMPE``) in ``.org`` files are converted
   to ``.. code:: example``, which cannot be recognized by ``Pygments``.
   So just change them to ``.. code::`` manually.
