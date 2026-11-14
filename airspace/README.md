# Airspace Home Assistant 加载项 6.9.50

仓库地址：https://github.com/ckjensun-liao/HAnetbar

在 Home Assistant 加载项商店添加以上仓库地址，安装或更新 AI电竞智控。继续使用 airspace slug 与原有加载项数据目录 /data；升级前请创建完整备份。管理页面默认端口 8125，客户端入口端口 8100 仍由加载项配置控制。

本公共仓库仅提供安装 metadata、Dockerfile 与使用说明。原始源码不发布；开发与构建在私有仓库完成。GitHub 自动生成的 “Source code (zip)” 和 “Source code (tar.gz)” 仅包含本安装 metadata，不能作为完整离线运行包。Release 中唯一的 HA-O-Airspace-6.9.50.zip 才是完整 HA 安装包。

后端以固定 Node 24.21.0 的 V8 字节码分发。字节码仍可逆向分析，不是加密，也不承诺不可还原。前端浏览器资源可见，可通过浏览器下载与检查。安装脚本使用精确 SHA256 验证 Release ZIP 的完整性。

首次安装请填写 ha_url、ha_token 与 initial_admin_password。已有安装保留 /data，不要卸载加载项或清空数据。initial_admin_password 非空时，每次启动按该值设置管理员密码；留空保留已有密码。未配置 HA 凭据的启动状态不代表已完成业务连接验证。

在线安装与更新见 [INSTALL.md](../INSTALL.md)。本版本保留原有授权行为，不新增不可绕过授权的承诺。
