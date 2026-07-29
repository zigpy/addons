ARG BUILD_FROM=ghcr.io/home-assistant/base:3.23

FROM rust:1-alpine AS builder

RUN apk add --no-cache git musl-dev

ARG ZIGGURAT_VERSION=96face24e321f990d80ad5269bd9d1b2efc3c8fc

ENV CARGO_PROFILE_RELEASE_LTO=true \
    CARGO_PROFILE_RELEASE_CODEGEN_UNITS=1 \
    CARGO_PROFILE_RELEASE_PANIC=abort \
    CARGO_PROFILE_RELEASE_STRIP=true

RUN --mount=type=cache,target=/usr/local/cargo/registry \
    --mount=type=cache,target=/tmp/cargo-target \
    CARGO_TARGET_DIR=/tmp/cargo-target \
    cargo install ziggurat-server \
        --git "https://github.com/zigpy/ziggurat" \
        --rev "${ZIGGURAT_VERSION}" \
        --bin ziggurat \
        --locked \
        --root /usr/local

FROM ${BUILD_FROM}

COPY rootfs /
COPY --from=builder /usr/local/bin/ziggurat /usr/bin/ziggurat

HEALTHCHECK --interval=30s --timeout=5s --start-period=30s \
    CMD nc -z 127.0.0.1 9999 || exit 1
