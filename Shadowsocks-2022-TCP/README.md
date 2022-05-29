## Xray + Shadowsocks-2022-TCP 手动安装教程

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



## v2rayN配置指南（添加自定义配置服务器）

1.[下载v2rayN](https://github.com/2dust/v2rayN/releases)，找到最新版本，在“▸ Assets”栏里，找到名为v2rayN.zip的链接并下载。[下载Xray-core](https://github.com/XTLS/Xray-core/releases) ，找到最新版本，在“▸ Assets”栏里，找到名为Xray-windows-64.zip的链接并下载。把2个压缩包解压，复制xray.exe到v2rayN文件夹里面，运行v2rayN.exe。

2.复制[客户端配置](https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-2022-TCP/config_client.json)，新建一个文本文档，粘贴内容，找到`"address": "",`，在`""`中间输入你VPS的IP，找到`"password": ""`，在`""`中间粘贴密钥，Ctrl+S保存。

- 点击 **服务器 — 添加自定义配置服务器**。
- 点击 **浏览 — 确定** 在弹出的对话框中，将右下角的Config改为All，选择刚才新建的文本文档，点击**打开 — 确定**。
- 点击 **确定**。
- 点击服务器列表中刚才新增的服务器，**按回车键载入配置**。
- 右键点击屏幕右下角的v2rayN图标，点击 **系统代理 — 自动配置系统代理**。

3.点击 **检查更新 — Update Geo files** 在信息栏确认有提示“下载 GeoFile: geoip 成功”，“下载 GeoFile: geoip 成功”，再次点击服务器列表中刚才新增的服务器，**按回车键重新载入配置，确认生效**。
