# Base image updated by Renovate, update versionCompatibility on Alpine base bump
ARG BUILD_FROM=ghcr.io/home-assistant/base:3.23-2026.10.1@sha256:9fd5d40f0682f0dee626cd0d2ea07b96ffef345dac1c6f025d4b4ce30ad362b4
FROM ${BUILD_FROM}

ARG ZWAVEJS_UI_VERSION=11.25.1

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
