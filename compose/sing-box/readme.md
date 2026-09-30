# sing-box 与 Landscape 软路由实现透明代理

> [!question]
> 在`compose`文件中一定要挂载`Landscap`配置目录中`uninx_link`目录
> 使用旧版本`sniff`

## 添加节点

在`app/server/sing-box`目录下添加自己的节点，配置节点选择和自动选择的节点信息。

## 启动容器

通过命令启动容器，之后在`Landscape`中配置流的走向即可。


```shell
docker builder build --build-arg SING_BOX_VERSION=v1.14.0 --build-arg REDIRECT_PKG_HANDLER_VERSION=v0.24.3 --platform linux/arm64,linux/loong64,linux/riscv64,linux/s390x,linux/amd64 .
```

```json
{
  "supported": [
    "linux/amd64",
    "linux/amd64/v2",
    "linux/amd64/v3",
    "linux/arm64",
    "linux/riscv64",
    "linux/ppc64le",
    "linux/s390x",
    "linux/386",
    "linux/mips64le",
    "linux/mips64",
    "linux/loong64",
    "linux/arm/v7",
    "linux/arm/v6"
  ],
  "emulators": [
    "qemu-aarch64",
    "qemu-arm",
    "qemu-loongarch64",
    "qemu-mips64",
    "qemu-mips64el",
    "qemu-ppc64le",
    "qemu-riscv64",
    "qemu-s390x"
  ]
}
```