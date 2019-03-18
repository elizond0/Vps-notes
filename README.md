# Vps-notes

## 1.Vultr 搭建 ssr 服务器

### 1.1 前期准备

1. xshell - ssh 终端工具
2. vultr - vps 服务器供应商
3. shadowSocksR - 代理工具

### 1.2 vultr 有 ip 地址和 root 秘钥，在 xshell 新建连接使用

- 检测 ip 是否被墙，[内](http://coolaf.com/tool/port)[外](https://www.yougetsignal.com/tools/open-ports/)网 ip&端口扫描 22ssh

### 1.3 部署 ssr 服务器,CentOS/Debian/Ubuntu ShadowsocksR 单/多端口一键管理脚本

- 安装 ssr

```dos
/* 此处bash安装库若有forbid提示，则说明该项目已经失效，需要另外寻找 */
yum -y install wget
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

- 如果加密协议选用 chacha 系列，需要另外安装 libsodium，也可以通过工具自动安装

```dos
# 因为这库是基于C语言的，所以我们先去安装GCC
yum -y groupinstall "Development Tools"
# 下载最新稳定版本
wget https://download.libsodium.org/libsodium/releases/LATEST.tar.gz
# 解压
tar xf LATEST.tar.gz && cd libsodium-1.0.11 # libsodium-1.0.11按照实际解压后的文件夹名
# 编译
./configure && make -j4 && make install
echo /usr/local/lib > /etc/ld.so.conf.d/usr_local_lib.conf
ldconfig
```

### 1.4 安装后配置命令 bash ssr.sh

1. 安装 SSR 键入数字 1
2. 输入端口号 例如 8989
3. 输入 ssr 服务器连接密码
4. 加密方式选择 aes-256-cfg，键入数字 10（建议 chacha20-ietf）
5. ssr 协议插件 origin 键入数字 1（建议 auth_sha1_v4_compatible）
6. ssr 混淆插件 plain 键入数字 1 （建议 tls1.2_ticket_auth_compatible）
7. 设备数限制、单线程限速、端口总限速看个人情况配置
8. 确认完配置信息后会显示 SSR 账号信息，记得保存

### 1.5 CentOS7 默认防火墙阻止 SS 端口，需要手动放行，PORT 替换成之前的配置的端口号

```dos
firewall-cmd --permanent --add-port=PORT/tcp
firewall-cmd --reload
```

### 1.6 谷歌 BBR 加速，输入下列代码安装完成后重启服务器 reboot 即可

```dos
yum -y install wget
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh
chmod +x bbr.sh
./bbr.sh
```

### 1.7 使用 SSR 代理客户端连接，根据账号配置信息连接

### 1.8 个人 SSR 账号备份

<!-- ```html
 ShadowsocksR账号 配置信息：

 I  P	    : 149.28.187.124
 端口	    : 233
 密码	    : qweasdzxc321
 加密	    : chacha20-ietf
 协议	    : auth_sha1_v4_compatible
 混淆	    : tls1.2_ticket_auth_compatible
 设备数限制 : 0(无限)
 单线程限速 : 0 KB/S
 端口总限速 : 0 KB/S
 SS    链接 : ss://Y2hhY2hhMjAtaWV0Zjpxd2Vhc2R6eGMzMjFAMTQ5LjI4LjE4Ny4xMjQ6MjMz
 SS  二维码 : http://doub.pw/qr/qr.php?text=ss://Y2hhY2hhMjAtaWV0Zjpxd2Vhc2R6eGMzMjFAMTQ5LjI4LjE4Ny4xMjQ6MjMz
 SSR   链接 : ssr://MTQ5LjI4LjE4Ny4xMjQ6MjMzOmF1dGhfc2hhMV92NDpjaGFjaGEyMC1pZXRmOnRsczEuMl90aWNrZXRfYXV0aDpjWGRsWVhOa2VuaGpNekl4
 SSR 二维码 : http://doub.pw/qr/qr.php?text=ssr://MTQ5LjI4LjE4Ny4xMjQ6MjMzOmF1dGhfc2hhMV92NDpjaGFjaGEyMC1pZXRmOnRsczEuMl90aWNrZXRfYXV0aDpjWGRsWVhOa2VuaGpNekl4


  提示:
 在浏览器中，打开二维码链接，就可以看到二维码图片。
 协议和混淆后面的[ _compatible ]，指的是 兼容原版协议/混淆。
``` -->
