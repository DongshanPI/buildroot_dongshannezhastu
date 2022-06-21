# Buildoot For Dongshan NezhaSTU D1-H

## 简介

* 此套构建系统基于全志RISCV-64 Linux D1-H  芯片，适配了buildroot 2022lts主线版本，兼容了百问网的项目课程以及相关组件，真正做到了低耦合，高可用，使用不同的buildroot external tree规格，讲不同的项目 不同的组件分别管理，来实现更容易上手 也更容易学习理解。

### 目录结构说明

```bas
book@virtual-machine:~/buildroot_dongshannezhastu$ tree -L 2
.
├── br2lvgl
│   ├── Config.in
│   ├── configs
│   ├── external.desc
│   ├── external.mk
│   └── package
├── br2nezhastu
│   ├── board
│   ├── Config.in
│   ├── configs
│   ├── external.desc
│   ├── external.mk
│   └── LICENSE
├── br2qt5
│   ├── Config.in
│   ├── configs
│   ├── external.desc
│   ├── external.mk
│   └── package
├── buildroot-awol
│   ├── arch
│   ├── board
│   ├── boot
│   ├── CHANGES
│   ├── Config.in
│   ├── Config.in.legacy
│   ├── configs
│   ├── COPYING
│   ├── DEVELOPERS
│   ├── dl
│   ├── docs
│   ├── fs
│   ├── linux
│   ├── Makefile
│   ├── Makefile.legacy
│   ├── package
│   ├── README
│   ├── support
│   ├── system
│   ├── toolchain
│   └── utils
├── docs
├── README_cn.md
└── README.md
```

## 配置开发环境

### ubuntu-18.04

 运行环境配置： 此系统基于ubuntu18.04进行验证，需要安装如下依赖。

```bash
 sudo apt-get install -y which sed make binutils build-essential  gcc g++ bash patch gzip bzip2 perl  tar cpio unzip rsync file  bc wget python ncurses5  bazaar cvs git mercurial rsync scp subversion android-tools-mkbootimg
```

 安装完成后，执行如下命令进行开始编译操作。



### 获取sdk源码

* 默认源码都存放在github仓库内，请使用如下命令获取


```bash
book@virtual-machine:~$ git clone  https://github.com/DongshanPI/buildroot_dongshannezhastu
book@virtual-machine:~$ cd buildroot_dshannezhastu
book@virtual-machine:~/buildroot_dongshannezhastu$ git submodule update --init --recursive
book@virtual-machine:~/buildroot_dongshannezhastu$ git submodule update --recursive --remote
```



*  对于国内无法访问github的同学，可以使用国内备用gitee站点， 如下命令。

```bash
book@virtual-machine:~$ git clone  https://gitee.com/weidognshan/buildroot_dongshannezhastu
book@virtual-machine:~$ cd buildroot_dshannezhastu
book@virtual-machine:~/buildroot_dongshannezhastu$ git submodule update --init --recursive
book@virtual-machine:~/buildroot_dongshannezhastu$ git submodule update --recursive --remote
```



## 最小系统编译烧写

### 编译sdcard 最小系统镜像

```bash
book@virtual-machine:~/buildroot_dongshannezhastu$ cd buildroot-awol/
book@virtual-machine:~/buildroot_dongshannezhastu/buildroot-awol$ make  BR2_EXTERNAL="../br2lvgl  ../br2qt5 ../br2nezhastu"  dongshannezhastu_sdcard_core_defconfig

book@virtual-machine:~/buildroot_dongshannezhastu/buildroot-awol$ make 
```



### 烧写sdcard 最小系统镜像

编译完成后会在 output/images目录下输出 sdcard.img文件，将文件拷贝到Windows系统下使用 wind32diskimage烧写，或者使用dd if 烧录到tf卡内，

之后插到开发板上，即可启动。



### 编译spi nand最小系统镜像
```bash
book@virtual-machine:~/buildroot_dongshannezhastu$ cd buildroot-awol/
book@virtual-machine:~/buildroot_dongshannezhastu/buildroot-awol$ make  BR2_EXTERNAL="../br2lvgl  ../br2qt5 ../br2nezhastu"  dongshannezhastu_spinand_core_defconfig

book@virtual-machine:~/buildroot_dongshannezhastu/buildroot-awol$ make 
```




### 烧写spi nand最小系统镜像

编译完成后会在 output/images目录下输出 d1-h-nezhastu_uart0.img 文件，将文件拷贝到Windows系统下使用 使用 全志官方的  AllwinnertechPhoeniSuit 进行烧写。



## 项目示例配置

### 编译qt5 配置



### 编译lvgl8 配置



### 编译mqtt项目配置











