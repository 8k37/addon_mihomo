ARG BUILD_FROM="ghcr.io/home-assistant/amd64-base:3.19"
FROM ${BUILD_FROM}

ARG XUI_VERSION
ARG BUILD_ARCH

# Map Home Assistant arch to 3x-ui release arch
RUN set -eux; \
    case "${BUILD_ARCH}" in \
      amd64)   XUI_ARCH=amd64 ;; \
      i386)    XUI_ARCH=386 ;; \
      aarch64) XUI_ARCH=arm64 ;; \
      armv7)   XUI_ARCH=armv7 ;; \
      armhf)   XUI_ARCH=armv5 ;; \
      *) echo "unsupported arch: ${BUILD_ARCH}"; exit 1 ;; \
    esac; \
    apk add --no-cache ca-certificates curl tar tzdata; \
    curl -fsSL -o /tmp/xui.tar.gz \
      "https://github.com/MHSanaei/3x-ui/releases/download/v${XUI_VERSION}/x-ui-linux-${XUI_ARCH}.tar.gz"; \
    mkdir -p /app; \
    tar -xzf /tmp/xui.tar.gz -C /app; \
    rm -f /tmp/xui.tar.gz; \
    chmod +x /app/x-ui/x-ui /app/x-ui/bin/* 2>/dev/null || true

COPY rootfs /
