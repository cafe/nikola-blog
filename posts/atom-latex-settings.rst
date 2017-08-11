.. title: Atom LaTeX Settings
.. slug: atom-latex-settings
.. date: 2016-04-25 12:21:47 UTC+08:00
.. tags: latex, atom
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

Packages:
=========

#. Install TeX Live (https://www.tug.org/texlive/)
#. Install Atom

.. TEASER_END

#. Install Atom Packages

   -  ``latex`` (compile latex)
   -  ``language-lax`` (syntax highlighting)
   -  ``latexer`` (autocmpletion)
   -  ``latextools`` (more support)
   -  ``minimap`` (preview of code)
   -  ``open-recent`` (open recent files)
   -  ``pdf-view`` (builtin pdf viewer)
   -  ``file-icons``
   -  ``autocomplete-paths``
   -  ``spell-check``

#. Package Settings:

   -  ``latex``:

      -  Tex Path: ``C:\texlive\2015\bin\win32``         
      -  Builder: latexmk
      -  Always Open Result in Atom: Yes
      -  (Other settings: keep default)

   -  ``spell-check``:

      -  Grammars: text.tex

   -  ``pdf-view``:

      -  Fit to width on open: Yes

Important shortcuts:
====================

-  ``Alt+Shift+S``: search for latex snippet
-  ``Alt+Ctrl+B``: compile
-  ``Alt+Ctrl+S``: sync
-  ``Alt+Ctrl+C``: clear

