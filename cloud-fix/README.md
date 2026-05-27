# 云编译配置参考

本目录镜像 [ku891/build-actions](https://github.com/ku891/build-actions) 的 ImmortalWrt x86_64 配置。

## 当前默认插件（主固件 x86_64）

- OpenClash、MosDNS、DDNS、SQM、KMS  
- **不含 fileshare**（与最初可稳定云编译的配置一致；需要时可按下方自行加回）

## Cudy TR3000（256MB Flash）

- seed 文件：`build/Immortalwrt/seed/cudy-tr3000-256m`  
- 机型：`cudy_tr3000-256mb-v1`（**不是** 128MB 的 `cudy_tr3000-v1`）  
- 在 `settings.ini` 中设置：`CONFIG_FILE="cudy-tr3000-256m"`

## 可选：自行加回 fileshare Go 版

插件仓库：[ku891/fileshare-openwrt](https://github.com/ku891/fileshare-openwrt)（`go-v2.0` 为 Go 实现，不依赖 Node）

1. 在 `diy-part.sh` 末尾、`CLEAR_PATH` 之前增加：

```bash
grep -q 'src-git fileshare' feeds.conf.default || \
  echo 'src-git fileshare https://github.com/ku891/fileshare-openwrt.git;go-v2.0' >> feeds.conf.default
```

2. 在 `seed/x86_64` 增加：

```
CONFIG_PACKAGE_fileshare=y
CONFIG_PACKAGE_luci-app-fileshare=y
```

## 单独云编译 fileshare IPK（不编整固件）

在 [ku891/build-actions Actions](https://github.com/ku891/build-actions/actions) 中手动运行工作流：**「单独编译-fileshare-IPK」**。

- 可选择 ImmortalWrt 分支、`fileshare-openwrt` 分支（默认 `go-v2.0`）  
- **TARGET_PROFILE**：`x86_64`；TR3000 机型请用本目录 seed **`cudy-tr3000-256m`** 编全固件（上游 Actions 的 TR3000 选项仍指向 128MB 旧机型，256MB 版勿选）  
- 完成后在 **Artifacts** 下载 `fileshare*.ipk`（及可选 `luci-app-fileshare*.ipk`）

## 相关仓库

| 仓库 | 作用 |
|------|------|
| ku891/build-actions | 云编译流程与 seed |
| ku891/common | 公共脚本 |
| ku891/fileshare-openwrt | fileshare 插件（可选） |
| ku891/bendi | 本地 `local.sh`（本仓库未改其核心脚本） |

