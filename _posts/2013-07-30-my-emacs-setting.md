---
layout: post
title: "My Emacs setting"
category: Emacs
tags: [Emacs, Emacs Prelude, Font]
---
{% include JB/setup %}

# Emacs prelude
I use the [Emacs Prelude](http://batsov.com/prelude/) to support the customization of my Emacs.

## Install
- Install Emacs 24

- If you are not a beginner you might already have .emacs and .emacs.d under your home folder. Then before installation first rename your ~/.emacs to personal.el, and ~/.emacs.d to ~/personal. Move personal.el into ~/personal.
- If you don't have git or curl. Install them:

        sudo apt-get install git-core
        sudo apt-get install curl libcurl3 libcurl3-dev php5-curl
        sudo /etc/init.d/apache2 restart

- Install prelude

        curl -L http://git.io/epre | sh

- Now a .emacs.d is built again under your home folder. Move your ~/personal into it. Your personal.el will be loaded at last on starting emacs.

## Usage
Follow the instruction on [Emacs Prelude](http://batsov.com/prelude/) to get start with the default settings and key bindings in prelude. Unfortunately many features are not mentioned and you are recommended to read the source codes.

# Customize font in Emacs on Ubuntu
The default font looks ugly for me and I've determined to change it the first week I used Emacs. There are two ways to do that: 1. Define font in .emacs (for me the personal.el file); 2. Define font in X. If you choose the first solution Emacs will start with its default font and change to your font after .emacs is loaded and that's annoying for me. Here's how to do it in the second way:

- Install font manager

        sudo apt-get install font-manager

- Browse and choose your favorite font in font-manage for example "Bitstream Charter"

- Install x11-utils, x11-xserver-utils

        sudo apt-get install x11-utils x11-xserver-utils

- Search the font in X

        xlsfonts | grep bitstream | more

- If you get nothing then the font you choose is not a X-font and you have to choose another one. Otherwise you'll get output like

    > -bitstream-bitstream charter-bold-i-normal--0-0-0-0-p-0-adobe-standard
    > -bitstream-bitstream charter-medium-i-normal--0-0-0-0-p-0-adobe-standard
    > -bitstream-bitstream charter-medium-r-normal--0-0-0-0-p-0-adobe-standard
    > -bitstream-bitstream charter-medium-r-normal--0-0-0-0-p-0-ascii-0
    > -bitstream-bitstream charter-medium-r-normal--0-0-0-0-p-0-iso10646-1
    > -bitstream-bitstream charter-medium-r-normal--0-0-0-0-p-0-iso8859-1
    > -bitstream-charter-bold-i-normal--0-0-100-100-p-0-iso8859-1
    > -bitstream-charter-bold-r-normal--0-0-100-100-p-0-iso8859-1
    > --More--

- Create a .Xresources under your home folder if you don't have one. Write the following in it:

        Emacs.Fontset-0:-bitstream-courier 10 pitch-*-*-normal--*-*-*-*-m-*-myfontset
        Emacs.font:myfontset

    The first line is choosed from the output of your xlsfonts. The last part is replaced by a user defined name. The "bold/medium" and "i/r" are font style, the zeros are font size. They don't need to be determined and can be replaced by '*'s. Other parts of the line are more detailed features of the font and you'll know whether you want it only after you use it. The above bitstream-courier looks pretty fine for me and is recommended to be used with light background.

    Note that other instructions on the net tell you to use a .Xdefaults file. However, I found that if font is defined in .Xdefaults it will lose effect after reboot.

- Load your .Xresources file

        xrdb .Xresources

- Now restart your Emacs to see the effect.

# My personal.el file
The following is just a backup.

    ;;; personal.el --- my settings
    ;;; Commentary:

    ;;; Code:
    ;; theme
    (disable-theme 'zenburn)
    ;;(load-theme 'dichromacy t)

    ;; cursor
    (setq-default cursor-type 'bar)

    ;; minor mode
    ;; outline minor mode prefix
    (setq outline-minor-mode-prefix [(control o)])

    ;; auctex
    (mapc (lambda (mode)
    (add-hook 'LaTeX-mode-hook mode))
    (list 'LaTeX-math-mode
    'linum-mode
    'auto-complete-mode
    'outline-minor-mode
    'auto-fill-mode))
    (add-hook 'LaTeX-mode-hook
    (lambda ()
    (setq TeX-auto-untabify t     ; remove all tabs before saving
    TeX-engine 'xetex       ; use xelatex default
    TeX-show-compilation t) ; display compilation windows
    ;; (TeX-global-PDF-mode t)       ; PDF mode enable, not plain
    (setq TeX-save-query nil)
    (imenu-add-menubar-index) ))

    ;; reftex
    (require 'reftex)
    (add-hook 'LaTeX-mode-hook 'turn-on-reftex)
    (setq reftex-plug-into-AUCTeX t)

    ;; cdlatex
    (add-hook 'LaTeX-mode-hook 'turn-on-cdlatex)
    (autoload 'cdlatex-mode "cdlatex" "CDLaTeX Mode" t)
    (autoload 'turn-on-cdlatex "cdlatex" "CDLaTeX Mode" nil)

    ;; bibretrieve
    (add-to-list 'load-path "~/.emacs.d/personal/bibretrieve")
    (load "bibretrieve")

    ;; auto name post file
    (defun insert-post-title ()
    "Insert the date in current position."
    (interactive)
    (insert (format-time-string "%Y-%m-%d-")))

    ;; set key for naming post file
    (global-set-key (kbd "<f4>") 'insert-post-title)

    ;; template
    (autoload 'file-template-auto-insert "file-template" t t)
    (add-hook 'find-file-not-found-hooks
    'file-template-find-file-not-found-hook 'append)

    ;; org refile
    (setq org-refile-targets (quote (("note.org" :maxlevel . 1)
    ("todo.org" :maxlevel . 2)
    ("project.org" :maxlevel . 1)
    ("finished.org" :maxlevel . 1))))


    ;; org capture
    (setq org-directory "~/org/")
    (setq org-default-notes-file "~/org/inbox")
    (define-key global-map "\C-cc" 'org-capture)

    ;; org todo keywords
    (setq org-todo-keywords
    '((sequence "TODO(t)" "|" "DONE(d)" "ABORTED(a)")))

    ;; capture templats
    (setq org-capture-templates
    '(("t" "Todo" entry (file+headline "~/org/todo.org" "Unorganized Tasks")
    "* TODO %?\n")
    ("b" "To buy" entry (file+headline "~/org/todo.org" "To buy")
    "* TODO %?\n")
    ("a" "Appointment" entry (file+headline "~/org/todo.org" "Appointments")
    "* TODO %?\n %i %^T\n")
    ("s" "Schedule" entry (file+headline "~/org/todo.org" "Schedule")
    "* TODO %?\n %i %t\n")
    ("f" "Future" entry (file+headline "~/org/todo.org" "Future")
    "* %?\n")
    ("i" "Idea" entry (file+headline "~/org/note.org" "Ideas")
    "* %?\n")
    ("B" "Book" entry (file+headline "~/org/note.org" "Books")
    "* %?\n :PROPERTIES:\n %^{TITLE}p %^{AUTHOR}p :START-DATE: %U\n :END:\n")
    )
    )

    ;; org publish
    (require 'org-publish)
    (setq org-publish-project-alist
    '(

    ;; ... add all the components here (see below)...
    ;; org note
    ("org-notes"
    :base-directory "~/orgpub/post"
    :base-extension "org"
    :publishing-directory "~/lilinleave.github.com/_posts"
    :recursive t
    :publishing-function org-publish-org-to-html
    :headline-levels 4             ; Just the default for this project.
    :body-only t ;; Only export section between <body> </body>
    )
    ;; org static
    ("org-static"
    :base-directory "~/orgpub/"
    :base-extension "css\\|js\\|png\\|jpg\\|gif\\|pdf\\|mp3\\|ogg\\|swf"
    :publishing-directory "~/lilinleave.github.com/"
    :recursive t
    :publishing-function org-publish-attachment
    )
    ("pub" :components ("org-notes" "org-static"))
    )
    )

    (provide 'personal)
    ;;; personal.el ends here
