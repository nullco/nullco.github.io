+++
author = "null.co"
title = "Vim Cheatsheet"
date = "2024-10-23"
description = ""
tags = [
    "cheatsheet",
    "vim",
]
categories = [
    "cheatsheet"
]
aliases = ["cheatsheet"]
+++

## Normal Mode

#### Moving around

`h j k l` Arrows: left down up right

`f{char}` Forward to next occurence of `{char}`
  
`F{char}` Forward to previous occrence of `{char}`

`t{char}` Forward until next occurence of `{char}`
  
`T{char}` Forward until previous occrence of `{char}`

`*` Search for word under cursor

`n` Get next search result

`N` Get previous search result

`$` Go to last line character

`^` Go to first line character

`0` Go to start of line

`gg` Go to start of buffer

`G` Go to end of buffer

`;` Repeat last motion

`,` Apply last motion reversed

`%` Move to matching opening/closing character e.g. `(]}`

`{` Move to previous paragraph

`}` Move to next paragraph

#### Modify right from normal mode

`.` Repeat last change

`u` Undo last change

`x` Delete character under cursor

`<C-r>` Redo last change

`dd` Delete current line

`>G` Indent right from current line to end of buffer

`<C-a>` Add 1 to the next number in the current line

`<C-x>` Remove 1 from the next number in the current line

`J` Join current and next line together

`K` Check man page of word under cursor

#### Entering Insert mode

`i` Insert before current cursor position

`I` Insert at the start of the current line

`a` Append after current cursor position

`A` Append at the end of the current line

`s` Remove character at cursor position and keep editing

`S` Remove line contents and keep editing

`C` Remove from character at cursor position till end of line and keep editing

#### Entering Replace mode

`R` Enter replace mode at current cursor position.

#### Entering Visual mode

`v` Enter character-wise visual mode

`V` Enter line-wise visual mode

`<C-v>` Enter block-wise visual mode

`gv` Enter visual mode reselecting last selected text.


#### Actions

An `{action}` is the combination of an `{operator}` and a `{motion}`

* Examples of operators: `c`, `d`, `y`, `gU`
* Examples of motions: `l`, `w`, `p`

`{repeat}{action}` Repeat the `{action}` `{repeat}` times

## Insert mode

`<C-h>` Delete back one character (backspace)

`<C-w>` Delete back one word

`<C-u>` Delete back to start of line

`<Esc>` Switch to normal mode

`<C-[>` Switch to normal mode

`<C-o>` Switch to insert normal model

`<C-r>{reg}` Paste the contents of the register identified by `{reg}`

`<C-r><C-p>{reg}` Paste the contents of the register identified by `{reg}` in a smarter way

`<C-r>={expression}<CR>` Paste the results of an arithmetic `{expression}`

`<C-v>{code}` Put character at current cursor position identified by `{code}`.

## Visual mode

`o` Toggle the free end of a selection

## Comand mode

Most commands follow the syntax `:{range}{command}`.

### Ranges

A `{range}` is determined by a start and end address.

An `{address}` can be:

* `.` For the current line
* `$` For the end of the buffer
* `/{pattern/` For a pattern
* `{number}` For a line number
* `{address}+{number}` For an address `{number}` lines after the `{address}`

Specify a range in the following ways:

`:{start},{end}` For a range between `{start}` address and `{end}` address

### Commands

TBD

### Special commands

`/{pattern}` Scan document for next match of `{pattern}`

`?{pattern}` Scan document for previous match of `{pattern}`

## Useful Actions

`cw` Change from cursor till the end of word

`dw` Delete a word from current cursor position till its end

`diw` Delete all characteres from the current word

`daw` Delete all characters from the word and additional spaces surrounding it

`g~iw` Swap case of entire word

`guiw` Make entire word lower case

`gUiw` Make entire word uppercase

`ggyG` Yank all contents of buffer

`zz` Redraw the screen with the current line in the middle

`:%s/{find}/{replace}/g<CR>` Substitue `{find}` for `{replace}` in entire buffer

`:{start},{end}s/{find}/{replace}/g<CR>` Substitue `{find}` for `{replace}` in between `{start}` and `{end}` lines in buffer

`d/{pattern}<CR>` Deletes all text between cursor and next occurrence of `{pattern}`

## Useful Commands

`:bd` Close current buffer

`:bn` Go to next buffer

`:bn` Go to previous buffer

`:split` Split window horizontally

`:vsplit` Split window vertically

`:term` Open terminal

`:tabnew` Create new tab

`:tabn` Go to next tab

`:tabp` Go to previous tab

