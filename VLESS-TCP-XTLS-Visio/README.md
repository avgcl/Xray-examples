## v2rayN配置指南

下载客户端配置[config_client.json](https://raw.githubusercontent.com/chika0801/Xray-examples/main/VLESS-TCP-XTLS-Visio/config_client.json)

找到在["address": ""](https://github.com/chika0801/Xray-examples/blob/94d9a0965fb1ef9882be0820feb8a7d89ee8bc59/VLESS-TCP-XTLS-Visio/config_client.json#L61)，在`""`中间输入VPS的IP

找到在[""serverName": ""](https://github.com/chika0801/Xray-examples/blob/94d9a0965fb1ef9882be0820feb8a7d89ee8bc59/VLESS-TCP-XTLS-Visio/config_client.json#L77)，在`""`中间输入证书中包含的域名



小技巧：只要证书在有效期内，证书中包含的域名不用解析到VPS的IP。一份证书，在多个VPS上使用。

![1](https://user-images.githubusercontent.com/88967758/195763557-f9706952-f2fc-466f-9787-bf00d138562d.jpg)
