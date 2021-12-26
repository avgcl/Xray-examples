## Xray + Shadowsocks-TCP 手动安装教程

准备软件

- [Xshell 7 免费版](https://www.netsarang.com/en/free-for-home-school/)

重装系统（请去你的VPS网站上操作，建议重装系统为Deian10或11）

- Debian 10
- Debian 11
- Ubuntu 18.04
- Ubuntu 20.04

开始安装

- 使用Xshell 7连接你的VPS
- 使用root用户登陆
- 请从步骤0开始按顺序操作

0.安装curl
```
apt update -y && apt install -y curl
```

1.安装[Xray](https://github.com/XTLS/Xray-core/releases)
```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install --version 1.5.2
```

2.下载配置文件
```
curl -Lo /usr/local/etc/xray/config.json https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-TCP
/config_server.json
```

3.下载[路由规则文件加强版](https://github.com/Loyalsoldier/v2ray-rules-dat)
```
curl -Lo /usr/local/share/xray/geosite.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat && curl -Lo /usr/local/share/xray/geoip.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geoip.dat
```

4.重启Xray
```
systemctl restart xray && systemctl status xray
```

## Windows系统客户端配置指南
1.下载和设置v2rayN

[打开链接](https://github.com/2dust/v2rayN/releases) 点击最新版本栏里的“▸ Assets `4`”，找到名为`v2rayN-Core.zip`的链接并下载。把压缩包解压，找到`v2rayN-Core`文件夹里的`v2rayN.exe`并双击运行。

- 点击 设置 — 参数设置 — v2rayN设置，勾选“更新Core时忽略Geo文件”，将“Core类型”改为“Xray_core”，确定。
- 点击 设置 — 路由设置，将“域名解析策略”改为“IPIfNonMatch”，取消勾选“启用路由高级功能”，将“域名匹配算法”改为“mph”，点击“基础功能”，点击“一键导入基础规则”，确定，确定。
- 右键点击屏幕右下角的v2rayN图标，点击“系统代理 — 自动配置系统代理”。

2.在v2rayN中添加服务器

- 复制[客户端配置](https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-TCP/config_client.json)，新建一个文本文档，粘贴其内容，找到`"address": "", //地址`，在`""`中间添加你VPS的IP，并保存。
- 点击 服务器 — 添加自定义配置服务器 — 确定，在弹出的对话框中，将右下角的Config (.json)改为All (.*)，选择刚才新建的文本文档，点击打开，确定。
- 点击服务器列表中刚才新增的服务器，按回车键载入配置。

3.点击“检查更新”
- 点击““Xray-Core — 是否下载? — 是”。
- 点击“Update GeoSite — 是否下载? — 是”。
- 点击“Update GeoIP — 是否下载? — 是”。

## Android系统客户端配置指南

1.自己想办法在手机上安装[v2rayNG](https://github.com/2dust/v2rayNg/releases)，通常是下载`v2rayNG_1.x.x_arm64-v8a.apk`版本

2.用手机浏览器打开[客户端配置](https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-TCP/config_client.json)，全选后并复制

3.进入v2rayNG，点击右上角`+` — 自定义配置 — 从剪贴板导入自定义配置

4.找到刚才新增的服务器，点击最右边的钢笔图标

5.找到`"address": "", //地址`，在`""`中间添加你VPS的IP，点击右上角的`✓`

6.用手机浏览器打开[路由规则文件加强版](https://github.com/Loyalsoldier/v2ray-rules-dat)，下载geoip.dat和geosite.dat文件

7.进入v2flyNG，点击左上角`≡` — Geo 资源文件，点击右上角`+`，分别选择刚才下载的geoip.dat和geosite.dat文件

8.回到v2flyNG主界面，点击右下角的v2flyNG图标

## 注意事项

1.[为什么要禁止VPS访问CN域名和IP](https://github.com/XTLS/Xray-core/discussions/593#discussioncomment-845165)

2.请正确设置CN域名和IP直连，若在客户端未正确设置CN域名和IP直连，将在VPS端被阻止

3.密码建议使用[20位或更强的](https://1password.com/password-generator/)

4.为什么要使用自定义配置服务器？因为客户端配置需要手动添加["ivCheck"](https://github.com/v2fly/v2ray-core/pull/777#issuecomment-813963430)参数
