# 使用官方 NVIDIA PyTorch 基础镜像
FROM pytorch/pytorch:2.5.1-cuda12.4-cudnn9-devel

# 设置工作目录
WORKDIR /workspace/ms-swift

# 设置环境变量
ENV PYTHONUNBUFFERED=1 \
    DEBIAN_FRONTEND=noninteractive \
    TZ=Asia/Shanghai \
    CUDA_HOME=/usr/local/cuda

# 安装系统依赖
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    wget \
    curl \
    vim \
    build-essential \
    cmake \
    ninja-build \
    libsndfile1 \
    libgl1-mesa-glx \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender-dev \
    libgomp1 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# 升级 pip 并安装基础工具
RUN pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
RUN pip install --no-cache-dir --upgrade pip "setuptools<81" wheel

# 复制项目文件到容器
COPY . /workspace/ms-swift/

# 安装依赖
RUN pip install --no-cache-dir "vllm>=0.5.1,<0.11.1" && \
    pip install --no-cache-dir "sglang<0.5.6" && \
    pip install --no-cache-dir "deepspeed<0.18" && \
    pip install --no-cache-dir qwen_vl_utils qwen_omni_utils keye_vl_utils

# 可参考 requirements/install_all.sh 安装更多可选依赖

# 安装 ms-swift 及全部依赖（使用全能力安装）
# 此命令会安装 base + eval + swanlab + ray 等所有额外依赖
RUN pip install --no-cache-dir -e '.[all]'

# 暴露端口
ENV WEBUI_PORT=8000
EXPOSE 8000

ENTRYPOINT [ "swift", "web-ui" ]
