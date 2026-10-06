ARG BUILDER_IMAGER=golang:1.26.8
ARG BUILDPLATFORM
FROM --platform=${BUILDPLATFORM}  ${BUILDER_IMAGER} AS builder
ARG MIHOMO_VERSION
WORKDIR /mihomo
RUN curl -L https://github.com/MetaCubeX/mihomo/archive/refs/tags/v1.19.32.tar.gz \
      | tar -xz -C /mihomo --strip-components=1

RUN go env && \
    go build -v -tags "with_gvisor" -trimpath  \
    -ldflags "-extldflags '--static'  \
              -X 'github.com/metacubex/mihomo/constant.Version=${MIHOMO_VERSION}'  \
              -X 'github.com/metacubex/mihomo/constant.BuildTime=$(date)' -w -s -buildid="


ARG RUN_IMAGER=alpine
FROM ${RUN_IMAGER}
ARG REDIRECT_PKG_HANDLER_VERSION
ARG REDIRECT_ARCH
ARG REDIRECT_PKG_URL=https://github.com/ThisSeanZhang/landscape/releases/download/${REDIRECT_PKG_HANDLER_VERSION}/redirect_pkg_handler-${REDIRECT_ARCH}

RUN apk update && \
    apk add --no-cache libgcc libelf s6-overlay iptables

COPY --from=builder /mihomo/mihomo /usr/bin

ADD --chmod=755 ${REDIRECT_PKG_URL} /redirect_pkg_handler

COPY rootfs /

ENTRYPOINT [ "/init" ]
