---
title: Installing tmux where needed
---

Tmux
====
I enjoy using tmux...

Installing as user on Centos 5.7
-------

```


wget https://github.com/downloads/libevent/libevent/libevent-2.0.21-stable.tar.gz
tar xzvf libevent-2.0.21-stable.tar.gz
cd libevent-2.0.21-stable
./configure --disable-shared --enable-static --prefix=$HOME/.local
make && make install
cd ..
wget http://ftp.gnu.org/pub/gnu/ncurses/ncurses-5.9.tar.gz
tar xzvf ncurses-5.9.tar.gz
cd ncurses-5.9
./configure --disable-shared --enable-static --prefix=$HOME/.local
make && make install
cd ..
wget http://downloads.sourceforge.net/tmux/tmux-1.8.tar.gz
tar xzf tmux-1.8.tar.gz
cd tmux-1.8
PKG_CONFIG_PATH=$HOME/.local/lib/pkgconfig CFLAGS="-I$HOME/.local/include -I$HOME/.local/include/ncurses" LDFLAGS="-L$HOME/.local/lib" ./configure --enable-static --prefix=$HOME/.local
make && make install
```
