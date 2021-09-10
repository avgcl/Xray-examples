## Xray-core安装脚本 https://github.com/XTLS/Xray-install
推荐使用安装命令<pre>bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install</pre>
若使用VLESS-TCP-XTLS或VLESS-gRPC需执行命令，修改SSL证书文件<pre>chown -R nobody:nogroup /etc/ssl/private/</pre>

## Nginx 1.21及以上版本安装命令
Deiban 10
<pre>wget -qO /usr/share/keyrings/nginx-archive-keyring.key https://nginx.org/keys/nginx_signing.key && printf "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.key] https://nginx.org/packages/mainline/debian/ buster nginx" > /etc/apt/sources.list.d/sources.list && apt update -y && apt install -y nginx</pre>

Debian 11
<pre>wget -qO /usr/share/keyrings/nginx-archive-keyring.key https://nginx.org/keys/nginx_signing.key && printf "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.key] https://nginx.org/packages/mainline/debian/ bullseye nginx" > /etc/apt/sources.list.d/sources.list && apt update -y && apt install -y nginx</pre>
