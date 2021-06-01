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
**服务器操作**
* mkdir frp  cd frp
* wget https://github.com/fatedier/frp/releases/download/v0.22.0/frp_0.22.0_linux_amd64.tar.gz [版本点这里](https://github.com/fatedier/frp/releases)  
* tar -zxvf frp_0.22.0_linux_amd64.tar.gz  
* cp -r frp_0.22.0_linux_amd64 frp 重命名方便操作  
* 服务端只需要关注frps frps.ini frps_full.ini 可以删除 rm -rf frpc frpc.ini frpc_full.ini
* vim frps.ini
