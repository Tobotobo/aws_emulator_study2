FROM mcr.microsoft.com/devcontainers/base:ubuntu26.04

# 日本語ロケールと日本時間の設定
ENV LANG=ja_JP.UTF-8 \
    LANGUAGE=ja_JP:ja \
    TZ=Asia/Tokyo
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        locales \
        tzdata \
    && sed -i 's/^# *ja_JP.UTF-8 UTF-8/ja_JP.UTF-8 UTF-8/' /etc/locale.gen \
    && locale-gen \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo "$TZ" > /etc/timezone \
    && rm -rf /var/lib/apt/lists/*

# AWS CLI のインストール
# https://docs.aws.amazon.com/ja_jp/cli/latest/userguide/getting-started-install.html
RUN curl -fsSL https://awscli.amazonaws.com/v2/install.sh | bash -s -- --system

# Python と AWS SDK for Python (Boto3) をインストール
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        python3 \
        python3-boto3 \
    && rm -rf /var/lib/apt/lists/*