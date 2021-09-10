## 服务器安装：Xray Nginx 需要SSL证书

## 客户端v2rayN配置方式

![VLESS-gRPC](https://user-images.githubusercontent.com/88967758/132800221-1e67083c-6d38-4f00-8f24-38ae688f3d09.jpg)

## 原理图：
v2rayN client <--- gRPC with TLS(VLESS) ---> Nginx server <--- Unix domain socket(反向代理) ---> Xray server
