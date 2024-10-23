+++
title = 'Vim'
date = 2024-10-23T17:31:33+08:00
draft = false
tags = [ 'vim' ]
categories = '开发工具'
+++

## vimrc 备份

```config
let mapleader=","
set hlsearch
set incsearch
" 默认设置不区分大小写的搜索
set ignorecase
" 如果有大写字母，切换到区分大小写的搜索
set smartcase
set showmode
" 显示当前行号
set number
set relativenumber
set scrolloff=3
set history=500
" 共享系统粘贴板
set clipboard=unnamedplus,unnamed
set easymotion
" 自动保存
set autowrite
" 文件自动检测外部变化
set autoread
" 关闭提示音
set vb
" 响应速度
set updatetime=100
" 命令补全
set wildmenu
" tab -> 4个空格
set ts=4
set expandtab
set autoindent
set smartindent
set shiftwidth=4
" 突出显示当前行
set cursorline

" 清除突出显示的搜索结果
nnoremap <Space>sc :nohlsearch<CR>
" 退出插入模式
inoremap jj <Esc>
inoremap jk <Esc>
" 移动到行首
nnoremap H ^
" 移动到行尾
nnoremap L $
" 重做
nnoremap U <C-r>
" 退出选中
vnoremap v <Esc>
" 退
map Q :q!<CR>
map W :w<CR>
" 在末尾插入 ;
nnoremap ;; A;<Esc>

" 清空搜索结果
exec "nohlsearch"


" IDE Action ========================================================================
" 格式代码
nmap <Space>fm :action ReformatCode<CR>
" 优化import
nmap <Space>oi :action OptimizeImports<CR>
" Ace jump
nmap <Leader>f :action AceAction<CR>
" 跳转
nmap <Leader>b :action GotoDeclaration<CR>
" 跳转实现
nmap <Space>b :action GotoImplementation<CR>
" 打开最近项目
nmap <Leader>n :action ManageRecentProjects<CR>
" 打开文件
nmap <Leader>k :action OpenFile<CR>
" 重命名文件
nmap <Leader>rf :action RenameFile<CR>
" 自动补全
nmap <Leader><Space> :action SmartTypeCompletion<CR>
" 随处搜索
nmap <Leader><Leader> :action SearchEverywhere<CR>
" 提示选择
imap <A-j> <Down>
imap <A-k> <Up>
```