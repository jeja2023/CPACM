# 使用轻量级 Python 3.11 镜像
FROM python:3.11-slim

# 设置工作目录
WORKDIR /app

# 设置环境变量
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    APP_DATA_DIR=/app/data \
    APP_LOGS_DIR=/app/logs \
    WEBUI_HOST=0.0.0.0 \
    WEBUI_PORT=9090

# 安装运行所需的系统库（不包括编译环境，仅保留运行库以减小体积）
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpq5 \
    curl \
    && rm -rf /var/lib/apt/lists/*

# 复制依赖文件并安装
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 复制项目代码
COPY . .

# 确保脚本有执行权限 (如果后续需要脚本)
# RUN chmod +x docker/*.sh

# 设置存储卷，持久化数据库和日志
VOLUME ["/app/data", "/app/logs"]

# 暴露端口
EXPOSE 9090

# 直接使用 python 运行 webui.py 启动 FastAPI 服务
CMD ["python", "webui.py"]
