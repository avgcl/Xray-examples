## Xray手动安装教程（VMess-gRPC版）

1.安装curl

<pre>apt update -y && apt install -y curl</pre>

2.安装Xray

<pre>bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install</pre>

3.下载Xray的配置文件

<pre>wget -qO /usr/local/etc/xray/config.json https://raw.githubusercontent.com/chika0801/Xray-examples/main/VMess-gRPC/config_server.json</pre>

4.重启Xray

<pre>systemctl restart xray && systemctl status xray</pre>

## 客户端v2rayN配置方式

服务器 — 添加[VMess]服务器

![1](https://user-images.githubusercontent.com/88967758/133038521-a5ff5c72-4743-4193-aa7b-b805a1f730aa.jpg)

## 客户端v2rayNG配置方式

右上角“+” — 手动输入[VMess]

![Screenshot_20210913-150332](https://user-images.githubusercontent.com/88967758/133039075-cf96a28b-1729-4d98-9f66-2ee97beea469.jpg)

## 原理图：
v2rayN client <--- gRPC(VMess) ---> Xray server
