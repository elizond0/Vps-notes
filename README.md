# Vps-notes

## 1.Vultr 搭建ssr服务器

* 1.1 前期准备
1. xshell - ssh终端工具
2. vultr - vps服务器供应商
3. shadowSocksR - 代理工具

* 1.2 vultr有ip地址和root秘钥，在xshell新建连接使用
  * 检测ip是否被墙，[内](http://coolaf.com/tool/port)[外](https://www.yougetsignal.com/tools/open-ports/)网ip&端口扫描22ssh

* 1.3 部署ssr服务器,CentOS/Debian/Ubuntu ShadowsocksR单/多端口一键管理脚本

```dos
/* 此处bash安装库若有forbid提示，则说明该项目已经失效，需要另外寻找 */
yum -y install wget
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

* 1.4 安装后配置命令 bash ssr.sh
1. 安装 SSR 键入数字1
2. 输入端口号 例如8989
3. 输入ssr服务器连接密码
4. 加密方式选择aes-256-cfg，键入数字10
5. ssr协议插件origin 键入数字1
6. ssr混淆插件plain 键入数字1
7. 设备数限制、单线程限速、端口总限速看个人情况配置
8. 确认完配置信息后会显示SSR账号信息，记得保存

* 1.5 CentOS7默认防火墙阻止SS端口，需要手动放行，PORT替换成之前的配置的端口号

```dos
firewall-cmd --permanent --add-port=PORT/tcp
firewall-cmd --reload
```

* 1.6 谷歌BBR加速，输入下列代码安装完成后重启服务器reboot即可

```dos
yum -y install wget
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh
chmod +x bbr.sh
./bbr.sh
```

* 1.7 使用SSR代理客户端连接，根据账号配置信息连接

* 1.8 个人SSR账号备份

<!-- ```html
 ShadowsocksR账号 配置信息：

 I  P	    : 45.77.236.45
 端口	    : 8989
 密码	    : qweasdzxc321
 加密	    : aes-256-cfb
 协议	    : origin
 混淆	    : plain
 设备数限制 : 0(无限)
 单线程限速 : 0 KB/S
 端口总限速 : 0 KB/S
 SS    链接 : ss://YWVzLTI1Ni1jZmI6cXdlYXNkenhjMzIxQDQ1Ljc3LjIzNi40NTo4OTg5
 SS  二维码 : http://doub.pw/qr/qr.php?text=ss://YWVzLTI1Ni1jZmI6cXdlYXNkenhjMzIxQDQ1Ljc3LjIzNi40NTo4OTg5
 SSR   链接 : ssr://NDUuNzcuMjM2LjQ1Ojg5ODk6b3JpZ2luOmFlcy0yNTYtY2ZiOnBsYWluOmNYZGxZWE5rZW5oak16SXg
 SSR 二维码 : http://doub.pw/qr/qr.php?text=ssr://NDUuNzcuMjM2LjQ1Ojg5ODk6b3JpZ2luOmFlcy0yNTYtY2ZiOnBsYWluOmNYZGxZWE5rZW5oak16SXg

  提示:
 在浏览器中，打开二维码链接，就可以看到二维码图片。
 协议和混淆后面的[ _compatible ]，指的是 兼容原版协议/混淆。
``` -->
