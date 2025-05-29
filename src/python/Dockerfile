# syntax=docker.io/docker/dockerfile:1

FROM docker.io/ubuntu:noble AS base

USER root

ENV TZ=Asia/Singapore \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    ca-certificates locales-all

WORKDIR /root

ARG PYTHON_VERSION=3.12

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    curl jq \
    python3.12 python3.12-venv \
    && python3.12 -m ensurepip --upgrade \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
