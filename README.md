# surge
Surge 自用配置（公开仓库版）

> 本仓库只放公开版配置：订阅链接用占位符，私人订阅链接的版本不上传。
> 本地另有一份 `Surge-CN-Custom-SanJose-Chuncheon.conf`，仅在本地工作副本里，不推送。

## 配置

- `Surge-CN-SanJose-Chuncheon-upload.conf`：公开版主配置。Google / AI / Meta 走 San Jose，Cryptocurrency 走 Chuncheon。
- 本地 Custom 版与公开版的区别只有订阅链接不同，规则、策略组、模块引用一致。

## 结构

- `Rules/`：配置引用的全部规则（19 个 `.list`），已从第三方仓库整理到本仓库，来源见 `Rules/SOURCES.md`。`.conf` 不再直接引用第三方 RULE-SET 地址。
- `Modules/`：Surge 模块（模块卡片里单独安装，不写进 `.conf`）。
- `Scripts/`：模块引用的脚本。
- `Icons/`：策略组图标（原生 App Store 图标，透明底，约 1.5 倍放大版）。

## YouTube 去广告（当前启用）

- 当前启用：`Modules/YouTube.Enhance.iKeLee.sgmodule`（iKeLee 版，本地解密）
  - 安装：`https://raw.githubusercontent.com/kobelalala/surge/main/Modules/YouTube.Enhance.iKeLee.sgmodule`
  - 去广告、画中画、字幕翻译（默认简体中文）、YouTube Music、后台播放；UMP 解密在手机本地完成，不经过任何第三方 Worker。
  - 2026-11-09 在 Surge 实测：完全没广告。
  - 启用前须开 MITM、重写、脚本三个开关；一次只能启用一个 YouTube 模块，启用本模块前先停用 Siu-Leung 版。
- 备用（停用）：`Modules/YouTube.Enhance.Local.sgmodule`（Siu-Leung 版，本地解密），脚本在 `Scripts/YouTube-Local/`。
- 已删除：旧 Maasea 版模块与脚本（2026-11-09 删除，7 月构建，跟不上 YouTube 7 月 11–12 日的链路变化）；自建 Cloudflare Worker `youtubead` 也已删除，不再使用。
- 详情与来源见 `Modules/SOURCES.md`。

## 相关仓库

- `kobelalala/adblock-scripts`：iKeLee 插件合集 fork（Loon `.lpx`，以后加 Surge 目录），275 个插件，引用已全部改成自己的地址。Loon 插件不能直接装进 Surge，要逐个转写成 `.sgmodule` 再实测。

## 图标

`Icons/`：Apple（黑苹果标）、Muse、Disney+（米奇头）、Netflix、Steam（透明底）、OKX（加密钱包，透明底）、YouTube（透明底红色播放按钮）。

## 注意

- 不要把包含私人订阅链接的版本上传到公开仓库。
- 改动配置后先在本地 Custom 版测，确认无误再同步到公开版。
