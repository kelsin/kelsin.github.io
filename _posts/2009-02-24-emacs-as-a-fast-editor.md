---
layout: post
title: Emacs as a fast $EDITOR
date: 2009-02-24 15:30:13.000000000 -08:00
tags:
  - servers
  - emacs
---

I've been using vim as my `$EDITOR` setting for quite some time, and recently
started using emacsclient. Two things about this setup bothered me. First I
would have to switch to my emacs workspace in Xmonad in order to reach the
editor, and when working on svn or git commits my cursor would be where it was
last time I edited a commit. Not wanting to change the way Xmonad keeps emacs
windows appearing on the same workspace or the way emacs saves my cursor
position I found a way around both problems.

``` bash
# Setup common ultilities
export EDITOR="emacsclient --tty"
export ALTERNATE_EDITOR=gvim
```

This is in my bash config (a sourced file in .bashrc). The `--tty` option on
emacs client uses the new Multi-tty code in Emacs 23 to load a terminal emacs
(connected to my running emacs) in the current terminal. This works
beautifully. With a 256-color xterm and the same font selected I almost can't
tell I'm not in my Xwindows emacs frame. No more switching windows when I want
to quick edit something. I also alias `e` to `$EDITOR` so I can open files super
quick.

``` lisp
;; Multi TTY
(add-hook 'server-visit-hook
          '(lambda ()
             (goto-char (point-min))))
(server-start)
```

This is a snippet from my `.emacs.d/init.el` file. This adds a hook so that when
Emacs visits a file via the server it will move the pointer to the top.

Problems solved.
