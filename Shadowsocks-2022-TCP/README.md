## [Shadowsocks-2022](https://github.com/Shadowsocks-NET/shadowsocks-specs) 安装指南

1. 安装程序

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install --beta
```

2. 下载配置

```
curl -Lo /usr/local/etc/xray/config.json https://raw.githubusercontent.com/chika0801/Xray-examples/main/Shadowsocks-2022-TCP/config_server.json
```

3. 设置密钥

- 使用SSH软件登录你的VPS，输入`openssl rand -base64 16`生成密钥。
- 使用WinSCP登录你的VPS，进入`/usr/local/etc/xray/`目录，双击`config.json`文件，找到`"password": "",`，在`""`中间粘贴密钥，Ctrl+S保存。
- 使用SSH软件登录你的VPS，输入`systemctl restart xray`重启Xray。
- 端口是`50000`，加密方式是`2022-blake3-aes-128-gcm`。

4. 其它

- 因为有[重放保护](https://github.com/Shadowsocks-NET/shadowsocks-specs/blob/main/2022-1-shadowsocks-2022-edition.md#314-replay-protection)机制，客户端与服务器的时间差要在[30秒](https://github.com/Shadowsocks-NET/shadowsocks-specs/blob/main/2022-1-shadowsocks-2022-edition.md#313-header)以内。
- 同步时间命令

```
apt install -y systemd-timesyncd && systemctl enable --now systemd-timesyncd
```

或

```
apt install -y ntpdate && ntpdate pool.ntp.org
```

```
crontab -e
```

```
0 0 * * * /usr/sbin/ntpdate pool.ntp.org
```
