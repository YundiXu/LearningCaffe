之前在windows下已经成功装上caffe了，并且用GPU跑finetune例程没有问题。

之前用GPU训练的时候风扇声音都很大，同事颇具怨言……然后昨天上午突然断电之后，世界都安静了……再开机，还是很安静，再跑跑，还是很安静，咦！有点不习惯哦！
然后狗血的事情发生了……
跑着跑着大概CaffeNet在iteration=400的时候，突然报错：
```
Check failed: error == cudaSuccess ( 30 vs. 0) unknown error
```
然后`caffe.exe停止运行`了。

经历各种重装，转到Ubuntu下去跑，还是这样报错，越来越感觉到安静的不可思议！
谷歌了，别人遇到类似情况说是显卡版本太低，新版CUDA不支持，但是不会呀，之前用的好好的呀！我们用的显卡computing capability 3.7呐，远大于2.0呀！

然后经过几次重启，测deviceQuery，跑caffe训练，挂掉……发现，刚启动电脑是测deviceQuery是有4块GPU的（不好意思，比较土豪），跑caffe挂掉之后，再测deviceQuery就只剩2块了，再跑跑看，就检测不到显卡了。好像知道了什么！

然后安了个测GPU/CPU温度的软件`AIDA64`，就眼看着caffe跑着显卡温度越来越高，到93°了！caffe挂掉，AIDA64里显卡少掉2块。

好了，应该是风扇坏掉了，显卡过热自我保护而断电了，然后就挂了，真相就是这样的！
好累啊……