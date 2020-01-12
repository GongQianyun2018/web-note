# VPS搭建
## 客户端安装
### 下载shadowsocks

> sudo apt-get install python-pip

> sudo pip install shadowsocks

> sslocal -help
* 配置
 
 可以选择配置文件运行，也可以直接在命令行中运行，这里选择的是第一种。在/home/gqy/ss_config中新建ss.json文件，文件信息如下：
 ```json
 {
	"server":"103.114.***.***",
	"server_port":8388,
	"local_address":"127.0.0.1",
	"local_port":1080,
	"password":"keyword",
	"timeout":300,
	"method":"ase-256-cfd"
}
 ```
 输入以下命令运行：
 > sslocal -c /home/gqy/ss_config/ss.json
 
 若出现以下类似效果就表示连接成功：
 ![image1](https://github.com/GongQianyun2018/web-note/blob/master/img/day2_VPS_1.png)

在这里出现了一个错误：EVP_CIPHER_CTX_cleanup。这是由于Ubuntu18.04下由于升级openssl至1.1.0以上版本导致shadowsocks服务出现EVP_CIPHER_CTX_cleanup错误而无法启动的问题这是由于在openssl 1.1.0中废弃了EVP_CIPHER_CTX_cleanup()函数而引入了EVE_CIPHER_CTX_reset()函数所导致的：
> EVP_CIPHER_CTX was made opaque in OpenSSL 1.1.0. As a result, EVP_CIPHER_CTX_reset() appeared and EVP_CIPHER_CTX_cleanup() disappeared. EVP_CIPHER_CTX_init() remains as an alias for EVP_CIPHER_CTX_reset().

因此可以通过将EVP_CIPHER_CTX_cleanup()函数替换为EVP_CIPHER_CTX_reset() 函数来解决该问题，即可以：
  * 根据错误信息定位到文件 /home/feng/.local/lib/python3.6/site-packages/shadowsocks/crypto/openssl.py 。
  * 搜索 cleanup 并将其替换为 reset 。

* 配置代理 
* 设置开机启动gnome-session-properties，如下图：

 ![image2](https://github.com/GongQianyun2018/web-note/blob/master/img/day_2_VPS_2.png)
 
### 也可选择下载shadowssocks-qt5

### 启动shadowsocks服务
* 使用shadowsocks：

> sslocal -c /home/gqy/ss_config/ss.json -d start

> sslocal -c /home/gqy/ss_config/ss.json -d stop

> sslocal -c /home/gqy/ss_config/ss.json -d restart

* 使用shadowsocks-qt5:输入信息即可
### 设置系统代理为手动，如下图：

 ![image3](https://github.com/GongQianyun2018/web-note/blob/master/img/day_2_VPS_3.png)

### 下载chrome浏览器

使用SwitchySharp插件，配置完成后可将系统代理设置为自动，URL设为空


## 服务端安装

* 购买服务器：https://my.hosteons.com/index.php
* 下载putty，按照用户名（默认root）和密码登录（邮件发送）
* 安装ShadowsocksR：
> sudo apt install python3-pip

> sudo pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip

> sudo ssserver --version
* 创建配置文件
> ssserver --version

> sudo nano /etc/shadowsocks/config.json
```json
{
    "server":"::",
    "server_port":8388,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"XXX",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
}
```
* 测试shadowsocks是否工作
> ssserver -c /etc/shadowsocks/config.json

* 加速





