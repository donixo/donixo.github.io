---
layout: post
title:  "Instalasi Vim Dengan Vundle"
date:   2015-10-15 18:08:39 +0700
categories: vim vundle
---

Ketika awal-awal menggunakan `vim`, saya banyak bergantung ke bundle-manager yang keren via `pathogen`. Pada `pathogen` kita dapat lebih rapi dalam memanage file-file autoload dan bundle.

Namun kini ada solusi yang lebih mudah Mengganti `pathogen` dengan [vundle](https://github.com/VundleVim/Vundle.vim), kelebihannya adalah dengan mengandalkan vundle, kita dapat mencari dan menginstall sendiri dependencies dari git repo dengan hanya menambahkan paket yang ingin kita install ke dalam vim lewat beberapa baris di `.vimrc`.

Contohnya seperti di bawah ini di `~/.vimrc`:



```bash
Bundle 'tpope/vim-endwise'
Bundle 'tpope/vim-git'
Bundle 'tpope/vim-surround'
```


## Instalasi Vim 


install vim versi terbaru menggunakan `brew` di mac:

```bash
$ brew install vim --override-system-vi
```

Parameter `—override-system-vi` digunakan karena secara default sudah ada `vi` bawaan Mac, hanya saja kadang pembaruan nya suka lama. Karena itu saya lebih memilih untuk menggunakan `vim` hasil instalasi dari `brew`.

`mkdir ~/.vim` untuk membuat direktori baru untuk menyimpan bundle vim. Setelah itu kita dapat melakukan clone `vundle` dari git repo


## Instalasi Vundle

Setelah selesai menginstall 


```bash
$ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

Kemudian bersihkan ` ~/.vimrc` lalu ganti dengan baris berikut ini sesuai urutan baris, kemudian simpan:

```vimrc
set nocompatible
filetype off
set rtp+=~/.vim/bundle/vundle/
call vundle#rc()

Bundle 'gmarik/vundle'
Bundle 'tpope/vim-endwise'
Bundle 'tpope/vim-git'
Bundle 'tpope/vim-surround'
Plugin 'bling/vim-airline'
Bundle 'edkolev/tmuxline.vim'
Bundle 'jlanzarotta/bufexplorer'
Plugin 'flazz/vim-colorschemes'
Bundle 'Valloric/YouCompleteMe'
Bundle 'kien/ctrlp.vim'

filetype on


set laststatus=2
filetype plugin indent on
set nu
set ai
set ts=4
set shiftwidth=4
set hlsearch
set equalalways
set linebreak
set expandtab
set gdefault
set ruler
set ignorecase
set visualbell
set nofoldenable
syntax enable
set encoding=utf-8
set guifont=Menlo\ for\ Powerline
let g:airline_powerline_fonts = 1
set t_Co=256
colorscheme wombat256mod

nnoremap <leader><space> :noh<cr>
nnoremap <leader>t :TlistToggle<cr>
nnoremap <leader><space>e :Errors<cr>
inoremap <C-space> <C-x><C-o>
inoremap jj <ESC>
autocmd FileType php set omnifunc=phpcomplete#CompletePHP
autocmd FileType python set omnifunc=pythoncomplete#Complete
autocmd FileType javascript set omnifunc=javascriptcomplete#CompleteJS
autocmd FileType css set omnifunc=csscomplete#CompleteCSS
autocmd FileType html set omnifunc=htmlcomplete#CompleteTags

autocmd BufReadPost *
\ if ! exists("g:leave_my_cursor_position_alone") |
\ if line("'\"") > 0 && line ("'\"") <= line("$") |
\ exe "normal g'\"" |
\ endif |
\ endif
sign define fixme text=!> linehl=Todo texthl=Error
function! SignFixme()
execute(":sign place ".line(".")." line=".line(".")." name=fixme file=".expand("%:p"))
endfunction
map <F5> :call SignFixme()<CR>

```

Setelah selesai, jalankan `:PluginInstall` pada vim untuk menyelesaikan instalasi. Hasilnya dapat kita lihat pada gambar di bawah ini:

![vundle-install](/assets/vundle-install.png)



## Airline

Kalau diperhatikan pada `.vimrc` yang ada di atas, terlihat saya menggunakan bundle `vim-airline`. Bundle ini digunakan untuk ‘mempercantik’ tampilan `vim`. Pada `vim-airline` ini, dibutuhkan font khusus agar karakter-karakter khusus yang digunakan untuk tampilan `airline`. Salah satu font yang banyak digunakan adalah `Menlo for Powerline`. Saya mengunduhnya pada laman Github [disini](https://github.com/abertsch/Menlo-for-Powerline).

Untuk menginstallnya mudah saja, tinggal unduh dan double klik semua file `.ttf` hasil unduhan. Secara otomatis console dan/atau macvim kita akan menggunakan font Menlo tersebut, karena di `.vimrc` sebelumnya kita telah menyatakan vim akan menggunakan font Menlo:

```bash
set guifont=Menlo\ for\ Powerline
let g:airline_powerline_fonts = 1
```
Hasilnya akan muncul seperti di bawah ini:

![airline](/assets/airline-result.png)
