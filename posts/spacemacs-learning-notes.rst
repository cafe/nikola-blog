.. title: Spacemacs Learning Notes
.. slug: spacemacs-learning-notes
.. date: 2016-04-25 12:23:49 UTC+08:00
.. tags: emacs
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

Emacs Tutorial (Official)
=========================

-  ``C``: Ctrl
-  ``M``: Alt (Meta)
-  ``RET``: Enter (Return)

.. TEASER_END

Shortcuts
---------

-  ``C-x C-c``: exit
-  ``C-z``: run emacs in background
-  
-  ``C-/``: undo
-  ``C-g``: stop command
-  ``C-g C-/``: redo
-  ``C-u 4 C-x Tab``: indent selected region by 4 spaces. Use a negtive
   number will do un-indent.
-  
-  ``C/M-v``: move forward/backward one screenful
-  ``C-l``: move the text around the cursor to the center of the screen
-  ``C/M-f``: move forward a character/word
-  ``C/M-b``: move backward a character/word
-  ``C-n``: move to next line
-  ``C-p``: move to previous line
-  ``C/M-a``: move to beginning of line/sentence
-  ``C/M-e``: move to end of line/sentence
-  ``M-<``: move to beginning of whole text
-  ``M->``: move to end of whole text
-  ``C-u 8 C-f``: move forward 8 characters
-  ``M-g M-g``: go to line
-  
-  ``C-x 0``: delete window
-  ``C-x 1``: one window (kill other windows)
-  ``C-x 2``: split window vertically
-  ``C-x 3``: split window horizontally
-  ``C-h c C-f``: display brief description of the C - f command
-  ``C-h k C-f``: display documentation on the C - f command
-  ``C/M-d``: delete the next character/word (deleted contents cannot be
   yanked)
-  ``C/M-k``: kill to end of line/sentence
-  ``C-w``: kill selected text
-  ``C-y``: yank (paste) killed text
-  ``M-y``: bring privously killed text
-  ``C-@``: mark for selection
-  
-  ``C-x C-s``: save current buffer to its file
-  ``C-x s``: save all buffers to their files
-  ``C-x C-f``: find file
-  ``C-x C-b``: list buffers
-  ``C-x b``: switch to a buffer
-  ``C-x f``: margin
-  
-  ``M-x repl s``: replace string
-  ``M-x recover-file``: recover an auto-saved edition
-  ``M-x xx-mode``: switch to (toggle) xx mode
-  ``C-h m``: view current mode
-  ``C-h a xx``: list all the commands whose names contain xx
-  
-  ``C-s/r``: search forward/backward
-  ``C-x 2``: split screen to 2 windows
-  ``C-M-v``: scroll the other window
-  ``C-x o``: focus on the other window
-  ``M-x make-frame``: create a new frame (window)
-  ``M-x delete-frame``: delete selected frame (window)

Spacemacs First Impressions
===========================

-  http://spacemacs.org/doc/QUICK_START
-  https://github.com/syl20bnr/spacemacs/blob/master/doc/DOCUMENTATION.org
   (The most important one)
-  http://jr0cket.co.uk/2015/08/spacemacs-first-impressions-from-an-emacs-driven-developer.html

Shortcuts
---------

-  ``SPC``: referred to as the leader key. ``M-m`` in emacs style and
   space bar in vim style. It can be changed by setting the variable
   ``dotspacemacs-emacs-leader-key`` in emacs mode or
   ``dotspacemacs-leader-key`` in vim mode in the file ``~/.spacemacs``.
-  ``~``: referred to as the major-mode leader key: ``SPC m``.
-  ``SPC ?`` Search for specific keybindings
-  ``SPC f e h``: access documentation
-  ``C-x RET f``: see/change the file encoding

Describe functions for help info
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  ``SPC h d f``: describe-functions
-  ``SPC h d k``: describe-key
-  ``SPC h d m``: describe-mode
-  ``SPC h d v``: describe-variable

Use ``.spacemacs`` instead of ``init.el`` for configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``.spacemacs`` keybindings:
^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  ``M-m f e d``: open the ~/.spacemacs file
-  ``M-m f e R``: reload the configuration from ~/.spacemacs

Misc
~~~~

-  ``SPC f t``: toggle NeoTree
-  ``SPC T h``: select a theme
-  ``SPC c l/L``: comment/uncomment

``.spacemacs`` has 3 sections:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  ``dotspacemacs/init`` configuration applied when Spacemacs first
   starts, eg evil or holy mode(emacs), themes, fonts, full screen,
   recent files, etc
-  ``dotspacemacs/layers`` add features to spacemacs using layers, a
   layer can contain elisp and packages from Melpa/Elpa
-  ``dotspacemacs/user-config`` additional layer configuration or your
   own customisations. Adding ``(menu-bar-mode 1)`` here will bring menu
   bar back after initialization.

keybindings and commands organizer: Helm ``M-m``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  ``a`` applications
-  ``b`` buffers
-  ``c`` compile/comments
-  ``C`` capture/colors
-  ``e`` errors
-  ``f`` files
-  ``g`` git/version control
-  ``S`` spelling
-  ``T`` themes

numbered buffers
~~~~~~~~~~~~~~~~

Jump to any buffer using ``M-m`` and buffer number, e.g., ``M-m 3``
jumps to buffer number

adding layers
~~~~~~~~~~~~~

-  Open ``~/.spacemacs`` and add the layers to
   ``dotspacemacs-configuration-layers``. We can uncomment some useful
   layers listed there.
-  ``M-m f e h``: list all layers
-  ``M-m configuration-layer/create-layer`` create your own layer

other configurations
~~~~~~~~~~~~~~~~~~~~

``dotspacemacs/config``
^^^^^^^^^^^^^^^^^^^^^^^

-  change font:

   .. code:: clojure

           dotspacemacs-default-font '("Ubuntu Mono"
                                   :size 16
                                   :weight normal
                                   :width normal
                                   :powerline-scale 1.1)

-  set key bindings:

   .. code:: clojure

           (define-key global-map (kbd "C-+") 'text-scale-increase)
           (define-key global-map (kbd "C--") 'text-scale-decrease)

   **\*\*\*** ``dotspacemacs/init``

-  full screen mode at startup

   .. code:: clojure

           dotspacemacs-fullscreen-at-startup t

-  Markdown preview install ``pandoc``, then add ``pandoc`` layer to
   ``dotspacemacs-configuration-layers`` in ``~/.spacemacs``.
   Additionally, add

   .. code:: clojure

           (add-hook 'markdown-mode-hook 'pandoc-mode)

   to the ``user-config`` to enable pandoc-mode when opening markdown
   files (see http://joostkremers.github.io/pandoc-mode/). Use menu
   ``Pandoc->Create PDF`` to export ``.pdf`` file. To export ``.html``
   file, go to menu and set ``Pandoc->Output Format->HTML`` and
   ``Pandoc->Files->Output File->Create Output Filename``. Then click
   ``Pandoc->Run Pandoc``, the ``.html`` file is generated. To export to
   other file formats, just follow the previous steps and change
   ``Pandoc->Output Forma`` to the object file format like ``docx``,
   ``LaTeX``, etc.

