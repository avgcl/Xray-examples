## [XTLS Vision](https://github.com/XTLS/Xray-core/discussions/1295)安装指南

1.安装程序

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install --version 1.6.2
```

2.下载配置

```
curl -Lo /usr/local/etc/xray/config.json https://raw.githubusercontent.com/chika0801/Xray-examples/main/VLESS-TCP-XTLS-Visio/config_server.json
```

3.上传证书和私钥

将证书文件改名为`fullchain.cer`，将私钥文件改名为`private.key`，使用WinSCP登录你的VPS，将它们上传到`/etc/ssl/private/`目录。

[用acme申请 SSL 证书](https://github.com/chika0801/Xray-install#1%E7%94%A8acme%E7%94%B3%E8%AF%B7-ssl-%E8%AF%81%E4%B9%A6)

[什么是 SSL 证书](https://www.kaspersky.com.cn/resource-center/definitions/what-is-a-ssl-certificate)

4.启动程序

```
systemctl start xray
```

```
systemctl status xray
```

- 配置 `/usr/local/etc/xray/config.json`
- 证书 `/etc/ssl/private/fullchain.cer`
- 私钥 `/etc/ssl/private/private.key`
- 查看日志 `journalctl -u xray --output cat -e`
- 实时日志 `journalctl -u xray --output cat -f`

## v2rayN配置指南

下载客户端配置[config_client.json](https://raw.githubusercontent.com/chika0801/Xray-examples/main/VLESS-TCP-XTLS-Visio/config_client.json)

找到在`"address": ""`，在`""`中间输入VPS的IP

找到在`"serverName": ""`，在`""`中间输入证书中包含的域名



小技巧：只要证书在有效期内，证书中包含的域名不用解析到VPS的IP。一份证书，在多个VPS上使用。

![1](https://user-images.githubusercontent.com/88967758/195763557-f9706952-f2fc-466f-9787-bf00d138562d.jpg)
