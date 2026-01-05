# ===============================
# Fluentd (EKS + Elasticsearch)
# ===============================
FROM fluent/fluentd:v1.16-debian-1

USER root

# Debian 계열이므로 apt 사용
RUN apt-get update && apt-get install -y \
    build-essential \
    ruby-dev \
    curl \
    tzdata \
    libffi-dev \
    libssl-dev \
 && rm -rf /var/lib/apt/lists/*

# 필수 플러그인만 설치 (정확)
RUN gem install \
    fluent-plugin-kubernetes_metadata_filter \
    fluent-plugin-elasticsearch \
    fluent-plugin-parser-cri \
    fluent-plugin-prometheus \
    fluent-plugin-s3 \
 && gem sources --clear-all

ENV TZ=Asia/Seoul

USER fluent

CMD ["fluentd", "-c", "/fluentd/etc/fluent.conf"]
