# ipACOM风电边缘计算联邦管理平台使用说明

## 安装说明

### 准备工作

准备一台已装linux操作系统的主机，要求内存不低于4G，且确保已安装docker

### 安装

将rtfedoral_install.run拷贝到linux系统的install_dir目录中，install_dir可自由指定，如路径/opt/

进入install_dir目录，以管理方式运行安装程序, sudo ./rtfedoral_install.run

### 验证

访问http://ipaddr:18000, 若能打开网页，说明安装成功,ipaddr为linux主机的ip地址。

可以通过成员管理添加单个成员和批量添加多个成员。

可通过固件升级进行平台和算法仓库的升级。

## 使用说明

### 使用要求

在已安装联邦管理的linux主机上,开启ftp等文件服务,文件目录为/rtfdata/fedoral_working,外部系统可以对该目录及子目录文件进行存取，目录树为，其中shellcmd目录是远程执行脚本的工作目录，update_workdir是远程程序更新的工作目录。
```
remote_working/
├── shellcmd
└── update_workdir
    ├── EcsUpdate
    └── UpdateFeed
```
### 联邦管理包含功能

#### 周期读取终端状态存数据库(mysql)
参考《前置系统远程管理方案》
#### 检测shellcmd目录下的脚本，并执行。

#### 算法仓库更新

检测update_workdir/EcsUpdate下的更新包，执行更新操作，并将执行结果输出到update_workdir/UpdateFeed目录，参考《前置系统远程管理方案》。

