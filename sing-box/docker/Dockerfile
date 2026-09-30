ARG SING_BOX_VERSION=latest

FROM ghcr.io/sagernet/sing-box:${SING_BOX_VERSION}

ARG REDIRECT_PKG_HANDLER_VERSION
ARG REDIRECT_PKG_URL=https://github.com/ThisSeanZhang/landscape/releases/download/${REDIRECT_PKG_HANDLER_VERSION}/redirect_pkg_handler-${REDIRECT_ARCH}-static

RUN apk update && \
    apk add --no-cache libgcc libelf s6-overlay iptables

ADD --chmod=755 ${REDIRECT_PKG_URL} /redirect_pkg_handler

COPY rootfs /

ENTRYPOINT [ "/init" ]
