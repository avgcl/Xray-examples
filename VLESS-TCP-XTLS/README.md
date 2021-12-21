## DNS查询流程说明

### 客户端配置

#### 被查询的域名是包含在geosite的CN类别
- 路由模块 → 命中CN域名走直连的规则
- 出站模块 → 直连出站，请求内容是域名使用DNS模块查询
- DNS模块 → 使用阿里的DNS查询，返回域名的IP（DNS查询结束）
- 出站模块 → 直连出站，请求内容是IP，使用本机网络出站，建立连接，开始传输数据
---
#### 被查询的域名不是包含在geosite的CN类别
- 路由模块 → 未命中任何路由规则
- DNS模块 → 使用AdGuard的DNS查询
- 路由模块 → 命中dns.adguard.com走代理的规则
- 出站模块 → 代理出站，与服务器建立通讯，由服务器进行DNS查询，收到查询域名的IP（DNS查询结束）
---
- 路由模块 → IP是包含在geoip的CN类别
- 出站模块 → 直连出站，请求内容是域名使用DNS模块查询
- DNS模块 → 使用AdGuard的DNS查询，命中DNS缓存，返回缓存的IP
- 出站模块 → 直连出站，请求内容是IP，使用本机网络出站，建立连接，开始传输数据
---
- 路由模块 → IP不是包含在geoip的CN类别
- 出站模块 → 默认使用第1个出站配置，发送DNS查询请求到服务器 → 等待服务器处理 → 收到服务器通知，连接已准备就绪，开始传输数据
---
### 服务器端配置
- 收到客户端的DNS查询请求

#### 被查询的域名是包含在geosite的CN类别
- 路由模块 → 命中CN域名走阻止的规则
- 出站模块 → 阻止出站
---
#### 被查询的域名不是包含在geosite的CN类别
- 路由模块 → 未命中任何路由规则
- DNS模块 → 使用AdGuard的DNS查询，返回域名的IP（DNS查询结束）
---
- 路由模块 → IP是包含在geoip的CN类别
- 出站模块 → 阻止出站
---
- 路由模块 → IP不是包含在geoip的CN类别
- 出站模块 → 直连出站，请求内容是域名使用DNS模块查询
- DNS模块 → 使用AdGuard的DNS查询，命中DNS缓存，返回缓存的IP
- 出站模块 → 直连出站，请求内容是IP，使用本机网络出站，建立连接，通知客户端，连接已准备就绪
---
- 推荐使用 [路由规则文件加强版](https://github.com/Loyalsoldier/v2ray-rules-dat)
- 推荐文章 [漫谈各种黑科技式 DNS 技术在代理环境中的应用](https://tachyondevel.medium.com) 
- 推荐文章 [路由 (routing) 功能简析](https://xtls.github.io/Xray-docs-next/document/level-1/routing-lv1-part1.html)
- 推荐文档 (https://www.v2fly.org/config/dns.html)
- 推荐文档 (https://guide.v2fly.org/basics/dns.html)
- 推荐文章 [为什么要禁止VPS访问CN域名和IP](https://github.com/XTLS/Xray-core/discussions/593#discussioncomment-845165)
---
## 客户端v2rayN配置方式

![VLESS-TCP-XTLS](https://user-images.githubusercontent.com/88967758/132801053-cc8b3aee-5da8-45d5-9e23-115f3b766e52.jpg)
