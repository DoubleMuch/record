### Btraj记录
#### 20210707
1.https://github.com/HKUST-Aerial-Robotics/Btraj  代码一开始编译的问题，解决办法：


在 plan_utils/rviz_plugins的CMAKELISTS中第83行的add_library(${PROJECT_NAME} ${SOURCE_FILES})后面添加一行


add_dependencies(${PROJECT_NAME} multi_map_server_generate_messages_cpp)


2.run simulation.launch 中鼠标点击设置航点不动的问题，主要原因way_pointgenerate.cpp中第174行if (msg->pose.position.z > 0) 限制了要求读回的鼠标点击的坐标z要大于0才可以，但实验发现不论鼠标点击哪里，获得的xy,都比较正常，z一直为0，不知是我的电脑问题还是由bug，解决办法，修改 plan_utils/rviz_plugins/pose_tool.cpp第90行改成


Ogre::Plane ground_plane( Ogre::Vector3::UNIT_Z, 1.0f );设置点击鼠标左键触发事件的时候z轴强制设置为1，这个后续需要继续改，暂时这样可以通过鼠标控制xy的目标点


3.b_traj_node.cpp中pointInflate函数里面vector<pcl::PointXYZ> infPts(20);不应该初始化为20，因为后面添加是用push_back导致前20个其实是空点，增加了无效点云的数量，使可视化卡顿。初始化直接为0就好。



4.待解决！另有还有一个问题没解决的就是，在相邻点云膨胀的时候，会出现许多重复的点云，也都一并放入了cloud_inflation中，也会增加卡顿。如果可以，可以在前面添加一个去除在同一个栅格中的点云的步骤、



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






