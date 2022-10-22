---
layout: post
title: Distraction free writing in Vim with Goyo
read_time: true  
comments: true
category: Open Source
tags: [ GitHub Projects ]
---

I can’t believe that I’ve never mentioned one of my most used Vim plugins ever. I’m talking about [Goyo](https://github.com/junegunn/goyo.vim).

It adds a distraction free mode that helps me focus on my writing by centering the content and hiding all other elements.
supports console ANSI-sequences for curl, httpie or wget; HTML for web browsers; or PNG for graphical viewers. 

<img src="/assets/groovy-gorilla.png" width="654">

### Usage

Toggle Goyo:

`:Goyo`

Turn on and resize Goyo to the dimension 100x50:
`:Goyo 100x50`

Turn off Goyo:

`:Goyo!`

### My configuration changes

The plugin works just fine as is, but I did change the text area to 100x50 (as seen in the example image above), as I find that to be a better fit for me.

These are the settings that I added to my .vimrc configuration file:

`let g:goyo_width=100`
`let g:goyo_height=50`

Also bound the toggle feature to the key <Leader>g:

`map <Leader>g :Goyo<CR>`

