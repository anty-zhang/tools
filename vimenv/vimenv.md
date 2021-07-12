[[TOC]]

# 查看VIM版本及支持的python版本

```bash
# 查看vim的版本
vim --version

# 查看vim使用的python版本,可在编辑器中运行
:python import sys; print(sys.version)
```

# VIM扩展

```bash
git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim

touch ~/.vimrc

cat ~/.vimrc

set nocompatible              " required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'gmarik/Vundle.vim'

" Add all your plugins here (note older versions of Vundle used Bundle instead of Plugin)

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
```

# pydiction 自动补全插件

```bash
git clone https://github.com/rkulla/pydiction.git

mkdir -p ~/.vim/tools/pydiction

cp pydiction/complete-dict ~/.vim/tools/pydiction/
cp -r pydiction/after ~/.vim/

# 在~/.vimrc文件尾添加
filetype plugin on 
let g:pydiction_location = ‘~/.vim/tools/pydiction/complete-dict’
let g:pydiction_menu_height = 5
```

# 语法检测安装

```bash
# 下载插件
pyflakes http://www.vim.org/scripts/script.php?script_id=2441
pep8 http://www.vim.org/scripts/script.php?script_id=2914
flake8 http://www.vim.org/scripts/script.php?script_id=4440

# 然后放到
~/.vim/ftplugin/python

# 配置vimrc
flakes 加到vimrc里面

if has("gui_running")
highlight SpellBad term=underline gui=undercurl guisp=Orange
endif
let g:pyflakes_use_quickfix = 1 "这是开关

pep8可以设置哪个键来检测,默认F5

"let g:pep8_map='whatever key'

flake8
"Auto-check file for errors on write:
let g:PyFlakeOnWrite = 1
"List of checkers used:
let g:PyFlakeCheckers = 'pep8,mccabe,pyflakes'
"Default maximum complexity for mccabe:
let g:PyFlakeDefaultComplexity=10
"List of disabled pep8 warnings and errors:
let g:PyFlakeDisabledMessages = 'E501'
"Default height of quickfix window:
let g:PyFlakeCWindow = 6
"Whether to place signs or not:
let g:PyFlakeSigns = 1
"Maximum line length for PyFlakeAuto command
let g:PyFlakeMaxLineLength = 100
"Visual-mode key command for PyFlakeAuto
let g:PyFlakeRangeCommand = 'Q'
```

# 颜色配置方案

```bash
git clone https://github.com/altercation/solarized.git

mkdir ~/.vim/colors

```
