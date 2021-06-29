---
title: N2N搭建教程
date: 2019-05-27 17:37:54
tags:
- N2N
description: N2N异地组网搭建教程
categories:
- 异地组网
---


##   Centos 安装教程

 ```sh
   1. yum install subversion gcc-c++ openssl-devel git cmake  # 安装所需依赖包
   2. git clone  https://github.com/meyerd/n2n.git # (此版本是N2N_v2s 版本必须相同方可使用)
   3. cd n2n/n2n_v2
   4. mkdir build
   5. cd build
   6. cmake .. (如果报错升级一下 yum install make)
   7. make
   8. make install
   9. supernode -l 1000 # 端口为1000  请打开此端口的防火墙
   10. edge -d n2n -c mynetwork -k password -a 10.10.10.X -l xx.xx.xx.xx:1195
       #-d n2n 是网卡名称
       # -c  网络组名称
       # -k 是密码
       #-a 是本地边缘节点的ip
       #-l 是服务器的IP:port
 ```



   ## Windows

   下载一个n2n_v2s的客户端即可

   ## MAC

   mac 安装比较麻烦：

   ```shell
   brew install openssl #安装open ssl
   brew install cmake 
   brew cask install tuntap # 如果安装出错  又找不到解决办法   可以试试 重启电脑 再次安装 
   git clone  https://github.com/meyerd/n2n.git  #打开v2文件夹
   修改CMakeLists.txt
   #set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -I${OPENSSL_INCLUDE_DIR}")
   #替换为
   #set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -L${OPENSSL_ROOT_DIR}/lib -I${OPENSSL_INCLUDE_DIR}")
   #即添加了-L/usr/local/opt/openssl/lib这个选项
   mkdir build
   cd build
   cmake -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl ..
   make
   #启动命令：
   sudo ./edge -d n2n -c mynetwork -k password -a 10.10.10.60 -l xx.xx.xx.xx:1195 -f
   #-f 是前台运行
   #如果提示：ERROR: Unable to open tap device
   #查看是否有如下两个内核扩展
   ls /Library/Extensions/tap.kext
   ls /Library/Extensions/tun.kext
   校验内核扩展的参数
   find /Library/Extensions/{tap,tun}.kext/ -type f | xargs shasum
   加载内核扩展
   sudo /sbin/kextload /Library/Extensions/tap.kext
   sudo /sbin/kextload /Library/Extensions/tun.kext

   ```

##    OpenWrt

```shell
    路由器k2   n2n_v2s
    #下载地址  mipsel 下的stati下的edge
    github.com/lucktu/n2n  
    安装kmod-tun
    然后执行
    ./edge -d n2n -c mynetwork -k password -a 10.10.10.60 -l xx.xx.xx.xx:1195 -f
    防火墙添加设置接收
    window 添加路由
    route add 192.168.199.0 mask 255.255.255.0 10.10.10.60
    192.168.199.0 是对方内网IP  
    10.10.10.60 是对方N2N IP

    mac

    route -n add -net 192.168.199.0 -netmask 255.255.255.0 10.10.10.60


```

