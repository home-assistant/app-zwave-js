# Base image updated by Renovate, update versionCompatibility on Alpine base bump
ARG BUILD_FROM=ghcr.io/home-assistant/base:3.23-2026.10.3@sha256:1550b137f45bbb61f932a5ec97265c1d8594ddc4a986b127fb06a5c8c4bcaa6d
FROM ${BUILD_FROM}

ARG ZWAVEJS_UI_VERSION=11.25.2

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
