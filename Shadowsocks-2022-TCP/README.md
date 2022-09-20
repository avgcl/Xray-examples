## Shadowsocks-2022 安装指南

1.安装Xray

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install --beta
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

- 使用SSH客户端软件连接你的VPS，输入`openssl rand -base64 16`生成密钥。
- 使用WinSCP连接你的VPS，进入/usr/local/etc/xray/目录，双击config.json文件，找到`"password": "",`，在`""`中间粘贴密钥，Ctrl+S保存。
- 使用SSH客户端软件连接你的VPS，输入`systemctl restart xray`重启Xray。
- 端口是50000，加密方式是2022-blake3-aes-128-gcm。

5.其它

- 因为有[重放保护](https://github.com/Shadowsocks-NET/shadowsocks-specs/blob/main/2022-1-shadowsocks-2022-edition.md#314-replay-protection)机制，客户端与服务器端的时间差要在[30秒](https://github.com/Shadowsocks-NET/shadowsocks-specs/blob/main/2022-1-shadowsocks-2022-edition.md#313-header)以内。
- 同步时间命令

```
apt install -y ntpdate && ntpdate pool.ntp.org
```

- 自动同步时间

```
crontab -e
```

```
0 0 * * * /usr/sbin/ntpdate pool.ntp.org > /dev/null 2>&1
```
