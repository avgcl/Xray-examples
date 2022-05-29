## Shadowsocks-2022安装指南

1.安装Xray

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install --version 1.5.6
```

2.下载配置文件

```
curl -Lo /usr/local/etc/xray/config.json https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-2022-TCP/config_server.json
```

3.下载路由规则文件加强版

```
curl -Lo /usr/local/share/xray/geosite.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat && curl -Lo /usr/local/share/xray/geoip.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geoip.dat
```

4.设置密钥
- 使用SSH客户端软件连接你的VPS，输入`openssl rand -base64 32`生成密钥。
- 使用WinSCP连接你的VPS，进入/usr/local/etc/xray/目录，双击config.json文件，找到`"password": "",`，在`""`中间粘贴密钥，Ctrl+S保存。
- 使用SSH客户端软件连接你的VPS，输入`systemctl restart xray`重启Xray。

5.注意
- 因为有[重放保护](https://github.com/Shadowsocks-NET/shadowsocks-specs/blob/ss-2022/2022-1-shadowsocks-2022-edition.md#314-replay-protection)机制，客户端与服务器端的时间差要在[30秒](https://github.com/Shadowsocks-NET/shadowsocks-specs/blob/ss-2022/2022-1-shadowsocks-2022-edition.md#313-header)以内
- 同步时间命令
```
apt install -y ntpdate && ntpdate cn.pool.ntp.org
```



## v2rayN配置指南（添加自定义配置服务器）

1.复制[客户端配置](https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-2022-TCP/config_client_v2rayN_custom.json)，新建一个文本文档，粘贴内容，找到`"address": "",`，在`""`中间输入你VPS的IP，找到`"password": ""`，在`""`中间粘贴密钥，Ctrl+S保存，将文件扩展名改为*.json。

2.下载[v2rayN](https://github.com/2dust/v2rayN/releases)，找到最新版本，在“▸ Assets”栏里，找到名为v2rayN.zip的链接并下载。下载[Xray-core](https://github.com/XTLS/Xray-core/releases) ，找到最新版本，在“▸ Assets”栏里，找到名为Xray-windows-64.zip的链接并下载。把2个压缩包解压，复制xray.exe到v2rayN文件夹里面，双击v2rayN.exe启动。

- 点击 **服务器 — 添加自定义配置服务器**。
- 点击 **浏览 — 确定** 在弹出的对话框中，选择刚才新建的文本文档，点击 **打开 — 确定**。
- 点击 **确定**。
- 点击服务器列表中刚才新增的服务器，**按回车键**设为活动服务器。
- 点击 **检查更新 — Update Geo files** 在信息栏确认有提示“下载 GeoFile: geoip 成功”，“下载 GeoFile: geoip 成功”，再次**按回车键**设为活动服务器，使其生效。
- 右键点击屏幕右下角的v2rayN图标，点击 **系统代理 — 自动配置系统代理**。



## v2rayNG配置指南（自定义配置）

1.复制[客户端配置](https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-2022-TCP/config_client_v2rayNG_custom.json)，新建一个文本文档，粘贴内容，找到`"address": "",`，在`""`中间输入你VPS的IP，找到`"password": ""`，在`""`中间粘贴密钥，Ctrl+S保存，将文件扩展名改为*.json。

2.下载[v2rayNG](https://github.com/2dust/v2rayNg/releases)，找到最新版本，通常是下载v2rayNG_1.X.X_arm64-v8a.apk的文件。把下载的apk文件，客户端配置文件，复制到手机，在手机上安装v2rayNG。

- 进入v2rayNG，点击右上角 + — 自定义配置 — 从本地导入自定义配置，选择客户端配置文件。
- 点击左上角 ≡  — 设置，勾选“启用本地DNS”。
- 点击右下角的灰色V字母图标，变成绿色后提示“启动服务成功”。
- 点击左上角 ≡ —  Geo 资源文件，点击右上角的云朵图标，下载完后提示“成功geosite.dat 成功geoip.dat”。
- 推荐使用分应用代理，根据你的需要，选择被代理的App，重新关开一次服务，使其生效。
