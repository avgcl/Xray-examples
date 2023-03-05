**使用waro-go，注册warp，导出wireguard配置**
```
mkdir /root/warp && curl -Lo /root/warp/warp https://gitlab.com/ProjectWARP/warp-go/-/releases/v1.0.8/downloads/warp-go_1.0.8_linux_amd64.tar.gz && tar -xzf /root/warp/warp -C /root/warp && mv /root/warp/warp-go /root && chmod +x /root/warp-go && rm -r /root/warp && /root/warp-go --register && /root/warp-go -export-singbox wireguard.json
```

打开 **/root/wireguard.json**，复制"private_key"的值，粘贴到"secretKey": "",处，复制"reserved"的值，粘贴到"reserved":[,,]处

打开 **/usr/local/etc/xray/config.json**，按需增加"routing"和"outbounds"内容后（注意检查json语法），`systemctl restart xray`生效，可访问ip.sb查看是否为cloudflare的IP

```
    "routing": {
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "type": "field",
                "domain": [
                    "ip.sb",
                    "geosite:openai"
                ],
                "outboundTag": "wireguard"
            },
            {
                "type": "field",
                "ip": [
                    "geoip:cn"
                ],
                "outboundTag": "wireguard"
            }
        ]
    }
```

```
    "outbounds": [
        {
            "protocol": "wireguard",
            "settings": {
                "secretKey": "",
                "address": [
                    "172.16.0.2/32"
                ],
                "peers": [
                    {
                        "publicKey": "bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
                        "allowedIPs": [
                            "0.0.0.0/0"
                        ],
                        "endpoint": "engage.cloudflareclient.com:2408"
                    }
                ],
                "mtu": 1280,
                "reserved":[,,]
            },
            "tag": "wireguard"
        }
    ]
```
