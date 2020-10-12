# 在centos上部署rtframe及相关组件，需要注意几个问题


* docker run -w映射目录容器内的程序对映射的目录没有写权限，这个和selinux鉴权有关，最直接的方式就是关闭它
修改/etc/selinux/config,将SELINUX=enforcing 修改为 SELINUX=disabled，重启生效

* nsqadmin的管理功能使用不正常，不能正确解析生成的节点域名，这个和firewalld.service有关，最直接的方式就是关闭

systemctl disable firewalld.service


* 安装采集卡驱动需要安装依赖包

 dnf install kernel-devel

 dnf install elfutils-libelf-devel
 
* kworker/0:1+kacpid内核导致CPU占用高分析，电源管理ACPI

grep . -r /sys/firmware/acpi/interrupts

echo disable > /sys/firmware/acpi/interrupts/gpe6F

sudo perf record -g -a sleep 10

perf report -i perf.data


* 关于centos异常关机可能导致的文件系统崩溃的可能性分析

目前的基本理解，用xfs或ext3/4等日志文件系统，在写数据之前会先写日志，确保出错后能够回滚。

但存在一种可能，就是存储器写缓存打开，回写的时候不一定是顺序写，这样也可能导致xfs出错，所以要么启用barrier,要么关闭写缓存

安装hdparm,关闭写缓存。
