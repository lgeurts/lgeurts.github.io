---
layout: post
title: Goyo, distraction free writing in (Neo)Vim
read_time: true  
comments: true
category: Open Source
tags: [ GitHub Projects ]
---

Can’t believe I’ve never mentioned [Goyo](https://github.com/junegunn/goyo.vim), one of my most used Vim plugins ever.

It adds a distraction free mode that helps me focus while writing by centering the content and hiding all other elements.

<img src="/assets/vim-goyo.png" width="654">

Other nice features are the support of console ANSI-sequences for curl, httpie or wget; HTML for web browsers; or PNG for graphical viewers. 

### Usage

Toggle Goyo:

`:Goyo`

Turn on and resize Goyo to the dimension 100x50:

`:Goyo 100x50`

Turn off Goyo:

`:Goyo!`

### My configuration changes

The plugin works just fine as is, but I did change the text area in my .vimrc config file (as seen in the image above), as I find that to be a better fit for my eyes.

`let g:goyo_width=100`

`let g:goyo_height=50`

Finally, as piece de resistance I added a shortcut by bounding the toggle feature to the key <Leader>g:

`map <Leader>g :Goyo<CR>`
