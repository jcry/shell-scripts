# shell-scripts
Linux Shell Scripts
## KCPTUN
脚本已更新到v20，请以前版本的朋友可以直接更新，请先切换到 kcptun.sh 文件目录下运行

     wget --no-check-certificate https://github.com/kuoruan/shell-scripts/raw/master/kcptun/kcptun.sh
     chmod +x ./kcptun.sh
     ./kcptun.sh
 
### Supervisor 相关命令：
    1
    service supervisord {start|stop|restart|status}
### Kcptun 相关命令：
    1
    supervisorctl {start|stop|restart|status} kcptun
Supervisor 启动的时候会同时启动 Kcptun，运行 kcptun 相关命令时先确保 Supervisor 已启动。

### 其他说明
注意：以下命令需要在 kcptun.sh 同级目录下执行

1.如果想加速另一个端口，请使用

    ./kcptun.sh add

2.查看日志

    ./kcptun.sh log <id>
    
3.查看配置信息

    ./kcptun.sh config <id>

如果你记不住以上命令，请使用

    ./kcptun.sh help

============================================================================================
## OpenVZ 平台 Google BBR 一键安装脚本

已测试通过的系统： Ubuntu 14.04 x64、Ubuntu 16.04 x64、CentOS 6 x64、CentOS 7 x64 只支持 64 位系统，要求 glibc 版本 2.14 以上。

    wget https://raw.githubusercontent.com/kuoruan/shell-scripts/master/ovz-bbr/ovz-bbr-installer.sh
    chmod +x ovz-bbr-installer.sh
    ./ovz-bbr-installer.sh

如需卸载，请使用：

    ./ovz-bbr-installer.sh uninstall

### 多端口加速
安装的时候只配置了一个加速端口，但是你可以配置多端口加速，配置方法非常简单。 修改文件

    vi /usr/local/haproxy-lkl/etc/port-rules

使用 systemctl 或者 service 命令来启动、停止和重启 HAporxy-lkl：

    systemctl {start|stop|restart} haproxy-lkl
    
    service haproxy-lkl {start|stop|restart}
    
/usr/local/haproxy-lkl/etc/haproxy.cfg 这个文件是通过 port-rules 自动生成的，每次启动都会重新生成，所以直接修改它的配置没用。 如果想要自定义配置，请修改启动文件：

    vi /usr/local/haproxy-lkl/sbin/haproxy-lkl
    
### 判断 BBR 已正常工作
判断 bbr 是否正常启动可以尝试 ping 10.0.0.2，如果能通，说明 bbr 已经启动。

然后检查 iptables 规则

    iptables -t nat -nL
