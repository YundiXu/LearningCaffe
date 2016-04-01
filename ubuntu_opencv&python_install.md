#Python安装配置
之前有apt-get了python-dev，现在安装一些有用的工具。参考[http://ouxinyu.github.io/Blogs/20140723001.html](http://ouxinyu.github.io/Blogs/20140723001.html)
~~###1. 安装opencv3.1.0
之前装了libopencv-dev了，版本是2.4.8，但是发现后面要装python-opencv的时候报错：“could not find any downloads that satisfy the requirement python-opencv”。然后决定跟着网上的指导装一下opencv最新版，然后再装python-pencv。
先装一些依赖库：
```bash
$ sudo apt-get -y install build-essential libxine-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libqt4-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip
```
然后下载源码opencv-3.1.0.zip，编译：
```bash
unzip opencv-3.1.zip
cd ~/opencv-3.1.0
mkdir release
cd release
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local ..
make
sudo make install
```
要花好长时间……等待啊等待……~~
###2. 安装IDE运行环境
安装Spyder，因为它内置了 iPython 环境，Caffe有不少的程序是基于 iPython 环境完成的。安装方法很简单，直接在Ubuntu软件中心搜索“spyder”即可安装。
###3. 安装iPython NoteBook
```bash
$ sudo apt-get install -y ipython-notebook pandoc
```
启动(自动打开浏览器):
```bash
$ ipython notebook
```
###4. 一些python包
为了之后跑fast-rcnn和faster-rcnn，需要Python安装包：cython，python-opencv，easydict
装一个python包管理器pip先：
```bash
$ sudo apt-get install python-pip
```
再装那三个包：
```bash
$ sudo pip install cython
$ sudo apt-get install python-opencv
$ sudo pip install easydict
```
python-opencv包用pip下载不了，用apt-get可以。