# ===============================
# Fluentd (Production Base)
# ===============================
FROM fluent/fluentd:v1.16-1

USER root
WORKDIR /fluentd

# -------------------------------
# Build dependencies
# -------------------------------
RUN apk add --no-cache \
    build-base \
    ruby-dev \
    curl \
    tzdata \
    libffi-dev \
    openssl-dev \
    yaml-dev \
 && rm -rf /var/cache/apk/*

# -------------------------------
# RubyGems / Bundler 안정화
# -------------------------------
RUN gem update --system \
 && gem install bundler

# -------------------------------
# Fluentd plugins (순서 중요)
# -------------------------------
RUN gem install fluent-plugin-kubernetes_metadata_filter
RUN gem install fluent-plugin-elasticsearch
RUN gem install fluent-plugin-record-reformer
RUN gem install fluent-plugin-prometheus
RUN gem install fluent-plugin-s3

ENV TZ=Asia/Seoul

RUN chown -R fluent:fluent /fluentd

USER fluent

CMD ["fluentd", "-c", "/fluentd/etc/fluent.conf", "-p", "/fluentd/plugins"]
