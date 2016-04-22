#用自己的数据训练py-faster-rcnn

##1. 数据集格式设置
参考了这篇博文：[http://blog.csdn.net/liumaolincycle/article/details/50540487]
基本就是模仿VOC的文件夹结构来建自己数据集的文件夹结构，然后给每个图标记bounding box位置，一个图写一个.txt文档，超级费时！枯燥！伤眼睛！2000多张图我标记得要疯了！
然后改写一下VOCdevkit的转成xml的.m脚本，转成PASCAL VOC数据集那样的格式blablabla……
就是参照那个博文改的反正。

##2. py-faster-rcnn程序修改
复制$FRCNN_ROOT/lib/datasets里的pascal_voc.py重命名个自己数据集名字的.py文件，比如mydata.py然后按照自己数据集的情况改里面的代码：
* self._classes里的类名，改成自己的；
* 改改什么image_path啊annotation啊，什么的
最好逐行过一遍，把voc的都改成自己数据集的。要改的挺多的好像。

在$FRCNN_ROOT/lib/datasets/factory.py里加上以下行：
```python
my_devkit_path = 'dir to your dataset'
for split in ['train', 'val', 'trainval', 'test']:
    name = '{}_{}'.format('mydata', split)
    __sets[name] = (lambda split=split: datasets.mydata(split, my_devkit_path))
```

然后在$FRCNN_ROOT/lib/fast_rcnn里的config.py，把_C.MODELS_DIR里的pascal_voc去掉！
然后在$FRCNN_ROOT/models里面复制一个pascal_voc文件夹命名为自己的，我这里用ZF模型，就改里面的ZF/faster_rcnn_alt_opt里面的文件，每个都点开来看一下，把num_classes、cls_score层的num_output改成自己的类别数+1（+1是__background__)，bbox_pred层的num_output改成(类别数+1)*4。

然后复制$FRCNN_ROOT/tools里的train_faster_rcnn_alt_opt.py重命名个自己的名字，比如train_faster_rcnn_my.py然后好像也没什么要改的代码……过一遍看一看么……

然后好像就可以train了（这么快？怎么好像改了好久……），在$FRCNN_ROOT下面：
```
./tools/train_faster_rcnn_my.py --net_name ZF --weights （finetune，下载在$FRCNN_ROOT/data里的ZF model） --imdb mydata_trainval
```
--imdb 就是自己的数据集，在factory.py里加的那个样式。

好像差不多就是这样吧，昨天晚上训练的，今天写，有点忘记了……哎哎