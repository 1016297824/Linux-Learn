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