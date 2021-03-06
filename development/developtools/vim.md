# Vim

## About

Vim is a text editor for programmers, power users & command-line junkies.

## Configuration

```
""""""""""""""""""""""VUNDLE PLUGIN""""""""""""""""""""

" 不兼容vi
set nocompatible

" 不检测文件类型
filetype off

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
"Plugin 'VundleVim/Vundle.vim'

" let Vundle manage Vundle, required
Plugin 'gmarik/Vundle.vim'

" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.
" plugin on GitHub repo

Plugin 'kabbamine/vcoolor.vim'
Plugin 'guns/vim-clojure-highlight'
Plugin 'guns/vim-sexp'
Plugin 'guns/vim-clojure-static'
Plugin 'tpope/vim-fireplace'
Plugin 'kien/rainbow_parentheses.vim'
Plugin 'mattn/emmet-vim'
Plugin 'dhruvasagar/vim-table-mode'
Plugin 'gorodinskiy/vim-coloresque'
Plugin 'jelera/vim-javascript-syntax'
Plugin 'walm/jshint.vim'
Plugin 'moll/vim-node'
Plugin 'airblade/vim-gitgutter'
Plugin 'Yggdroot/indentLine'
Plugin 'nvie/vim-flake8'
Plugin 'davidhalter/jedi-vim'
Plugin 'axiaoxin/vim-json-line-format'
Plugin 'axiaoxin/favorite-vim-colorscheme'
Plugin 'junegunn/vim-emoji'
Plugin 'mhinz/vim-startify'
Plugin 'terryma/vim-multiple-cursors'
Plugin 'suan/vim-instant-markdown'
Plugin 'tpope/vim-surround'
Plugin 'SirVer/ultisnips'
Plugin 'honza/vim-snippets'
Plugin 'bling/vim-airline'
Plugin 'kien/ctrlp.vim'
Plugin 'majutsushi/tagbar'
Plugin 'scrooloose/nerdcommenter'
Plugin 'scrooloose/nerdtree'
Plugin 'Valloric/YouCompleteMe'

" All of your Plugins must be added before the following line
call vundle#end()            " required
" 针对不同的文件类型采用不同的缩进格式
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line



""""""""""""""""""""""BASE CONFIG"""""""""""""""""""""""

" 取消备份
set nobackup
set noswapfile

" 解决中文乱码
set encoding=utf-8
set fileencodings=utf-8,chinese,gbk,latin-1,gb2312,ucs-bom,cp936
if has("win32")
  set fileencoding=chinese
else
  set fileencoding=utf-8
endif

" 解决菜单乱码
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim

" 解决consle输出乱码
"language messages zh_CN.utf-8

" 状态栏配置
set laststatus=2

" 打开语法高亮
syntax enable

" 开启语法检测
syntax on

" vimrc文件修改之后自动加载
autocmd! bufwritepost .vimrc source %

" 文件修改之后自动载入
set autoread

" yy直接复制到系统剪切板（For macvim）
"set clipboard=unnamed

" 高亮搜索命中的文本
set hlsearch

" 随着键入即时搜索
set incsearch

" 搜索时忽略大小写
set ignorecase

" 有一个或以上大写字母时仍大小写敏感
set smartcase

set guifont=Menlo:h14

colorscheme Tomorrow-Night-Bright
" 使用自带配色
"colorscheme elflord
"set background=dark

" 在状态栏显示正在输入的命令
set showcmd

" 显示括号配对情况
set showmatch

" :next, :make 命令之前自动保存
set autowrite

" 允许使用鼠标
set mouse=a

" 设置行号
set nu

" 退格键可用
set backspace=2

" 退格键一次删掉4个空格
set smarttab

" 缩进
set autoindent
set smartindent

" 保存文件时自动删除行尾空格或Tab
autocmd BufWritePre * :%s/\s\+$//e

" 保存文件时自动删除末尾空行
autocmd BufWritePre * :%s/^$\n\+\%$//ge

" 填充Tab
set expandtab
set tabstop=4
set shiftwidth=4
set shiftround

" 填充空白字符
" au BufRead,BufNewFile *.py,*.pyw,*.c,*.h match BadWhitespace /\s\+$/

" 代码折叠 光标在缩进下方时用za命令折叠或展开
set fdm=indent
" 默认展开
set foldlevel=99

" 突出显示当前行，列
"set cursorline
"set cursorcolumn

" 设置 退出vim后，内容显示在终端屏幕, 可以用于查看和复制
set t_ti= t_te=

" 打开文件时始终跳转到上次光标所在位置
autocmd BufReadPost *
      \ if ! exists("g:leave_my_cursor_position_alone") |
      \     if line("'\"") > 0 && line ("'\"") <= line("$") |
      \         exe "normal g'\"" |
      \     endif |
      \ endif



"""""""""""""""""""""""""KEY MAPPING""""""""""""""""""""

" 映射切换buffer的键位
nnoremap [b :bp<CR>
nnoremap ]b :bn<CR>

" 映射切换tab的键位
nnoremap [t :tabp<CR>
nnoremap ]t :tabn<CR>

" normal模式下Ctrl+c全选并复制到系统剪贴板(linux必须装有vim-gnome)
nmap <C-c> gg"+yG

" visual模式下Ctrl+c复制选中内容到剪贴板
vmap <C-c> "+y

" Ctrl+v原样粘贴剪切板内容
inoremap <C-v> <ESC>"+pa

" w!!写入只读文件
cmap w!! w !sudo tee >/dev/null %

" F2切换行号显示
nnoremap <F2> :set nonu!<CR>:set foldcolumn=0<CR>

" F3打开目录树
nmap <silent> <F3> :NERDTreeToggle<CR>

" F4显示TagList
nmap <silent> <F4> :TagbarToggle<CR>

" F5运行脚本
if exists("$VIRTUAL_ENV")
    autocmd FileType python map <buffer> <F5> :!$VIRTUAL_ENV'/bin/python' %<CR>
else
    autocmd FileType python map <buffer> <F5> :!python %<CR>
endif

" <F6> 新建标签页
map <F6> <Esc>:tabnew<CR>

" <F7> 拷贝粘贴代码不破坏缩进
set pastetoggle=<F7>

" <F8> sort import and auto pep8
autocmd FileType python map <buffer> <F8> :!autopep8 -i -a --ignore=W690,E501 %;isort %;<CR><CR>

" <F9> pep8 by yapf
autocmd FileType python map <buffer> <F9> :!yapf -i % --style=pep8;isort %;<CR><CR>

" 给当前单词添加引号
nnoremap w" viw<esc>a"<esc>hbi"<esc>lel
nnoremap w' viw<esc>a'<esc>hbi'<esc>lel

" 在Normal Mode和Visual/Select Mode下，利用Tab键和Shift-Tab键来缩进文本
nnoremap > >>
nnoremap < <<
vnoremap > >gv
vnoremap < <gv

" 左右分割窗口Ctrl+w +v
" 上下分割窗口Ctrl+w +s
" 关闭窗口Ctrl+w  +q

" quicker window switching
nnoremap <C-h> <C-w>h
nnoremap <C-j> <C-w>j
nnoremap <C-k> <C-w>k
nnoremap <C-l> <C-w>l

" emoji
imap <C-e> <C-X><C-U>


""""""""""""""""""""""""""""""PLUGIN CONFIG""""""""""""""""""""""""""
" NerdCommenter
let g:NERDSpaceDelims=1

" NERDTREE
" 不显示的文件
let NERDTreeIgnore=['\.pyc$', '\~$']
" show nerdtree when starts up
"autocmd vimenter * NERDTree
" 退出最后一个buff时也退出nerdtree
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTreeType") && b:NERDTreeType == "primary") | q | endif

" CtrlP
let g:ctrlp_show_hidden = 1
let g:ctrlp_cmd = 'CtrlPMixed'

"Ctrl-X Ctrl-U emoji补全
set completefunc=emoji#complete

" instant-markdown
let g:instant_markdown_slow = 1

" airline
let g:airline_section_y = '%{strftime("%H:%M")}'
" 开启tabline
let g:airline#extensions#tabline#enabled = 1
" tabline中当前buffer两端的分隔字符
let g:airline#extensions#tabline#left_sep = ' '
" tabline中未激活buffer两端的分隔字符
let g:airline#extensions#tabline#left_alt_sep = '|'
" tabline中buffer显示编号
let g:airline#extensions#tabline#buffer_nr_show = 1

" jedi
autocmd FileType python setlocal completeopt-=preview
let g:jedi#completions_command = "<C-n>"

" flake8
let g:flake8_show_in_file = 1
let g:flake8_show_in_gutter = 1
autocmd! BufRead,BufWritePost *.py call Flake8()

" gitgutter
let g:gitgutter_sign_modified = '*'
let g:gitgutter_sign_removed = '-'

" ultisnips
let g:UltiSnipsExpandTrigger="<tab>"
let g:UltiSnipsJumpForwardTrigger="<tab>"
let g:UltiSnipsJumpBackwardTrigger="<s-tab>"

" jshint
autocmd! BufRead,BufWritePost *.js :JSHint

" vim-table-mode: markdown
let g:table_mode_corner="|"

" rainbow_parentheses
let g:rbpt_colorpairs = [
    \ ['brown',       'RoyalBlue3'],
    \ ['Darkblue',    'SeaGreen3'],
    \ ['darkgray',    'DarkOrchid3'],
    \ ['darkgreen',   'firebrick3'],
    \ ['darkcyan',    'RoyalBlue3'],
    \ ['darkred',     'SeaGreen3'],
    \ ['darkmagenta', 'DarkOrchid3'],
    \ ['brown',       'firebrick3'],
    \ ['gray',        'RoyalBlue3'],
    \ ['darkmagenta', 'DarkOrchid3'],
    \ ['Darkblue',    'firebrick3'],
    \ ['darkgreen',   'RoyalBlue3'],
    \ ['darkcyan',    'SeaGreen3'],
    \ ['darkred',     'DarkOrchid3'],
    \ ['red',         'firebrick3'],
    \ ]

let g:rbpt_max = 16
let g:rbpt_loadcmd_toggle = 0
au VimEnter * RainbowParenthesesToggle
au Syntax * RainbowParenthesesLoadRound
au Syntax * RainbowParenthesesLoadSquare
au Syntax * RainbowParenthesesLoadBraces

" vim-clojure-static
let g:clojure_syntax_keywords = {
    \ 'clojureMacro': ["defproject", "defcustom"],
    \ 'clojureFunc': ["string/join", "string/replace"]
    \ }

" vim-clojure-highlight
autocmd BufRead *.clj try | silent! Require | catch /^Fireplace/ | endtry

" vCoolor.vim
let g:vcoolor_map = '<leader>cp'
let g:vcool_ins_rgb_map = '<leader>cpr'       " Insert rgb color.
let g:vcool_ins_hsl_map = '<leader>cph'       " Insert hsl color.
let g:vcool_ins_rgba_map = '<leader>cpra'      " Insert rgba color.
```

