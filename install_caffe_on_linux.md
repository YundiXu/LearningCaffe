经过在windows下安装运行caffe的痛苦经历后，决定转战linux，毕竟caffe官方是基于linux的……

##基本依赖项
```bash
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler libatlas-base-dev libgflags-dev liggoogle-glog-dev liblmdb-dev libopencv-dev 
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
```

##NVIDIA驱动
```bash
sudo apt-get install nvidia-current
```

##CUDA
###先安装头文件：
```bash
sudo apt-get install linux-headers-$(uname -r)
```
###安装CUDA7.5(从官网下载的deb文件)：
```bash
sudo dpkg -i cuda-repo-ubuntu1404_7.5-18_amd64.deb  
sudo apt-get update  
sudo apt-get install cuda
```
###配置环境变量：
```bash
export PATH=/usr/local/cuda-7.5/bin:$PATH  
export LD_LIBRARY_PATH=/usr/local/cuda-7.5/lib64:$LD_LIBRARY_PATH
```
测试安装是否完成：
```bash
cuda-install-samples-7.5.sh  ~  
cd ~/NVIDIA_CUDA-7.5_Samples  
cd 1_Utilities/deviceQuery  
make
./deviceQuery
```
如果成功，会显示机子上安装的GPU的情况，运行结尾显示“Result = PASS”
###CUDA环境配置：
```bash
sudo nano /etc/ld.so.conf.d/cuda.conf
```
在`/usr/local/cuda/lib64`后，换行加上`/lib`
执行：
```bash
sudo ldconfig -v
```

##CUDNN
官网下载cudnn_v4的包，解压后，进入解压得到的cuda文件夹
```bash
cd include
sudo cp cudnn.h /usr/local/cuda/include/
cd ../lib64
sudo cp lib* /usr/local/cuda/lib64/
sudo ldconfig -v
```

##安装Caffe
```bash
git clone git://github.com/BVLC/caffe.git
cp Makfile.config.example Makefile.config
```
修改Makefile.config，去掉cudnn的注释，然后开始安装：
```bash
make all
make test
make runtest
```
