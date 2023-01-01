## [XTLS Vision](https://github.com/XTLS/Xray-core/discussions/1295) 安装指南

1. 安装程序

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install --beta
```

2. 下载配置

```
curl -Lo /usr/local/etc/xray/config.json https://raw.githubusercontent.com/chika0801/Xray-examples/main/VLESS-TCP-XTLS-Vision/config_server.json
```

3. 上传证书和私钥

- 将证书文件改名为`fullchain.cer`，将私钥文件改名为`private.key`，使用WinSCP登录你的VPS，将它们上传到`/etc/ssl/private`目录，执行下面的命令。

```
chown -R nobody:nogroup /etc/ssl/private
```

- [用acme申请 SSL 证书](https://github.com/chika0801/Xray-install#1%E7%94%A8acme%E7%94%B3%E8%AF%B7-ssl-%E8%AF%81%E4%B9%A6)

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

## v2rayN 5.x 配置指南

`服务器` ——> `添加[VLESS服务器]`

![1](https://user-images.githubusercontent.com/88967758/200235011-84299a14-7a5c-409b-a7c6-0ad42ba2c672.jpg)

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

## ShadowSocksR Plus+ 配置指南

<details><summary>点击查看</summary><br>

| 选项 | 值 |
| :--- | :--- |
| 服务器节点类型 | V2Ray/Xray |
| 别名（可选） |  |
| V2Ray/XRay 协议 | VLESS |
| 服务器地址 | VPS的IP |
| 端口 | 16387 |
| Vmess/VLESS ID (UUID) | chika |
| VLESS 加密 | none |
| 传输协议 | TCP |
| 伪装类型 | 无 |
| TLS | 勾上 |
| 流控（Flow） | xtls-rprx-vision |
| 指纹伪造 | chrome |
| TLS 主机名 | 证书中包含的域名 |
| TLS ALPN | 留空 |
| 允许不安全连接 | 不勾 |
| Mux | 不勾 |
| 自签证书 | 不勾 |
| 启用自动切换 | 不勾 |
| 本地端口 | 1234 |

</details>

## PassWall 配置指南

<details><summary>点击查看</summary><br>

| 选项 | 值 |
| :--- | :--- |
| 节点备注 |  |
| 类型 | Xray |
| 协议名称 | VLESS |
| 地址 | VPS的IP |
| 端口 | 16387 |
| 加密 | none |
| ID | chika |
| TLS | 勾上 |
| XTLS | 不勾 |
| flow | xtls-rprx-vision |
| alpn | 默认 |
| 域名 | 证书中包含的域名 |
| 允许不安全连接 | 不勾 |
| 指纹伪造 | chrome |
| 传输方式 | TCP |
| 伪装类型 | none |
| Mux | 不勾 |

</details>

## VLESS 流控与客户端选项速查表

<details><summary>点击查看</summary><br>

服务器配置："flow": "**xtls-rprx-vision**" + "security": "**tls**" + "**tls**Settings"
| 客户端选项 | uTLS 支持 | 说明 |
| :--- | :--- | :--- |
| 流控(flow): **xtls-rprx-vision**  + 传输层安全(tls): **tls** | 是 |  |
| 流控(flow): **留空** + 传输层安全(tls): **tls** |  | Vision 流控拒绝安全性较低的普通 TLS 连接 |

服务器配置："flow": "**xtls-rprx-vision,none**" + "security": "**tls**" + "**tls**Settings"
| 客户端选项 | uTLS 支持 | 说明 |
| :--- | :--- | :--- |
| 流控(flow): **xtls-rprx-vision**  + 传输层安全(tls): **tls** | 是 |  |
| 流控(flow): **留空** + 传输层安全(tls): **tls** | 是 | 仍然需要在同端口开放 VLESS-TCP-TLS |

服务器配置："flow": "**xtls-rprx-direct**" + "security": "**xtls**" + "**xtls**Settings"
| 客户端选项 | uTLS 支持 |
| :--- | :--- |
| 流控(flow): **xtls-rprx-direct** + 传输层安全(tls): **xtls** | 否 |
| 流控(flow): **xtls-rprx-splice** + 传输层安全(tls): **xtls** | 否 |
| 流控(flow) **留空** + 传输层安全(tls) **tls** | 是 |

</details>
