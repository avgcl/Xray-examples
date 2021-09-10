## 服务器安装：Xray Nginx 需要SSL证书

## 客户端v2rayN配置方式

![VLESS-TCP-XTLS](https://user-images.githubusercontent.com/88967758/132801053-cc8b3aee-5da8-45d5-9e23-115f3b766e52.jpg)

## 原理图：
v2rayN client <--- TCP with XTLS(VLESS) ---> Xray server <--- Unix domain socket(Fallback 回落) ---> Nginx server
