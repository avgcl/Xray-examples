### v2rayN - V6.17及以上版本 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 地址 | chika.example.com |
| 端口 | 443 |
| 用户ID | chika |
| 流控 | xtls-rprx-vision |
| 传输层安全 | tls |
| Fingerprint | chrome |

![1](https://user-images.githubusercontent.com/88967758/224359333-39fe1582-e98f-4f10-951e-3d54499bbe6d.png)

</details>

### v2rayNG 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 地址(address) | chika.example.com |
| 端口(prot) | 443 |
| 用户ID(id) | chika |
| 流控(flow) | xtls-rprx-vision |
| 传输协议(network) | tcp |
| 传输层安全(tls) | tls |
| SNI | 留空 |
| uTLS | chrome |

</details>

### NekoBox 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 服务器 | chika.example.com |
| 服务器端口 | 443 |
| 用户ID | chika |
| Flow (VLESS Sub-protocol) | xtls-rprx-vision |
| 包编码 | xudp |
| 传输协议 | tcp |
| 传输层加密 | tls |
| 服务器名称指标 | 留空 |
| 应用层协议协商 | 留空 |
| 证书（链） | 留空 |
| 允许不安全的连接 | 不选 |
| uTLS fingerprint | chrome |
| Reality Public Key | 留空 |
| Reality ShortId | 留空 |

</details>

### Shadowrocket 配置示例

<details><summary>点击查看</summary><br>

:exclamation:Shadowrocket 2.2.25 的 Vision 对应的服务端是 Xray-core v1.7.5，与 [v1.8.0 不完全兼容](https://github.com/XTLS/Xray-core/issues/1755#issuecomment-1462355442)，建议：

- **若要用小火箭的 Vision，服务端及其它客户端暂时使用 v1.7.5，勿升级到 v1.8.0**

```
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install --version 1.7.5
```

| 选项 | 值 |
| :--- | :--- |
| 类型 | VLESS |
| 地址 | chika.example.com |
| 端口 | 443 |
| UUID | chika |
| TLS | 选上 |
| XTLS | xtls-rprx-vision |
| 允许不安全 | 不选 |
| SNI | 留空 |
| ALPN | 留空 |
| 传输方式 | none |
| 多路复用 | 不选 |
| TCP 快速打开 | 不选 |
| UDP 转发 | 选上 |
| 代理通过 | 留空 |

</details>

### ShadowSocksR Plus+ 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 服务器节点类型 | V2Ray/Xray |
| V2Ray/XRay 协议 | VLESS |
| 服务器地址 | chika.example.com |
| 端口 | 443 |
| Vmess/VLESS ID (UUID) | chika |
| VLESS 加密 | none |
| 传输协议 | TCP |
| 伪装类型 | 无 |
| TLS | 勾上 |
| 流控（Flow） | xtls-rprx-vision |
| 指纹伪造 | chrome |
| TLS 主机名 | 留空 |
| TLS ALPN | 留空 |
| 允许不安全连接 | 不勾 |
| Mux | 不勾 |
| 自签证书 | 不勾 |
| 启用自动切换 | 不勾 |
| 本地端口 | 1234 |

</details>

### Pass Wall 配置示例

<details><summary>点击查看</summary><br>

| 名称 | 值 |
| :--- | :--- |
| 类型 | Xray |
| 传输协议 | VLESS |
| 地址（支持域名） | chika.example.com |
| 端口 | 443 |
| 加密方式 | none |
| ID | chika |
| TLS | 勾上 |
| flow | xtls-rprx-vision |
| REALITY | 不勾 |
| alpn | 默认 |
| 域名 | 留空 |
| 允许不安全连接 | 不勾 |
| 指纹伪造 | chrome |
| 传输协议 | TCP |
| 伪装类型 | none |

</details>

### Clash Meta Kernel 配置示例

<details><summary>点击查看</summary><br>

```
  - name: Vision
    type: vless
    server: chika.example.com
    port: 443
    uuid: chika
    network: tcp
    tls: true
    udp: true
    flow: xtls-rprx-vision
    servername: 
    client-fingerprint: chrome
```

</details>
