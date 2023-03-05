```
mkdir /root/warp && curl -Lo /root/warp/warp https://gitlab.com/ProjectWARP/warp-go/-/releases/v1.0.8/downloads/warp-go_1.0.8_linux_amd64.tar.gz && tar -xzf /root/warp/warp -C /root/warp && mv /root/warp/warp-go /root && chmod +x /root/warp-go && rm -r /root/warp && /root/warp-go --register && /root/warp-go -export-singbox wireguard.json
```

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
            }
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
                "reserved":[
                    10,
                    20,
                    30
                ]
            },
            "tag": "wireguard"
        }
    ]
```
