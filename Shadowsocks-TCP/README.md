## Xray + Shadowsocks-TCP 手动安装教程

0.安装curl（可选）

```
apt update -y && apt install -y curl
```

1.安装Xray

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```

2.下载配置文件

```
curl -Lo /usr/local/etc/xray/config.json https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-TCP/config_server.json
```

3.下载路由规则文件加强版

```
curl -Lo /usr/local/share/xray/geosite.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat && curl -Lo /usr/local/share/xray/geoip.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geoip.dat
```

4.重启Xray

```
systemctl restart xray && systemctl status xray
```

5.自动更新路由规则文件加强版（可选）

```
printf "0 7 * * * /root/update_geodata.sh\n" > /root/update_geodata && crontab /root/update_geodata && printf "curl -sSLo /usr/local/share/xray/geosite.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat\ncurl -sSLo /usr/local/share/xray/geoip.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geoip.dat\nsleep 2\nsystemctl restart xray\n" > /root/update_geodata.sh && chmod +x /root/update_geodata.sh
```

## Windows系统客户端配置指南（使用自定义配置）

1.[打开链接1](https://github.com/2dust/v2rayN/releases)， 点击最新版本栏里的“▸ Assets”，找到名为v2rayN.zip的链接并下载。
[打开链接2](https://github.com/XTLS/Xray-core/releases) ，点击最新版本栏里的“▸ Assets”，找到名为Xray-windows-64.zip的链接并下载。
把2个压缩包解压，复制xray.exe到v2rayN文件夹里面，运行v2rayN.exe。

- 点击 设置 — 参数设置 — Core:DNS设置，1.1.1.1。v2rayN设置，勾选“更新Core时忽略Geo文件”，将“Core类型”改为“Xray_core”，确定。
- 点击 设置 — 路由设置，将“域名解析策略”改为“IPIfNonMatch”，取消勾选“启用路由高级功能”，将“域名匹配算法”改为“mph”，点击“基础功能”，点击“一键导入基础规则”，确定，确定。
- 右键点击屏幕右下角的v2rayN图标，点击“系统代理 — 自动配置系统代理”。

2.复制[客户端配置](https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-TCP/config_client.json)，新建一个文本文档，粘贴内容，找到`"address": "", //地址`，在`""`中间添加你VPS的IP，并保存。

- 点击 服务器 — 添加自定义配置服务器 — 确定，在弹出的对话框中，将右下角的Config改为All，选择刚才新建的文本文档，点击打开，确定。
- 点击服务器列表中刚才新增的服务器，按回车键载入配置。

3.点击“检查更新”
- 点击“Update GeoSite — 是否下载? — 是”。
- 点击“Update GeoIP — 是否下载? — 是”。

## Android系统客户端配置指南（使用自定义配置）

1.在电脑上下载[v2rayNG](https://github.com/2dust/v2rayNg/releases)，如v2rayNG_1.x.x_arm64-v8a.apk。

2.在电脑上下载路由规则文件加强版，[geoip.dat](https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geoip.dat)和[geosite.dat](https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat)。

3.在电脑上复制[客户端配置](https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-TCP/config_client.json)，新建一个文本文档，粘贴内容，找到`"address": "", //地址`，在`""`中间添加你VPS的IP，并保存，将文件扩展名改为*.json。

4.把v2rayNG_1.x.x_arm64-v8a.apk，geoip.dat，geosite.dat，客户端配置，用数据线复制到手机，在手机上安装v2rayNG。

5.进入v2rayNG，点击左上角≡ —— 设置，勾选“启用本地DNS”，“域名策略”改为“IPIfNonMatch”，“预定义规则”改为“绕过局域网及大陆地址而后代理”。

6.点击左上角`≡` — Geo 资源文件，点击右上角`+`，分别选择geoip.dat和geosite.dat。

7.点击右上角`+` — 自定义配置 — 从本地导入自定义配置，选择客户端配置。

8.点击右下角的灰色`V`字母图标。

## 注意事项

1.[为什么要禁止VPS访问CN域名和IP](https://github.com/XTLS/Xray-core/discussions/593#discussioncomment-845165)。

2.若使用其它客户端，需设置好CN域名和IP直连，否则将在VPS端被阻止。

3.密码建议使用20位或更强的。

4.为什么要使用自定义配置服务器？因为客户端配置需要手动添加["ivCheck"](https://github.com/v2fly/v2ray-core/pull/777#issuecomment-813963430)参数。
