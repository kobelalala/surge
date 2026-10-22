# 规则来源说明

本目录的规则于 2026-10-23 从原配置引用的第三方仓库整理而来，现统一由本仓库维护。
两个 .conf 已改为引用本仓库 `Rules/` 下的文件，不再直接引用第三方 RULE-SET 地址。

## Rabbit-Spec/Surge（Rules/）
上游：https://github.com/Rabbit-Spec/Surge （Master/Rules/）

- AIGC.list、Google.list、Apple.list、Microsoft.list、Telegram.list、Game.list
- YouTube.list、Netflix.list、Disney.list、BiliBili.list、ChinaMedia.list、GlobalMedia.list
- Proxy.list、China.list、ChinaCIDR.list

## blackmatrix7/ios_rule_script（rule/Surge/）
上游：https://github.com/blackmatrix7/ios_rule_script

- Facebook.list、Instagram.list、Threads.list
- Crypto.list 已整合进 Cryptocurrency.list（见下）

## Cryptocurrency.list（整合版）
- blackmatrix7 的 Crypto.list（201 条）
- 本仓库两个 .conf 中额外手动增加的交易所/钱包规则：Binance、OKX、Bybit（含 bybit.biz、bybdc6.com、byapps.net 等补充域名）、Bitget、Gate、Crypto.com、MetaMask、Trust Wallet、Ledger、Trezor、WalletConnect、Alchemy、Infura、Ankr、QuickNode 等
- 合并后去重，共 224 条。原先散落在 .conf 里的内联交易所规则已全部移入此文件。

## 仍保留外部引用的非规则内容
- 图标（icon-url，来自 Rabbit-Spec/Surge）
- GeoIP 数据库（geoip-maxmind-url，来自 Hackl0us/GeoIP2-CN，为二进制 .mmdb 文件，未纳入 Rules/）
