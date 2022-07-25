## v2rayN配置方式

![VLESS-TCP-TLS](https://user-images.githubusercontent.com/88967758/180816959-69ea476e-a3b5-466f-87d0-25842a0f34ac.jpg)

## DNS查询流程说明

**客户端**

**被查询的域名是包含在geosite的CN类别**
- 路由模块 → `命中CN域名走直连的规则`
- 出站模块 → 直连出站，使用系统默认DNS查询，建立连接，开始传输数据
---

**被查询的域名不是包含在geosite的CN类别**
- 路由模块 → `未命中任何域名规则`
- DNS模块 → 使用1.1.1.1的DNS查询

- 路由模块 → 命中1.1.1.1走代理的规则
- 出站模块 → 代理出站，与服务器建立通讯，由服务器访问1.1.1.1进行DNS查询，收到查询域名的IP
---

- 路由模块 → `IP是包含在geoip的CN类别`
- 出站模块 → 直连出站，使用系统默认DNS查询，建立连接，开始传输数据
---

- 路由模块 → `IP不是包含在geoip的CN类别`
- 出站模块 → 默认使用第1个出站配置，发送DNS查询请求到服务器，等待服务器处理
---

**服务器端**

**收到客户端的DNS查询请求**
- DNS模块 → 使用1.1.1.1的DNS查询，返回域名的IP
---

- 路由模块 → `IP是包含在geoip的CN类别`
- 出站模块 → 阻止出站
---

- 路由模块 → `IP不是包含在geoip的CN类别`
- 出站模块 → 直连出站，使用1.1.1.1的DNS查询，命中DNS缓存，建立连接，通知客户端，连接已准备就绪
---

**客户端**
- 出站模块 → 收到服务器通知，连接已准备就绪，开始传输数据
---

- 推荐文章 [漫谈各种黑科技式 DNS 技术在代理环境中的应用](https://tachyondevel.medium.com/%E6%BC%AB%E8%B0%88%E5%90%84%E7%A7%8D%E9%BB%91%E7%A7%91%E6%8A%80%E5%BC%8F-dns-%E6%8A%80%E6%9C%AF%E5%9C%A8%E4%BB%A3%E7%90%86%E7%8E%AF%E5%A2%83%E4%B8%AD%E7%9A%84%E5%BA%94%E7%94%A8-62c50e58cbd0) 
- 推荐文章 [浅谈在代理环境中的 DNS 解析行为](https://blog.skk.moe/post/what-happend-to-dns-in-proxy/)
- 推荐文章 [路由 (routing) 功能简析](https://xtls.github.io/Xray-docs-next/document/level-1/routing-lv1-part1.html)
- 推荐文章 [DNS 域名解析](https://www.v2fly.org/config/dns.html)
- 推荐文章 [DNS 服务](https://guide.v2fly.org/basics/dns.html)
- 推荐文章 [为什么要禁止VPS访问CN域名和IP](https://github.com/XTLS/Xray-core/discussions/593#discussioncomment-845165)
---
