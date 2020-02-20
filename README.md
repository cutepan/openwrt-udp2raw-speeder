# luci-udptools
openwrt luci for udpspeeder and udp2raw

使用方法：

安装需要的环境

apt-get install subversion build-essential libncurses5-dev zlib1g-dev gawk git ccache gettext libssl-dev xsltproc wget unzip python time
apt-get install libcloog-isl-dev
ln -s /usr/lib/x86_64-linux-gnu/libisl.so /usr/lib/libisl.so.10

添加 src-git lienol https://github.com/cutepan/openwrt-udp2raw-speeder 到 OpenWRT源码根目录feeds.conf.default文件
然后执行

./scripts/feeds update -a
./scripts/feeds install -a
或者你可以把该源码手动下载或Git Clone下载放到OpenWRT源码的Package目录里面，然后编译。 如果你使用的是Luci19，请编译时选上"luci","luci-compat","luci-lib-ipkg"后编译



关于luci-udptools
https://www.atrandys.com/2018/1247.html

1、需要openwrt路由器安装了udp2raw和udpspeeder软件。

2、支持udp2raw和udpspeeder串联使用，即：XX软件 + udpspeeder + udp2raw的方案。

3、无法单独使用udp2raw或udpspeeder，暂时不支持。


这里只能配置udp2raw串联udpspeeder，单独使用的功能目前不支持。配置界面参数讲解：

服务器IP：你的VPS的ip地址

服务器udp2raw端口：你的VPS运行的udp2raw服务端监听的端口

客户端IP：即本地监听的ip，一般设置为127.0.0.1，配合其他软件时（ss为例），ss的ip需要指向127.0.0.1

客户端udpspeeder端口：即udpspeeder的本地监听端口，配合其他软件使用时（ss为例），ss配置里的端口要和它一致

密码：即udp2raw的传输加密密码，需要和服务端udp2raw的密码一致

Fec参数：即udpspeeder的fec参数，视频场景设置为 20:10  游戏场景设置为 2:4

Fec延迟：即udpspeeder的延迟参数，视频场景可以填 8 游戏场景填写 0

注意：配置完参数后，要在启动页面重新启动服务才能生效。

三、搭配其他软件

注意：如果XX软件是openvpn/wireguard等全局使用VPN传输的软件，那么可以直接串联udp工具使用，但如果是SS/SSR等软件，他们使用tcp和udp传输，那么此类软件不能单独使用udptools，还需要tcp转发工具，后面我们会做一期教程专门介绍一下用法。

1、需要你的VPS搭建了服务端，形式为

udp2raw—->udpspeeder—->XX软件服务端

2、路由器中安装了XX软件的客户端，可以修改此类软件的配置文件，将ip指向客户端IP，将端口指向客户端udpspeeder端口即可。

XX软件客户端—->udpspeeder—->udp2raw

好了教程到此结束，个人能力有限，写得这个luci-udptools功能也有限，另外是否有未知问题还不明，待有时间再完善吧，各位小伙伴使用遇到的问题可以留言。