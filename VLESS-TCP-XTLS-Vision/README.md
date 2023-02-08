## [Xray](https://github.com/XTLS/Xray-core/releases) [XTLS Vision](https://github.com/XTLS/Xray-core/discussions/1295) 不带回落 (fallbacks) 安装指南

1. 安装程序

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install --beta
```

2. 下载配置

```
curl -Lo /usr/local/etc/xray/config.json https://raw.githubusercontent.com/chika0801/Xray-examples/main/VLESS-TCP-XTLS-Vision/config_server.json
```

3. 上传证书和私钥

- 将证书文件改名为`fullchain.cer`，将私钥文件改名为`private.key`，将它们上传到`/etc/ssl/private`目录，执行下面的命令。

```
chown -R nobody:nogroup /etc/ssl/private
```

4. 启动程序

```
systemctl restart xray
```

```
systemctl status xray
```

| 项目 | |
| :--- | :--- |
| 程序 | /usr/local/bin/xray |
| 配置 | /usr/local/etc/xray/config.json |
| 检查 | xray -test -config /usr/local/etc/xray/config.json |
| 路由规则文件 | /usr/local/share/xray/ |
| 查看日志 | journalctl -u xray --output cat -e |
| 实时日志 | journalctl -u xray --output cat -f |

## v2rayN 6.x 配置指南

<details><summary>点击查看</summary><br>

`服务器` ——> `添加[VLESS服务器]`

| 选项 | 值 |
| :--- | :--- |
| 地址(address) | VPS的IP |
| 端口(prot) | 16387 |
| 用户ID(id) | chika |
| 流控(flow) | xtls-rprx-vision |
| 传输协议(network) | tcp |
| TLS | tls |
| SNI | 证书中包含的域名 |
| uTLS | chrome |

</details>

小技巧：只要证书在有效期内，证书中包含的域名不用解析到VPS的IP。一份证书，在多个VPS上使用。

## v2rayNG 配置指南

<details><summary>点击查看</summary><br>

| 选项 | 值 |
| :--- | :--- |
| 地址(address) | VPS的IP |
| 端口(prot) | 16387 |
| 用户ID(id) | chika |
| 流控(flow) | xtls-rprx-vision |
| 传输协议(network) | tcp |
| 传输层安全(tls) | tls |
| SNI | 证书中包含的域名 |
| uTLS | chrome |

</details>
