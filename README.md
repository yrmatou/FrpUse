### frp功能很强大可以做很多事情，这里我只做 内网穿透实现web服务简单介绍  
做公众号 接口配置信息内网穿透心得，吐血的过程  

[官网地址](https://github.com/fatedier/frp)

----
### 简图
![image](https://user-images.githubusercontent.com/21699695/120302054-13879100-c300-11eb-81d8-3d06097b3990.png)
----
### 准备
* 公网服务器，SecureCRT(我用的，可以用其他软件)，window(我本地电脑)  
----
### 开始
**服务器设置**
* mkdir frp  cd frp
* wget https://github.com/fatedier/frp/releases/download/v0.22.0/frp_0.22.0_linux_amd64.tar.gz [版本点这里](https://github.com/fatedier/frp/releases)  
* tar -zxvf frp_0.22.0_linux_amd64.tar.gz  
* cp -r frp_0.22.0_linux_amd64 frp 重命名方便操作  
* 服务端只需要关注frps frps.ini frps_full.ini 可以删除 rm -rf frpc frpc.ini frpc_full.ini
* vim frps.ini
```json
[common]
bind_port = 7000 # 表示客户端和服务端连接的端口，默认是7000，也可以修改，只要跟客户端的bind_port保持一致就可以
token = 12345678 # 跟客户端设置的token保持一致即可
vhost_http_port = 10080 # 用于服务端主机访问的端口，需要再vps安全组里添加此端口才行。或者这里使用nginx内部转发到此端口就可
```
* 配置好启动 ./frps -c frps.ini 或者 nohup ./frps -c frps.ini &（后台运行）  
**客户端设置（我的是window系统）**
* 客户端只需要关注frpc frpc.ini frpc_full.ini 可以删除 frps frps.ini frps_full.ini  
* 双击 frpc.ini 编辑
```json
[common]
server_addr = xx.xx.xx.xx # 使用的是公网机器IP。
server_port = 7000 # 服务端设置的端口 可修改自己的
token = 12345678 # 必须和远程服务器一致

[web]
type = http # 为代理的类型，web服务设置为http类型
local_port = 9003 # 为本地客户端启动的web服务 修改成自己的
custom_domains = xx.xx.xx # 为外网VPS绑定的访问域名或者机器的IP，比如 www.q.xyz
```
* 配置好启动 ./frpc -c frpc.ini 或者 nohup ./frpc -c frpc.ini &（后台运行）  
使用外网IP或者域名:vhost_http_port，即custom_domains:10080，访问自己内网启动的web服务了

### 我这里开发没有用开放服务器安全组的方式，我用的是nginx代理端口访问
![image](https://user-images.githubusercontent.com/21699695/120308882-2a7db180-c307-11eb-9dc3-0104a99b829e.png)  
直接 https://www.q.xyz/wechat/v1/token 这样即可访问到本地指定的端口服务
