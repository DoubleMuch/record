### ooqp安装记录
ooqp参考链接
https://blog.csdn.net/qq_42488462/article/details/114393626


./configure 


make


make后如果libma27.a报错，需要先将MA27/src文件中的一个libma27.a的静态库文件拷问到ooqp文件中之后，开始安装


sudo install make
（会报错，但好像不影响，暂时没有管）


sudo apt install texlive-latex-base(解决问题）


参考链接
https://blog.csdn.net/Awesomewan/article/details/109495670

需要先安装以下两个：
#### 安装blas（顺利）
参考链接https://blog.csdn.net/mlnotes/article/details/9676269
#### 安装ma27（有问题）
./config 或 bash ./configure CPPFLAGS="-fPIC" CFLAGS="-fPIC" FFLAGS="-fPIC"

sudo make install 
报错，关于config.sub和sonfig.guess，把ooqp中这两个文件复制过来。
### Ubuntu环境下OOQP优化库的基本使用
https://qiaoxu123.github.io/post/ubuntu-ooqp-useguide/



passwd 改用户密码
sudo passwd 改root密码


* 妙算备份与刷机

    * 备份到根目录的backup.tgz里面 
        * cd /
        * su
        * tar cvpzf backup.tgz --exclude=/proc --exclude=/lost+found --exclude=/backup.tgz --exclude=/mnt --exclude=/sys --exclude=/media /
    * 刷机
        * 备份uuid 
            * sudo cp -pdr fstab ./外置存储
        * 解压
            * cd /
            * su
            * sudo tar xvpfz ./外置存储backup.tgz 
        * 恢复fstab
        * 覆盖/boot/grub/grub.cfg文件中的UUID号（主分区的，用fstab中的主分区uuid覆盖掉grub.cfb中的）



onboardsdk

cd Onboard-SDK
mkdir build
cd build
cmake ..
make djiosdk-core
sudo make install djiosdk-core


ceres 
cd crers
    mkdir build
    cd build
    cmake ..
    make 
   make install

sudo apt-get install ros-kinetic-ddynamic-reconfigure


realsense2 missing
参考
https://github.com/IntelRealSense/librealsense/blob/development/doc/distribution_linux.md


rosrun global_fusion global_fusion_node 
rosrun vins vins_node /home/dji/tfes/src/VINS-Fusion/config/realsense_d435i/realsense_stereo_imu_config.yaml
rosrun global_fusion global_fusion_node 

 rospack find  packagename 






