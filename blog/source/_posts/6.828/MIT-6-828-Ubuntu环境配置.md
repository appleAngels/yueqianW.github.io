---
title: MIT 6.828 Ubuntu环境配置
top: 0
date: 2020-03-23 10:29:57
tags:
# thumbnail: /../images/frontend.png
toc: true
comment: true
categories:
    - CS Course
    - MIT 6.828
---

<!-- Operating System Engineering -->

原本想在自己的 Mac 上安装，找了好几篇教程，都没办法安装上，所以没办法，只能先在 parallel 里装一个 ubuntu，再进行环境配置

<!-- more -->

首先输入 `objdump -i`

第二行应该出现 elf32-i386 字样；然后输入
`gcc -m32 -print-libgcc-file-name`  
应该出现`/usr/lib/gcc/i486-linux-gnu/version/libgcc.a`，或者`/usr/lib/gcc/x86_64-linux-gnu/version/32/libgcc.a`

如果上面都正常，说明不需要重新编译工具链；如果不正常，尝试输入下面的代码：

`sudo apt-get install -y build-essential gdb`
我的系统是 64 位的，需要装 32 位的库，之前没装就 make 了，出现了"**udivdi3"和"**muldi3"的错误，所以安装一下。

`sudo apt-get install gcc-multilib`
工具链已经安装完。

## 安装 qemu

qemu 需要从 github 上 clone 下来，最好 clone 原版但是速度慢，需要耐心等待。

`git clone https://github.com/mit-pdos/6.828-qemu.git qemu`
如果出现大意是 EOF 提前终止的提示，应该是因为 git 缓存不够，在命令行里输入

```
 sudo git config --global http.postBuffer 2000000000
 sudo git config --global https.postBuffer 2000000000
```

网上博客一般都只有 http 的 buffer 设置，但是 github 的协议是 https 的，我寻思着应该使用 https 的设置，但为了保险两个都设置了。然后安装以下几个文件：

```
sudo apt install libsdl1.2-dev
sudo apt install libtool-bin
sudo apt install libglib2.0-dev
sudo apt install libz-dev
sudo apt install libpixman-1-dev
```

## 设置 config

进入 qemu 目录，执行

```
./configure --disable-kvm --disable-werror --target-list="i386-softmmu x86_64-softmmu"
```

这里原指示是有一个 PFX 的选项，如果不填就默认存在/user/local 里。

注意要看你的系统有没有 python2，因为我的环境里只有 python3.6 但是后面报错了，如果没有 python2 要安装一下:

`sudo apt install python`
然后 cd 进 qemu 目录下，命令行输入

```
make
sudo make install
```

如果不是在 root 权限下，一定要加上 sudo，比如我之前不知，就出现了如下的错误：

```
install -d -m 0755 "/usr/local/share/qemu"
cannot change permissions of ‘/usr/local/share/qemu’: No such file or directory
```

## clone JOS

到 6.828 目录下，输入以下命令 clone JOS
`git clone https://pdos.csail.mit.edu/6.828/2018/jos.git lab`

## lab/make

如果环境都一样，按照我的步骤来现在应该没有问题，如果有问题百度或者谷歌大概都能解决了。这时候 clone 成功，来到 lab 文件夹下，命令行 make 即可。
`make qemu`

make 后会提示有出现一个 kernel 的 img 镜像文件，有这个，你就可以在 lab 文件夹下打开终端输入。

如果正常，会出现一个新的控制台窗口，这代表已经完成了。
