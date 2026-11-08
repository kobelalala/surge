# YouTube 去广告模块来源

- 原模块：Maasea/sgmodule `YouTube.Enhance.sgmodule`（2026-10-27 拉取，构建日期：response 2026/7/19，request 2026/7/12）
- 本仓库文件：
  - `Modules/YouTube.Enhance.sgmodule`：原模块改写，仅把两个 script-path 换成本仓库 raw 链接，名称、参数、MITM hostname 不变
  - `Scripts/YouTube/youtube.response.js`：原样复制
  - `Scripts/YouTube/youtube.request.js`：原样复制
- 未完全消除的外部依赖：`youtube.request.js` 内仍引用 `https://init-stream.maasea.workers.dev/`（initplayback 的 UMP 处理），该 Worker 代码不在 Maasea 公开仓库里，无法直接搬运；主去广告逻辑（response 脚本）在本仓库内。

## YouTube 本地解密模块（Siu-Leung）

- 原模块：Siu-Leung/surge-youtube-enhance `modules/youtube-enhance.sgmodule`（2026-11-08 拉取；fork 自 gholts/surge，源自 Maasea，Apache-2.0）
- 本仓库文件：
  - `Modules/YouTube.Enhance.Local.sgmodule`：原模块改写，6 处 script-path 换成本仓库 raw 链接；`#!name` 由 `YouTube Enhance` 改为 `YouTube Enhance (Local)`，以便与 Maasea 版在 Surge 里区分；参数、规则、MITM hostname 不变
  - `Scripts/YouTube-Local/request.js`：原样复制
  - `Scripts/YouTube-Local/response.js`：原样复制（含内联的 MIT 协议第三方库 fflate、@noble/ciphers、@noble/hashes，版权头保留在文件内）
- 特点：UMP 解密在脚本内本地完成（AES-128-CTR + HMAC-SHA256），不依赖任何 Cloudflare Worker；自建 Worker 可弃用。
- 注意：与 Maasea 版（`Modules/YouTube.Enhance.sgmodule`）二选一，不可同时启用。
- 外部引用：模块与两个脚本内已无指向 Siu-Leung 仓库的引用；`response.js` 内仅有 paulmillr.com 的版权署名文字（注释），不是拉取地址。
