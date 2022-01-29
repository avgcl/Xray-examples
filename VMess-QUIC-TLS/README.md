## 客户端v2rayN配置方式

![QUIC](https://user-images.githubusercontent.com/88967758/151653241-2c31347f-ebdd-4c34-a72f-0fb62788cfa3.jpg)

## Xray + VMess-QUIC-TLS 手动安装教程

0.将公钥文件改名为fullchain.pem，将私钥文件改名为privkey.pem，使用WinSCP连接你的VPS，将它们上传到/etc/ssl/private/目录，执行`cchown -R nobody:nogroup /etc/ssl/private/`命令

1.安装[Xray](https://github.com/XTLS/Xray-core/releases)

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install --version 1.5.3
```

2.下载[配置文件](https://raw.githubusercontent.com/chika0801/Xray-examples/main/VMess-QUIC-TLS/config_server.json)

```
curl -Lo /usr/local/etc/xray/config.json https://raw.githubusercontent.com/chika0801/Xray-examples/main/VMess-QUIC-TLS/config_server.json
```

3.下载[路由规则文件加强版](https://github.com/Loyalsoldier/v2ray-rules-dat)

```
curl -Lo /usr/local/share/xray/geosite.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat && curl -Lo /usr/local/share/xray/geoip.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geoip.dat
```

4.重启Xray

```
systemctl restart xray && systemctl status xray
```

5.自动更新路由规则文件加强版（可选）

```
printf "* 7 * * * /root/update_geodata.sh\n" > /root/update_geodata && crontab /root/update_geodata && printf "curl -sSLo /usr/local/share/xray/geosite.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geosite.dat\ncurl -sSLo /usr/local/share/xray/geoip.dat https://github.com/Loyalsoldier/v2ray-rules-dat/releases/latest/download/geoip.dat\nsleep 2\nsystemctl restart xray\n" > /root/update_geodata.sh && chmod +x /root/update_geodata.sh
```

