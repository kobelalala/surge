# YouTube 去广告模块来源

- 原模块：Maasea/sgmodule `YouTube.Enhance.sgmodule`（2026-10-27 拉取，构建日期：response 2026/7/19，request 2026/7/12）
- 本仓库文件：
  - `Modules/YouTube.Enhance.sgmodule`：原模块改写，仅把两个 script-path 换成本仓库 raw 链接，名称、参数、MITM hostname 不变
  - `Scripts/YouTube/youtube.response.js`：原样复制
  - `Scripts/YouTube/youtube.request.js`：原样复制
- 未完全消除的外部依赖：`youtube.request.js` 内仍引用 `https://init-stream.maasea.workers.dev/`（initplayback 的 UMP 处理），该 Worker 代码不在 Maasea 公开仓库里，无法直接搬运；主去广告逻辑（response 脚本）在本仓库内。
