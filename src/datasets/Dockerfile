# syntax=docker.io/docker/dockerfile:1

FROM docker.io/ubuntu:noble AS base

USER root

ENV TZ=Asia/Singapore \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    ca-certificates locales-all \
    curl jq \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /root

FROM base AS build

RUN curl -fsSL "https://ftp.ncbi.nlm.nih.gov/pub/datasets/command-line/v2/linux-$(case $(uname -m) in x86_64) echo amd64 ;; aarch64) echo arm64 ;; esac)/datasets" -o /tmp/datasets \
    && curl -fsSL "https://ftp.ncbi.nlm.nih.gov/pub/datasets/command-line/v2/linux-$(case $(uname -m) in x86_64) echo amd64 ;; aarch64) echo arm64 ;; esac)/dataformat" -o /tmp/dataformat \
    && mv /tmp/datasets /usr/local/bin \
    && mv /tmp/dataformat /usr/local/bin \
    && chmod +x /usr/local/bin/datasets /usr/local/bin/dataformat

FROM base AS final

COPY --from=build /usr/local/bin/datasets /usr/local/bin/datasets
COPY --from=build /usr/local/bin/dataformat /usr/local/bin/dataformat
