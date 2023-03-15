**推荐使用：** 

:rocket:VLESS-XTLS-Vision

:rocket:VLESS-XTLS-uTLS-REALITY

| 名称 | 基于TCP协议 | 自己准备证书 | TLSinTLS特征 | 通过CDN |
| :--- | :---: | :---: | :---: | :---: |
| Vision |  :o: | :o: | :x: | :x: |
| Vision-REALITY | :o: | :x: | :x: | :x: |
| gRPC-REALITY | :o: | :x: | :o: | :x: |
| H2-REALITY |  :o: | :x: | :o: | :x: |

:+1:**XTLS Vision [简介](https://github.com/XTLS/Xray-core/discussions/1295) [安装指南](https://github.com/chika0801/Xray-install) [客户端配置示例](https://github.com/chika0801/Xray-install/blob/main/README.md#%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)**


:+1:**REALITY [设计哲学](https://github.com/XTLS/Xray-core/issues/1689#issuecomment-1439447009) [配置模板说明](https://github.com/XTLS/REALITY#readme) [安装指南](https://github.com/chika0801/Xray-install/blob/main/REALITY.md)**

~~REALITY需要使用[最新测试版本](https://github.com/XTLS/Xray-core/actions/workflows/release.yml)的Xray-core文件~~

或者[自己编译](https://github.com/chika0801/Xray-install/blob/main/compile_Xray-core.md)使用最新源码的Xray-core文件

**希望你为[REALITY](https://github.com/XTLS/REALITY)仓库点一个:star:**

~~[我们定个新的小目标：REALITY stars 到 1024 当天出文章](https://github.com/XTLS/Xray-core/issues/1679#issuecomment-1436520973)~~

:eyes:**Xray-core need you help!**

**:star:Star [this project](https://github.com/XTLS/REALITY) to make the next future a REALITY.**

**使用提醒：** 

<details><summary>点击查看</summary><br>

:exclamation::exclamation::exclamation:

相对于 XTLS Vision 的使用基数，目前几乎没有收到 **配置正确** 的 Vision 被封端口的报告，**配置正确** 指的是：

1. 服务端使用合理的端口，禁回国流量
2. 只配置 XTLS Vision，不兼容普通 TLS 代理
3. 回落到网页，不回落/分流到其它代理协议
4. 客户端启用 uTLS（fingerprint） [#1.1](https://github.com/XTLS/Xray-core/issues/1544#issuecomment-1399194727)

---

首先，如果你特别不想被封，**请先选择一个干净的 IP**，并按照 **配置正确** 去搭建、使用 XTLS Vision。

**但是，即使你这样做了，也无法保证 100% 不被封**。自去年底始，很多人的未知流量秒封 IP，TLS in TLS 流量隔天封端口。XTLS Vision 不是未知流量，且完整处理了 TLS in TLS 特征，目前看来效果显著。**但这并不意味着，用 XTLS Vision 可以 100% 不被封，认识到这一点是非常、非常重要的，不要自己偶然被封就大惊小怪**。

**因为除了协议本身，还有很多角度能封你**。以 IP 为例，你无法保证 IP 真的干净，无法避免被邻居波及，无法避免整个 IP 段被重点拉清单。也有可能某些地区的 GFW 有独特的标准，比如某个 IP 只有寥寥数人访问连却能跑那么多流量，封。**如果你的 XTLS Vision 被封了，但没有出现去年底 TLS 那样的大规模被封报告，我真心建议你换端口、换 IP、换服务商依次试一遍**。 [#1.2](https://github.com/XTLS/Xray-core/issues/1544#issuecomment-1402118517)

---

如果你之前用了其它协议导致 TCP/443 端口被封，**Vision 并没有“解封已经被封的端口”的能力**，换个 IP 或端口 [#1.3](https://github.com/XTLS/Xray-core/issues/1670#issuecomment-1436240888)

:exclamation::exclamation::exclamation:

看来好多人还不知道代码里 Vision 只支持纯净入站或另一个 Vision 入站，~~当然要改也是不难的~~ [#2.1](https://github.com/XTLS/Xray-core/issues/1612#issuecomment-1418829266)

---
  
其实我早就看到了这个问题 [#1500](https://github.com/XTLS/Xray-core/issues/1500) ，~~只是不想改~~

因为根据历史，机场会用 SS 或 VMess 中转 XTLS 出墙，XTLS 把苦力活全干了，还给 GFW 喂了大量数据，却对社区没有任何帮助
我觉得这样并不好，所以我不会去改它，当然 PR is acceptable [#2.2](https://github.com/XTLS/Xray-core/issues/1612#issuecomment-1418880212)

:exclamation::exclamation::exclamation:

现在可以直接配置 REALITY H2 服务端，实测 N 个请求只开一条 H2，延迟超低，纵享丝滑。"flow" 为空，"network" 改为 "h2" 即可。

另一种方式是配置 REALITY VLESS 回落至 H2C，它可以与 Vision 共存，但暂不建议。H2 自带 MUX，理论上也可以减轻 TLS in TLS 特征，是否有效仍需实测。~~但若目标域名在白名单内，可能测不出区别。~~ [#3.1](https://t.me/projectXtls/57)

---

与 VLESS 回落功能无关，我看了下群，都什么理解啊，主动探测连 REALITY 那关都过不去，还轮得到 VLESS 回落？

用了 REALITY，VLESS 的回落就不是给你回落到网站用的，是给 Vision 与 H2 / gRPC 同端口共存用的。 [#3.2](https://github.com/XTLS/Xray-core/issues/1769#issuecomment-1464820362)

---

REALITY 是 TLSv1.3，VLESS 有回落很正常，默认回落到 H2C 或 gRPC 就能共存了，~~但这俩协议不一定不封端口，风险自负~~

~~其实我有个猜想，就是对于白名单网站，可能现在 GFW 并不分析流量模型，所以测不出来封不封端口~~ [#3.3](https://github.com/XTLS/Xray-core/issues/1769#issuecomment-1464821647)

---

gun（gRPC）最初就是 @DuckSoft 看到 CloudFlare 支持 gRPC 回源后写的，不是“gRPC后来也发展到过CDN”。

REALITY 不能过免费 CDN，故 gRPC 与 H2 区别不大，由于 gRPC 是 over H2，**直接用 H2 相对省一点点**。
REALITY 支持 gRPC 是顺手写的，just for fun，~~毕竟相比于 H2 大家更喜欢 gRPC，多 padding 一点可能还是好事？~~

你可以看到 Xray-core 内 REALITY 的第一个 commit 就有 REALITY H2 客户端支持，本来是没打算支持 gRPC 的。
~~但是 REALITY WS 就算了吧，这个组合属实没有必要。~~ [#3.4](https://github.com/XTLS/Xray-core/discussions/1719#discussioncomment-5138312)

:exclamation::exclamation::exclamation:

关于机场，说实话，我对机场落地这类技术，持保留态度。

从去年底乃至这些年的经验来看，**很多时候，GFW 的封锁策略优先讲究一个最多人用、最大收益，而不是你协议特征明不明显。**
TLS 类一疯狂，指纹和 TLS in TLS 检测就被重点安排上了，反而是小众的 UDP 类没有被针对、还可以用。
要说特征，其实混淆后的 UDP 包一眼假，检测起来比 TLS 类更容易，只是机场已经遍地 TLS 类，而 UDP 类还是自建居多。

那谁会成为靶子就很明显了，这也好理解，**假如你是 GFW 的供应商，最后交差个 FQ 封锁率才百分之几的东西，不太合适吧。**
肯定先找用的人多的下手，也就是机场喜欢用的那些什么 SS / VMess，什么 Trojan，针对研究，一封一片，效果拔群。

~~所以~~ [#4.1](https://github.com/XTLS/Xray-core/issues/1767#issuecomment-1464882669)

---

开混淆可以暂时解决“没有真正的 h3 server 而露馅”的问题，但是带来了另一个问题，**即变成了全随机数，它本身就是更明显的特征**

以前对于 SS 这类“全随机数是不是最大的特征”还有过争议，现在已经没有悬念了，**GFW 直接封了目标 IP 也不会有什么附带伤害**

根据目前的反馈，暂时只有部分地区的 GFW 把该策略应用到了 UDP，且暂时只是封端口，~~但是一旦机场大规模上，就~~ [#4.2](https://github.com/XTLS/Xray-core/issues/1767#issuecomment-1465101806)

:exclamation::exclamation::exclamation:

不稀罕，你不说我差点忘了，去年我有个套 CF 的 WSS 遇到了不断升级的“智能墙”：

- 最初，WSS 被精准阻断（网站能上），研究发现用 [Browser Dialer](https://github.com/XTLS/Xray-core/pull/421) 就能解决，所以是 Golang WSS 指纹被针对了。
- 不久后，又被精准阻断，**研究发现若一段时间内用浏览器打开过网页，WSS 才能用，加个自动请求解决了。**
- 最后，众所周知，TLS in TLS 检测被部署了，CF 节点倒没被直接封端口，但即时丢包干扰更恶心，相信不少人都深有体会。 [#5.1](https://github.com/XTLS/Xray-core/issues/1750#issuecomment-1459340564)

---

顺便，我说一下 WSS 代理为什么能被精准识别：

- **指纹：即使开了伪装，它发的 ALPN 始终为** `http/1.1~`，**一眼 WSS，实际上无法做到我们想要的“藏木于林”，只会裸送人头。**
- 握手：WSS 内层的 WS 要多握手一次，时序特征非常独特。其实开 [early data](https://github.com/XTLS/Xray-core/pull/375) 可以缓解，若不得不用 WSS，建议 `?ed=2048`
- TLS in TLS：这是 TLS 代理普遍存在的特征，需要针对性处理。多路复用可以缓解内层 TLS 握手特征，但却加重了“加密套娃”的特征，参考 [**XTLS Vision, TLS in TLS, to the star and beyond**](https://github.com/XTLS/Xray-core/discussions/1295) #1295 第二大段，所以目前 XTLS Vision 是较优解法。

**所以我现在的建议是：不要用 WSS，并且它应当被列为 deprecated**。套 CDN 有 gRPC，直连有 N 种姿势，已无任何必要用 WSS。 [#5.2](https://github.com/XTLS/Xray-core/issues/1750#issuecomment-1459469821)

:exclamation::exclamation::exclamation:

对于这一点，我建议大家修改一下 policy 的 handshake 和 connIdle 等，不要用默认值，不然特征太明显

~~中间人多收集些数据，分析出握手 60 秒超时 + 连接 300 秒超时，这不是 *ray 还能是~~啥 [#6.1](https://github.com/XTLS/Xray-core/issues/1511#issuecomment-1376887076)

---

回落当然是必要的，尤其是现在我们大规模用 uTLS 模仿浏览器指纹，GFW 一个探测，没网页的话岂不是一眼假？

服务端指纹特征是一个值得解决的问题。 [#6.2](https://github.com/XTLS/Xray-core/issues/1511#issuecomment-1382042986)

</details>
