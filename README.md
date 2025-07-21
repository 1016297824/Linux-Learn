Linux Learn

1.远程连接 MySQL 问题解决：
(1)查看用户和主机配置：
SELECT User,Host FROM mysql.user;
(2)开放 3306 端口
    1)查看 3306 端口状态：
        sudo firewall-cmd --query-port=3306/tcp
    2)开放 3306 端口：
        sudo firewall-cmd --permanent --add-port=3306/tcp
    3)重启防火墙：
        sudo firewall-cmd --reload

2.MySQL版本冲突解决：
(1)查看已安装的MySQL包：
    rpm -qa | grep mysql
(2)卸载冲突的仓库（以MySQL5.7为例）：
    yum remove mysql57-community-release
(3)清理缓存：
    yum clean all

3.关于Ubuntu24无法安装MySQL5.7解决：
(1)安装libtinfo5依赖：
    1)sudo apt update
    2)wget http://security.ubuntu.com/ubuntu/pool/universe/n/ncurses/libtinfo5_6.3-2ubuntu0.1_amd64.deb
    3)sudo apt install ./libtinfo5_6.3-2ubuntu0.1_amd64.deb
(2)安装libaio1和libaio-dev依赖：
    1)curl -O http://launchpadlibrarian.net/646633572/libaio1_0.3.113-4_amd64.deb
    2)sudo dpkg -i libaio1_0.3.113-4_amd64.deb
    3)sudo apt-get install libaio-dev
(3)以安装mysql 5.7.23为例：
    1)创建目录并进入：
        mkdir -p /opt/mysql && cd /opt/mysql
    2)下载压缩包
        wget https://downloads.mysql.com/archives/get/p/23/file/mysql-server_5.7.23-1ubuntu18.04_amd64.deb-bundle.tar
    3)解压：
        tar xvf ./mysql-server_5.7.23-1ubuntu18.04_amd64.deb-bundle.tar
    4)安装./libmysql*：
        sudo apt-get install ./libmysql*
    5)安装客户端1：
        sudo apt-get install ./mysql-community-client_5.7.23-1ubuntu18.04_amd64.deb
    6)安装客户端2：
        sudo apt-get install ./mysql-client_5.7.23-1ubuntu18.04_amd64.deb
    7)安装服务端1：
        sudo apt-get install ./mysql-community-server_5.7.23-1ubuntu18.04_amd64.deb
    8)安装服务端2：
        sudo apt-get install ./mysql-server_5.7.23-1ubuntu18.04_amd64.deb
(4)参考：
    https://www.yunieebk.com/mysql5_7_23/

4.Linux虚拟机扩容：
(1)安装工具：
    sudo apt-get install gparted
(2)启动工具：
    sudo gparted
(3)遇到读写权限问题：
    1)查看挂载目录：挂载于/mounted on 后的内容，一般为两个
    2)重新挂载（具体路径看挂载目录）：
        sudo -i
        mount -o remount -rw /
        mount -o remount -rw /var/snap/firefox/common/host-hunspell

5.远程连接放行
(1)方法一：关闭防火墙
    1)关闭：
        systemctl stop firewalld
    2)关闭开机自启：
        systemctl disable firewalld
(2)方法二：放行指定端口
    1)放行tcp规则端口并设置永久生效：
        firewall-cmd --add-port=[端口号]/tcp --permanent
    2)重新加载防火墙：
        firewall-cmd --reload