# Vim

https://www.vim.org/

## Modes

- Each mode dictates the behaviour
    - Normal
        - For navigating and manipulation of text
        - Typically the default mode
    - Insert
        - For adding/inserting text
        - Text typed will be inserted
    - Replace
        - For replacing text
        - Text type will replace text at cursor
    - Visual
        - For navigating and manipulation of text but shows selection
        - Similar to Normal mode but with some extra functioniality
    - Command
        - For entering single commands
- Transferring between modes
    - `Esc`: return to Normal mode from any mode
    - Normal to Insert mode
        - `i`: insert before caret
        - `a`: append after caret
        - `I`: insert at start of line
        - `A`: append at end of line insert mode
        - `o`: next line at insert mode
        - `O`: before line at insert mode
    - Normal to Replace mode
        - `r`: replace single letter
        - `R`: replace all
    - Normal to Visual mode
        - `v`: visual mode
    - Normal to Command mode
        - `:`: command mode
- Sections below typically referr to commands available in Normal/Visual mode
- Commands starting with `:` indicate entering command mode

## Exiting / Saving
- `:q` / `:quit`	exit the current window by saving current changes, if one window exists, exit the editor
- `:q!` / `:quit!`	exit without saving current changes
- `:wq` save the current file and exit, if the file has readonly permissions, failed
- `:wq!` save the current file and exit, even for readonly permissions of a file
- `:x` / `:exit`	save only for modifications and exit
- `:qa` / `:quitall`	exit all windows

## Navigation
- `h` left
- `j` down
- `k` up
- `l` right
- `w` beginning of next word
- `b` previous beginning of word
- `e` end of word
- `W` beginning of next word after a whitespace
- `B` beginning of previous word before a whitespace
- `E` end of word before a whitespace
- `0` / `^`: start of line
- `$`: end of line
- `Ctrl`+`f`: page down
- `Ctrl`+`b`: page up
- `:n`: (n is a number), jump to the nth line

## General
- `u`: Undo
- `Ctrl` + `r`: redo
- `5`[COMMAND]: perform command 5 times  (e.g. `5j` will move 5 characters to the right)
- `.`: repeat last action

## Search
- `/` / `?`: search forwards / backwards from cursor
   - `n` / `N`: next or previous result
- `*` / `#`: search for next / previous occurence of word under cursor

## Replace
- `:s/oldtext/newtext/options`: replace in current line
- `:%s/oldtext/newtext/options`: replace in current file

### Replace options
- `g`: global (multiple replaces)
- `i`: case insensitivve
- `c`: confirm

## Editing / Copy / Paste
- `x` / `X`: delete character at cursor / before cursou
- `y`: copy single character
- `p` / `P`: paste at cursor position / before cursor position
- `j`: join current and next line
- `Y` / `yy`: yank / copy entire line
- `D` / `dd`: delete current line and copy
- `d`[NAVIGATION_COMMAND]: delete corresponding range (e.g. `dw` deletes from cursor to beginning of next word)
- To paste from system clipboard use OS defaults: enter Insert mode and use Operating system level paste shortcut e.g. `Ctrl`+`V` / `Cmd`+`V`
- (In VISUAL mode) `c`: change current selection and toggle insert mode

## Indenting
- `>>`: increase indent
- `<<`: decrease indent
- `3>>`: increase indent for 3 lines
- `=`: auto indent

## Code folding

- `%`: find matching bracket / brace
- `zo`: open
- `zc`: close
- `zM`: close all
- `zR`: open all

## Configuration

- Stored in `~/.vimrc`

```
set nocompatible
 
" Search
set hlsearch    " highlight matches
set ignorecase  " case insensitive
set smartcase   " allow case sensitive search based auto decting on text entered
set incsearch   " highlight while typing
 
 
syntax on   " syntax highlighting
 
set number " line numbers
set cursorline
set cursorcolumn
 
set autoindent " auto indent
 
" Set shift width to 4 spaces.
set shiftwidth=4
" Set tab width to 4 columns.
set tabstop=4
" Use space characters instead of tabs.
set noexpandtab
 
set showmode "show mode at bottom when swtiching
set showcmd " show command at bottom
 
set showmatch "show matching brackets
set foldenable
set foldmethod=indent
set foldlevelstart=10
```