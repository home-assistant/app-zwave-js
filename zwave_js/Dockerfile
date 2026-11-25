# Base image updated by Renovate, update versionCompatibility on Alpine base bump
ARG BUILD_FROM=ghcr.io/home-assistant/base:3.23-2026.11.1@sha256:b9916671d3df931e47f2f90a219520e091b364c3a05a6d54dc5c9e1545bccf0b
FROM ${BUILD_FROM}

ARG ZWAVEJS_UI_VERSION=11.27.0

# Environment configuration
ENV \
    S6_KILL_GRACETIME=3000 \
    S6_SERVICES_GRACETIME=25000 \
    STORE_DIR=/config

# Install Z-Wave JS UI
WORKDIR /usr/src
RUN \
    set -x \
    && apk add --no-cache \
        nodejs \
        npm \
    && apk add --no-cache --virtual .build-dependencies \
        build-base \
        git \
        linux-headers \
        python3 \
    \
    && npm install -g "zwave-js-ui@${ZWAVEJS_UI_VERSION}" \
    \
    && apk del --no-cache \
        .build-dependencies

WORKDIR /
COPY rootfs /

LABEL \
    org.opencontainers.image.title="Home Assistant App: Z-Wave JS" \
    org.opencontainers.image.description="Control a Z-Wave network with Home Assistant Z-Wave JS" \
    org.opencontainers.image.source="https://github.com/home-assistant/app-zwave-js" \
    org.opencontainers.image.licenses="Apache License 2.0"
