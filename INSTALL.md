# 安装与升级

1. 在 Home Assistant 中创建完整备份，保存加载项配置。
2. 打开“设置 → 加载项 → 加载项商店 → 仓库”，添加 https://github.com/ckjensun-liao/HAnetbar 。保留 URL 拼写与 airspace slug，现有仓库加载项标识继续为 b01fe0ae_airspace。
3. 刷新加载项商店，安装或更新至 6.9.35。构建时会下载固定版本 ZIP 并核验确切 SHA256。下载或哈希校验失败会停止构建。
4. 保留现有 /data，不卸载加载项、不删除账号、授权、备份或数据库。配置 ha_url / ha_token，首次安装设置 initial_admin_password。
5. 启动后打开主机 8125 端口，检查版本、账号登录、HA 连接、任务及备份。8100 客户端端口默认不开放，按实际需求设置。

离线／本地安装：下载 Release 中唯一的 HA-O-Airspace-6.9.35.zip，按 SHA256 校验后解压，将 airspace 目录放入 /addons/airspace，刷新本地加载项并构建。ZIP 内 Dockerfile 直接 COPY 本地 runtime 与 app；不需要下载自身。ZIP 不是 HA 备份。

GitHub 自动的 Source code 压缩档只有安装 metadata；完整运行内容仅在上述 Release ZIP 中。Node 与 CPU 架构必须匹配，支持 amd64 和 aarch64。不要用其他 Node 版本重写 runtime。
