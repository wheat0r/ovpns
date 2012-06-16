麦叔自用 openvpn 全套解决方案
=====

适用于 Linux 系统的 openvpn 全套解决方案  
路由表信息来自 [jimmy/chnroutes](https://github.com/jimmyxu/chnroutes) 的更新脚本。使用 iproute2 的 ip -batch 方式解决 [chnroutes](https://code.google.com/p/chnroutes/) 加载过慢的问题，并在每次连接时重置可能被污染过的 dnsmasq 缓存  
使用 dnsmasq 解决单纯使用 8.8.8.8 导致的解析问题（修改自[火星猫提供的配置](http://wiki.felixc.at/Dnsmasq)）

##用法##

**先根据各个文件中的注释进行必要的修改**  
安装 openvpn 、 dnsmasq 和 iproute2  
把 dnsmasq.conf 放进 /etc  
以守护进程方式启动 dnsmasq  
在你的网络管理器里设置 dns 为 `127.0.0.1`  
执行 `python2 chnroutes.py`  
在生成的 vpn-up.sh 中 ip -batch 命令之前一行加入以下内容  
> rc.d restart dnsmasq &&

这里也准备了现成的路由表脚本 vpn-up.sh 和 vpn-down.sh 用作参考，但是仍然建议使用脚本重新生成  
在你的配置文件里写入  
> script-security 2  
    up "/bin/sh /文件路径/vpn-up.sh"  
    down "/bin/sh /文件路径/vpn-down.sh"  

然后就玩蛋去吧