## 客户端v2rayN配置方式

![VLESS-gRPC](https://user-images.githubusercontent.com/88967758/132800221-1e67083c-6d38-4f00-8f24-38ae688f3d09.jpg)

预防断流的参数，不确定是否有效

```
printf "net.ipv4.tcp_fin_timeout = 30\nnet.ipv4.tcp_slow_start_after_idle = 0\nnet.ipv4.tcp_tw_reuse = 1\n" > /etc/sysctl.d/grpc.conf && sysctl -p

```
