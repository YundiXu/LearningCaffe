Ubuntu系统属性：
```
$ uname -a
```

```
Linux ubuntu 3.19.0-51-generic #58~14.04.1-Ubuntu SMP Fri Feb 26 22:02)58 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
```
4块Nvidia Tesla K80显卡 + ASPEED VGA显卡。

之前写到在ubuntu上安装完成caffe，但是之后在忙别的事，都没开过ubuntu系统，结果今开ubuntu准备继续caffe时，开机黑屏，只有右上角光标忽闪忽闪……
折腾了半天啊啊啊！试各种网上给出的`purge`掉nvidia-*，重装cuda，balabalabala……最后我发觉问题原因应该是：安装cuda时安装了nvidia显卡驱动，然后ubuntu启动时默认选用了新安装的驱动来启动图形界面，啊啊啊，然后就抽抽了……嗯。

最后成功解决的方法超简单……

`ctrl+alt+F1` 进入命令行模式，会经常闪回黑屏，闪回黑屏就再按`ctrl+alt+F1`。登陆，然后简单一句：
```
sudo prime-select intel
```

搞定。

就是切换首要驱动为原先的intel来启动图形界面。
好累啊……