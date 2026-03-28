# Docker 部署说明

本项目支持通过 Docker 容器化部署，建议使用 Docker Compose 以一键完成构建和运行。

## 目录结构
- `Dockerfile`: 定义了应用的运行环境（Python 3.11 ）。
- `docker-compose.yml`: 用于多容器编排，并指定了数据持久化卷。
- `data/`: (运行后生成) 持久化存储 SQLite 数据库及应用配置。
- `logs/`: (运行后生成) 持久化存储应用日志文件。

## 快速启动

在项目根目录下执行以下命令：

```bash
# 切换到 docker 目录
cd docker

# 启动容器 (首次启动会自动构建镜像)
docker-compose up -d
```

启动成功后，即可通过 `http://localhost:9090` 访问 Web 界面。

## 持久化说明
- 数据库文件存储在宿主机的 `docker/data/` 目录中。
- 日志文件存储在宿主机的 `docker/logs/` 目录中。
- 即使更新镜像或重启容器，数据也不会丢失。

## 常见操作

```bash
# 查看日志
docker-compose logs -f

# 停止并移除容器
docker-compose down

# 重新构建镜像并启动
docker-compose up -d --build
```

## 注意事项
1. 如果你需要修改访问端口，请调整 `docker-compose.yml` 中的 `ports` 映射。
2. 初始访问密码默认为 `admin123`（如果尚未在数据库中更改）。
3. 如果宿主机已经在使用 9090 端口，请修改宿主机侧的端口号。
