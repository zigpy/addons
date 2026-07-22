ARG BUILD_FROM=ghcr.io/home-assistant/base:3.23

FROM rust:1-alpine AS builder

RUN apk add --no-cache musl-dev

# Targets the next zigpy/ziggurat release (the one including TCP RCP-transport
# support, PR #39) rather than the current 0.1.0 on crates.io, which predates it.
# zigpy/ziggurat's publish workflow stamps the crate version from the release tag at
# publish time, not from its Cargo.toml, so the exact next version number is whatever
# tag its maintainer cuts — confirm/adjust this before merging.
ARG ZIGGURAT_VERSION=0.2.0

ENV CARGO_PROFILE_RELEASE_LTO=true \
    CARGO_PROFILE_RELEASE_CODEGEN_UNITS=1 \
    CARGO_PROFILE_RELEASE_PANIC=abort \
    CARGO_PROFILE_RELEASE_STRIP=true

RUN --mount=type=cache,target=/usr/local/cargo/registry \
    --mount=type=cache,target=/tmp/cargo-target \
    CARGO_TARGET_DIR=/tmp/cargo-target \
    cargo install ziggurat-server \
        --version "${ZIGGURAT_VERSION}" \
        --bin ziggurat \
        --locked \
        --root /usr/local

FROM ${BUILD_FROM}

COPY rootfs /
COPY --from=builder /usr/local/bin/ziggurat /usr/bin/ziggurat

HEALTHCHECK --interval=30s --timeout=5s --start-period=30s \
    CMD nc -z 127.0.0.1 9999 || exit 1
