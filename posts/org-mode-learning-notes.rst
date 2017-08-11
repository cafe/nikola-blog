.. title: Org-Mode Learning Notes
.. slug: org-mode-learning-notes
.. date: 2016-04-25 12:23:26 UTC+08:00
.. tags: emacs, org-mode
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

Org-mode basics
===============

-  http://orgmode.org/worg/org-tutorials/org4beginners.html
-  http://orgmode.org/worg/index.html
-  http://orgmode.org/worg/org-tutorials/orgtutorial_dto.html

.. TEASER_END

Introduction
------------

Applications: notes, mindmaps, TODO lists, calendar, day planner, object
schedules...

Lists and Notes
~~~~~~~~~~~~~~~

shortcuts
^^^^^^^^^

-  ``tab / shift-Tab``: (un)fold
-  ``M-left/right``: promote or demote a headline
-  ``M-up/down``: move a headline up or down
-  ``M-RET``: insert a new headline

Plain lists:
^^^^^^^^^^^^

-  **Unordered lists** start with ``-,+,*`` (when using ``*`` as a
   bullet, lines must be indented or they will be seen as top -level
   headlines).
-  **Ordered lists** start with a number and a dot.
-  **Descriptions** use ``::`` (a blank space is still needed, like
   ``- Sean Austin ::``)

Notes:
^^^^^^

-  ``*bold*``
-  ``/italic/``
-  ``_underlined_``
-  ``=code=``
-  ``~verbatim~``
-  ``+strikethrough+``

todo
~~~~

shortcuts
^^^^^^^^^

-  ``M-shift-RET``: add TODO (call ``org-insert-todo-heading``)
-  ``shift-left/right``: cycle workflow
-  ``SPC m T``: show todo tree in current document (org-show-todo-tree).
   It will show only your current todos and folding the rest away.
-  ``C-c a``: agenda (The word **agenda** means *things to be done*)
-  ``C-c C-s``: pop up the calendar
-  ``C-c [``: add document to the list of agenda files.
-  ``C-c ]``: remove document from the list of agenda files
-  ``C-c .``: add date
-  ``C-u C-c .``: add time and date
-  ``C-c C-t``: close task (call ``org-todo``)

Appointments and deadlines
^^^^^^^^^^^^^^^^^^^^^^^^^^

It works in this way: 1. Add a new heading called "Call Fred"
(``M-RET Call Fred``) 2. At the end press ``C-c .`` (if you want to add
a time, use ``C-u C-c .`` instead), which will give the *date chooser*
at the bottom of the screen 3. Type something by hand or use
``shift-left/right`` to change the date 4. Go to the agenda ``C-c a``
and press ``a``, you get an agenda entry 5. Use ``C-c [`` to add file to
the agenda, and use ``C-c a a/t`` to view the agenda or list the todos

Help
====

-  ``C-h i``: call the info browser, and use ``tab`` to jump from
   hyperlink
-  It should be preferred to use ``Org`` menu to convert org file to tex
   then pdf file, which looks better than the pdf file generated
   directly from ``Pandoc`` menu.
