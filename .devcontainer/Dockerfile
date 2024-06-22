# ベースイメージとしてUbuntuを使用
# 匿名ユーザーは100回/6Hの制限があるので注意
# https://www.docker.com/ja-jp/increase-rate-limits/
FROM ubuntu:latest

# パッケージリストを更新し、必要なパッケージをインストール
RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    openjdk-11-jdk \
    build-essential \
    git \
    unzip \
    zip

# Bazelのインストール
RUN curl -fsSL https://bazel.build/bazel-release.pub.gpg | gpg --dearmor >bazel-archive-keyring.gpg \
    && mv bazel-archive-keyring.gpg /usr/share/keyrings/bazel-archive-keyring.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/bazel-archive-keyring.gpg] https://storage.googleapis.com/bazel-apt stable jdk1.8" | tee /etc/apt/sources.list.d/bazel.list \
    && apt-get update && apt-get install -y bazel \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

    # Buildifierのインストール
RUN curl -LO https://github.com/bazelbuild/buildtools/releases/download/5.1.0/buildifier-linux-amd64 \
&& chmod +x buildifier-linux-amd64 \
&& mv buildifier-linux-amd64 /usr/local/bin/buildifier

# ワークディレクトリの設定
WORKDIR /workspace

# デフォルトのシェルをbashに設定
CMD [ "bash" ]
