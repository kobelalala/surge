# YouTube 去广告模块来源

## Maasea 版（已删除，2026-11-09）

- 原模块：Maasea/sgmodule `YouTube.Enhance.sgmodule`（2026-10-27 拉取，构建日期：response 2026/7/19，request 2026/7/12）
- 已删除文件：`Modules/YouTube.Enhance.sgmodule`、`Scripts/YouTube/youtube.response.js`、`Scripts/YouTube/youtube.request.js`
- 删除原因：2026 年 7 月构建的旧脚本跟不上 YouTube 7 月 11～12 日换的加密 Onesie/UMP 链路，已由本地解密方案（Siu-Leung）替代。
- 注：`youtube.request.js` 内曾引用 `https://init-stream.maasea.workers.dev/`（initplayback 的 UMP 处理），该 Worker 代码不在 Maasea 公开仓库里，无法直接搬运。

## YouTube 本地解密模块（Siu-Leung）

- 原模块：Siu-Leung/surge-youtube-enhance `modules/youtube-enhance.sgmodule`（2026-11-08 拉取；fork 自 gholts/surge，源自 Maasea，Apache-2.0）
- 本仓库文件：
  - `Modules/YouTube.Enhance.Local.sgmodule`：原模块改写，6 处 script-path 换成本仓库 raw 链接；`#!name` 由 `YouTube Enhance` 改为 `YouTube Enhance (Local)`，以便与 Maasea 版在 Surge 里区分；参数、规则、MITM hostname 不变
  - `Scripts/YouTube-Local/request.js`：原样复制
  - `Scripts/YouTube-Local/response.js`：原样复制（含内联的 MIT 协议第三方库 fflate、@noble/ciphers、@noble/hashes，版权头保留在文件内）
- 特点：UMP 解密在脚本内本地完成（AES-128-CTR + HMAC-SHA256），不依赖任何 Cloudflare Worker；自建 Worker 可弃用。
- 注意：Maasea 版已于 2026-11-09 删除；现保留本本地解密模块与 iKeLee 版（见下），二选一。
- 外部引用：模块与两个脚本内已无指向 Siu-Leung 仓库的引用；`response.js` 内仅有 paulmillr.com 的版权署名文字（注释），不是拉取地址。

## YouTube 本地解密模块（iKeLee 版）

- 原插件：fkingikelee/fkikelee `lpx/YouTube_remove_ads.lpx`（2026-11-01 归档，插件打包日期 2026-10-02；作者 Maasea、VirgilClyne、Choler、DivineEngine、app2smile；已 fork 并改名至 kobelalala/adblock-scripts，引用已全部改成自己的地址）
- 本仓库文件：
  - `Modules/YouTube.Enhance.iKeLee.sgmodule`：新写（非原样搬运），`#!name` 为 `YouTube Enhance (iKeLee, Local)`，以便与 Siu-Leung 版区分；一次只能启用一个 YouTube 模块
  - `Scripts/YouTube-iKeLee/response.js`：iKeLee 插件的 response 脚本原样复制（Maasea 2026/7/19 构建，作者注释保留）；负责 youtubei 响应去广告、字幕翻译（改 caption track 加 tlang 参数，由 YouTube 自己翻译，不向外发请求）、画中画、YouTube Music、后台播放；参数 blockUpload/blockShorts/blockImmersive/captionLang/debug 由模块 `#!arguments` 传入
  - `Scripts/YouTube-iKeLee/request.js`：Siu-Leung `Scripts/YouTube-Local/request.js` 原样复制；负责 initplayback 密钥校验、log_event 去 hot-hash 头、player/ad_break 拦截
  - `Scripts/YouTube-iKeLee/ump-decrypt.js`：Siu-Leung `Scripts/YouTube-Local/response.js` 原样复制，仅挂在 initplayback 响应上做 UMP 本地解密（含内联的 MIT 协议第三方库 fflate、@noble/ciphers、@noble/hashes，版权头保留在文件内）
- 关键改动：iKeLee 原 request 脚本（Maasea 2026/7/12 构建）会把 initplayback 重定向到 Maasea 的 Worker（`https://init-stream.maasea.workers.dev/`）做 UMP 解密——已去掉，改成本地解密；运行时代码里不再有 workers.dev / Maasea Worker 地址（仅 response.js 文件头保留 Maasea 署名注释）。
- 密钥流转：三脚本共用 `$persistentStore` 的 `YouTubeConfig`（平台键 `youtube`/`youtubeMusic`，值 `{clientKey, encryptKey}` base64）；response.js 从 player/config/log_event 响应里取 onesieHotConfig 存入，request.js 校验 initplayback 请求，ump-decrypt.js 解密 initplayback 响应。
- 注意：本模块与 Siu-Leung 版 `YouTube.Enhance.Local` 二选一，不可同时启用；两个模块的脚本各自独立成套，互不引用。
