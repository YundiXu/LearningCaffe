##1. fast-rcnn github官方readme的安装指导（for demo）
从github上clone到Fast RCNN的仓库。生成cython模块，caffe和pycaffe。
```bash
$ git clone --recursive https://github.com/rbgirshick/fast-rcnn.git
$ cd lib
$ sudo make
$ cd ../caffe-fast-rcnn
```
像装caffe一样，copy Makefile，修改Makefile，去掉USE_CUDNN和WITH_PYTHON_LAYER的标注。
然后
```bash
$ sudo make
$ sudo make pycaffe
```
这里绕了个大弯见到鬼了……ubuntu_python_install那篇写道花了好长时间和好多空间装opencv3.1.0，结果呢，后来还是`make uninstall`了，删除线划掉！因为apt-get装的python-opencv是基于2.4.8的，libopencv-dev也是2.4.8的，这样不是匹配的刚刚好么，为毛要去高攀3.1.0！反正就是会报错，uninstall了就没错了，`make pycaffe`成功！

##2. 跑demo
然后就按照官方readme跑demo：
```bash
# 进到py-faster-rcnn根目录
$ cd ..
$ sudo ./tools/demo.py
```
期间遇到各种`No module named XXX`，就用万能的“sudo apt-get install XXX”装那个module就好，参考apt-get_check_list那篇，大概是在这个阶段装了`python-scipy` `python-matplotlib` `python-sklearn` `python-skimage` `python-h5py` `python-protobuf` `python-leveldb` `python-networkx` `python-nose` `python-pandas` `python-gflags` `python-yaml`这些。有人在装python的时候直接装了anaconda，里面包含了很多python包，不知道全不全，可以试试装装看，我还是缺什么装什么好了，也方便做个checklist。
跑出来结果么就是类似下面这个鬼样的：
![](https://github.com/YundiXu/LearningCaffe/blob/master/imgs/figure_3.png?raw=true)
![](https://github.com/YundiXu/LearningCaffe/blob/master/imgs/figure_4.png?raw=true)
![](https://github.com/YundiXu/LearningCaffe/blob/master/imgs/snapshot1.png?raw=true)

欢呼！！！！清明节能好好过了……

--------------0503加---------------
有个不错的小技巧：把数据集放在一个地方，然后快捷方式到要用它的框架、模型、网络那里。像这样——
```bash
$ cd $FRCN_ROOT/data
$ ln -s $VOCdevkit VOCdevkit2007
```
