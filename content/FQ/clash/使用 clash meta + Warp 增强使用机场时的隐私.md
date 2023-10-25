---
tags:
  - privacy
---
warp 需要用到的 wireguard 目前不支持在 [[链式代理|relay]] 中使用， 只能在 proxy 配置 [[dialer-proxy]]

proxy-groups 中添加前置代理的分组
```yaml
- {
name: 前置,
type: select,
proxies: [DIRECT, 自动选择, 默认, 香港, 台湾, 美国, 日本, 新加坡, 其它地区],
}
```
Warp 配置
```yaml
- name: WARP
type: wireguard
server: engage.cloudflareclient.com
port: 2408
ip: 172.16.0.2
ipv6: 2606:4700:110:8f0f:c898:f966:48a7:4ebf
private-key: "private-key"
public-key: "public-key"
udp: true
remote-dns-resolve: true
dns: ["1.1.1.1", "8.8.8.8"]
dialer-proxy: "前置"
```
上面例子，Clash <-> 前置 <-> WARP <-> Internet

## 说说作用
- 防止机场主监视
	- 机场主是有能力监视你访问的每一个地址和访问时间，特别是某些机场主有恶俗倾向。如果套上 warp，机场主就只能看到 warp 的加密流量。
- 访问机场禁止访问的网站