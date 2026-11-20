# Pika 探针监控（LazyCat 打包）

[pika-monitor/pika](https://github.com/pika-monitor/pika) 的懒猫微服打包仓库（镜像模式）。

采用上游官方镜像 `dushixiang/pika` + `victoriametrics/victoria-metrics`（SQLite 变体），
打包仓库不存储上游源码，版本升级由 GitHub Action 定期检查上游镜像 tag 并自动构建、发布。

- 应用包名：`community.lazycat.app.pika`
- 当前版本：0.2.8（跟随上游）
- 发布目标：喵喵商店（私有商店）；官方商店未启用
- 数据目录：`/lzcapp/var/data`（SQLite、日志、config.yaml）、`/lzcapp/var/vmdata`（时序指标，保留 7 天）

## 默认管理员

用户名 `admin`，初始密码见 `content/pika/config.yaml` 中 `Users` 段的注释（与上游
`docs/deployment-sqlite.md` 一致）。登录后请修改 `content` 中初始密码的说明并提示用户
在数据目录 `config.yaml` 里改 bcrypt 哈希。

首次启动会把内置默认配置种到数据目录并生成随机 JWT 密钥；之后每次启动从数据目录的
`config.yaml` 刷新容器内配置，用户改配置后重启应用即生效。
