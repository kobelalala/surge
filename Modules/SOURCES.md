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
- 注意：Maasea 版已于 2026-11-09 删除，现仅保留本本地解密模块。
- 外部引用：模块与两个脚本内已无指向 Siu-Leung 仓库的引用；`response.js` 内仅有 paulmillr.com 的版权署名文字（注释），不是拉取地址。
