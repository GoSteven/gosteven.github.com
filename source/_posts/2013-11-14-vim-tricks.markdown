---
layout: post
title: "vim tricks"
date: 2013-11-14 03:48
comments: true
categories: 
---

This post will keep accumunating the tricks that I felt useful.

### Disalbe and enable mouse 

enable mouse:
    :set mouse=a
disalbe mouse:
    :set mouse-=a

### Copy text out of vim with mouse=a enalbed

Press `shift` while selecting using mouse.

OS X (mac): hold alt/option while selecting.



### Simplist vimrc

    set mouse=a
    syntax on
    filetype on
    filetype indent on
    filetype plugin on

    map  <space> :
    map  <C-j> <C-w><down>
    map  <C-k> <C-w><up>
    map  <C-h> <C-w><left>
    map  <C-l> <C-w><right>
    imap <C-j> <down>
    imap <C-k> <up>
    imap <C-h> <left>
    imap <C-l> <right>

    let mapleader=";"
    map <leader>w :w!<cr>
    map <leader>q :close<cr>
    map <leader>[ <C-o>
    map <leader>] <C-]>
    map <leader><space> <C-w>

    map <leader>j :bn<cr>
    map <leader>k :bp<cr>
    map <leader>bd :bd<cr>

    map <leader>tn :tabnew<cr>
    map <leader>l  :tabn<cr>
    map <leader>h  :tabp<cr>
    map <C-t>      :tabnew<cr>
    map <C-tab>    :tabn<cr>
    map <C-S-tab>  :tabp<cr>


    set ts=4
    set expandtab
    set smarttab
    set shiftwidth=4
    set autoindent
    set smartindent

### A list of powerful vim plugins
[https://github.com/wklken/k-vim](https://github.com/wklken/k-vim)