#Install Plugin for Vim

# Vundle

## About

[Vundle] is short for _Vim bundle_ and is a [Vim] plugin manager.

[Vundle] allows you to...

* keep track of and [configure] your plugins right in the `.vimrc`
* [install] configured plugins (a.k.a. scripts/bundle)
* [update] configured plugins
* [search] by name all available [Vim scripts]
* [clean] unused plugins up
* run the above actions in a *single keypress* with [interactive mode]

[Vundle] automatically...

* manages the [runtime path] of your installed scripts
* regenerates [help tags] after installing and updating

[Vundle] is undergoing an [interface change], please stay up to date to get latest changes.

[![Gitter-chat](https://badges.gitter.im/VundleVim/Vundle.vim.svg)](https://gitter.im/VundleVim/Vundle.vim) for discussion and support.

![Vundle-installer](http://i.imgur.com/Rueh7Cc.png)

## Quick Start

1. Introduction:

   Installation requires [Git] and triggers [`git clone`] for each configured repository to `~/.vim/bundle/` by default.
   Curl is required for search.

   If you are using Windows, go directly to [Windows setup]. If you run into any issues, please consult the [FAQ].
   See [Tips] for some advanced configurations.

   Using non-POSIX shells, such as the popular Fish shell, requires additional setup. Please check the [FAQ].

2. Set up [Vundle]:

   `$ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

3. Configure Plugins:

   Put this at the top of your `.vimrc` to use Vundle. Remove plugins you don't need, they are for illustration purposes.

   ```vim
   set nocompatible              " be iMproved, required
   filetype off                  " required

   " set the runtime path to include Vundle and initialize
   set rtp+=~/.vim/bundle/Vundle.vim
   call vundle#begin()
   " alternatively, pass a path where Vundle should install plugins
   "call vundle#begin('~/some/path/here')

   " let Vundle manage Vundle, required
   Plugin 'VundleVim/Vundle.vim'

   " The following are examples of different formats supported.
   " Keep Plugin commands between vundle#begin/end.
   " plugin on GitHub repo
   Plugin 'tpope/vim-fugitive'
   " plugin from http://vim-scripts.org/vim/scripts.html
   Plugin 'L9'
   " Git plugin not hosted on GitHub
   Plugin 'git://git.wincent.com/command-t.git'
   " git repos on your local machine (i.e. when working on your own plugin)
   Plugin 'file:///home/gmarik/path/to/plugin'
   " The sparkup vim script is in a subdirectory of this repo called vim.
   " Pass the path to set the runtimepath properly.
   Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
   " Install L9 and avoid a Naming conflict if you've already installed a
   " different version somewhere else.
   Plugin 'ascenator/L9', {'name': 'newL9'}

   " All of your Plugins must be added before the following line
   call vundle#end()            " required
   filetype plugin indent on    " required
   " To ignore plugin indent changes, instead use:
   "filetype plugin on
   "
   " Brief help
   " :PluginList       - lists configured plugins
   " :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
   " :PluginSearch foo - searches for foo; append `!` to refresh local cache
   " :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
   "
   " see :h vundle for more details or wiki for FAQ
   " Put your non-Plugin stuff after this line
   ```

4. Install Plugins:

   Launch `vim` and run `:PluginInstall`

   To install from command line: `vim +PluginInstall +qall`

## Docs

See the [`:h vundle`](https://github.com/VundleVim/Vundle.vim/blob/master/doc/vundle.txt) Vimdoc for more details.

## Changelog

See the [changelog](https://github.com/VundleVim/Vundle.vim/blob/master/changelog.md).

## People Using Vundle

see [Examples](https://github.com/VundleVim/Vundle.vim/wiki/Examples)

## Contributors

see [Vundle contributors](https://github.com/VundleVim/Vundle.vim/graphs/contributors)

*Thank you!*

## Inspiration & Ideas

* [pathogen.vim](http://github.com/tpope/vim-pathogen/)
* [Bundler](https://github.com/bundler/bundler)
* [Scott Bronson](http://github.com/bronson)

## Also

* Vundle was developed and tested with [Vim] 7.3 on OS X, Linux and Windows
* Vundle tries to be as [KISS](http://en.wikipedia.org/wiki/KISS_principle) as possible

## TODO:
[Vundle] is a work in progress, so any ideas and patches are appreciated.

* ✓ activate newly added bundles on `.vimrc` reload or after `:PluginInstall`
* ✓ use preview window for search results
* ✓ Vim documentation
* ✓ put Vundle in `bundles/` too (will fix Vundle help)
* ✓ tests
* ✓ improve error handling
* allow specifying revision/version?
* handle dependencies
* show description in search results
* search by description as well
* make it rock!

[Vundle]:http://github.com/VundleVim/Vundle.vim
[Windows setup]:https://github.com/VundleVim/Vundle.vim/wiki/Vundle-for-Windows
[FAQ]:https://github.com/VundleVim/Vundle.vim/wiki
[Tips]:https://github.com/VundleVim/Vundle.vim/wiki/Tips-and-Tricks
[Vim]:http://www.vim.org
[Git]:http://git-scm.com
[`git clone`]:http://gitref.org/creating/#clone

[Vim scripts]:http://vim-scripts.org/vim/scripts.html
[help tags]:http://vimdoc.sourceforge.net/htmldoc/helphelp.html#:helptags
[runtime path]:http://vimdoc.sourceforge.net/htmldoc/options.html#%27runtimepath%27

[configure]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L126-L233
[install]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L234-L254
[update]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L255-L265
[search]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L266-L295
[clean]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L303-L318
[interactive mode]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L319-L360
[interface change]:https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L372-L396