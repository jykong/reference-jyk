# Vim Command Reference
Vim lets you edit text faster by giving you text navigation & editing commands using only key presses instead of using the mouse. It takes some practice to get the hang of it, but then it becomes fun!

Jump to section
* [Insert Mode](#insert-mode)
* [Normal Mode](#normal-mode)
* [Visual Mode](#visual-mode)
* [Command Mode](#command-mode)
## Modes
  __Vim has *multiple modes*__
  
  __*Keystrokes behave differently*__ between modes
  
  * If you're not sure which mode you're in, check the status on the bottom of the screen

Normal Mode
* This is the default mode
* Single character selection cursor
* Bottom status shows nothing [command line] or -- NORMAL -- [vscode]
* `escape` always returns to normal mode

Insert mode
* This is the standard text typing mode
* Triggered by `i`, `a`, or `o` from normal mode
* Thin insertion cursor
* Bottom status shows -- INSERT --

Visual mode
* Triggered by `v` or `V` from normal mode
* Highlight selection cursor
* Bottom status shows -- VISUAL --

Command mode
* Triggered by `/` or `:` from normal mode
* Bottom status replaced with text input field

---
## Insert Mode
* Simplest way enter insert mode is to press `i` from normal mode
* Type characters as you would normally
* Copy / paste works with normal hotkeys
* Basically functions the same as any normal editor, as if you weren't using Vim
* `escape` switch to normal mode

---
## Normal Mode
### Basic Cursor Movement
* `h j k l` move cursor left / down / up / right
* `0 $` jump to start / end of the line
* `enter` jump to start of next line

### Basic Editing
* `i a o` insert here / insert after / insert new line and enter [Insert Mode](#insert-mode)
* `u` undo
* `ctrl+r` redo
* `:w :q :wq :q!` _then_ `enter` save / close / save & close / force close without saving

### Intermediate Cursor Movement
* `11j 11k` move cursor 11 lines down / up
* `w b e` jump to next / previous / end of word
* `3w 3b 3e` jump to next / previous / end of 3 words
* `{ }` jump to previous / next paragraph
* `gg G` jump to start / end of document
* `7G` jump to start of line 7
* ` `` ` jump back (undo last jump)

### Intermediate Editing
* `x` cut character
* `yy y3j y3k` copy line / cut 3 lines down / cut 3 lines up
* `dd d3j d3k` cut line / cut 3 lines down / cut 3 lines up
* `p` paste
* `r` replace character with next character input
* `s S` substitute character / line and enter [Insert Mode](#insert-mode)
* `I A` insert at start / end of line and enter  [Insert Mode](#insert-mode)
* `v V` switch to visual / visual line selection mode ([see Visual Mode](##visual-mode))

### Find & Replace
Vim search patterns are regular expressions. See [Regular Expressions](https://github.com/jykong/reference-jyk/blob/master/regular_expressions/regular_expressions.md).

#### Find
* `/pattern` find and highlight "pattern"
* `/pattern` _then_ `enter` jump to next instance of "pattern"
  * `n` jump to next instance of "pattern"

#### Replace
Replace (substitute) command format is `:<line_range>s/<search_pattern>/<replace_text>/<suffixes>`

Line Range Specifiers:
* `%` all lines (entire document)
* `x,y` from line x to line y
* `.` this
* `+5 -5` next / previous 5
* `^ $` beginning / end

Suffixes:
* `g` global
* `c` ask for confirmation
* `i` case insensitive

Examples:
* `:%s/search_pattern/replace_text/gc` find all instances of "search_pattern" to replace with "replace_text", asking for confirmation
  * `y/n/a/q/l` yes, no (skip), all, quit, last
* `:%s/search_pattern/replace_text/g` replace all without asking for confirmation
* `:%s/search_pattern/replace_text/gi` replace all case insensititive
* `:.,$s/search_pattern/replace_text/g` replace all from this line until the end of the document (ignore preceding lines)
* `:.,^s/search_pattern/replace_text/g` replace all from this line until the end of the document (ignore subsequent lines)
* `:.,+5s/search_pattern/replace_text/g` replace all from this line until the next 5 lines
* `:g/search_pattern1/s/search_pattern2/replace_text/g` replace all instances of "search_pattern2" with "replace_text" from lines matching "search_pattern1"

### Repeat
* `.` repeat last command

---
## Visual Mode
Starts highlighting from cursor position prior to switching to visual mode
### Cursor Movement
Same as normal mode
### Editing
* `y` copy selection
* `d x` cut selection
* `s` cut selection and enter [Insert Mode](#insert-mode)

---
## Command Mode
### Command History
From either `/` or `:`
* `up arrow` previous command
* `down arrow` subsequent command
### Command History Partial Match
* `/prefix` or `:prefix`
  * `up arrow` previous command partially matching "prefix"
  * `down arrow` subsequent command partially matching "prefix"