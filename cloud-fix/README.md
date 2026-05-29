# 云编译配置参考（Cudy TR3000 256MB）

本目录是 [ku891/build-actions](https://github.com/ku891/build-actions) 中 **Immortalwrt / TR3000** 配置的本地镜像。

## 刷机后无 WiFi 的常见原因

1. **`seed/cudy-tr3000-256m` 被写成 x86 配置**（云编译 trigger 曾误覆盖）→ 镜像缺无线栈。
2. **seed 只有机型三行、没有 `wpad-openssl` 等** → 射频驱动/ hostapd 不完整。
3. **`diy-part.sh` 里 `Kernel_partition_size=256`** → 仅适用于 x86，TR3000 必须填 **0**。

## 目录

| 文件 | 说明 |
|------|------|
| `build/Immortalwrt/settings.ini` | 云编译机型：`CONFIG_FILE="cudy-tr3000-256m"` |
| `build/Immortalwrt/seed/cudy-tr3000-256m` | mediatek 机型 + WiFi 包 |
| `build/Immortalwrt/diy-part.sh` | 旁路由、分区等 |

## 修改后如何生效

1. 将 `cloud-fix/build/Immortalwrt/` 下文件同步到 GitHub **`ku891/build-actions`** 同路径。
2. 确认远程 **`seed/cudy-tr3000-256m` 第一行是 `CONFIG_TARGET_mediatek=y`**，不是 `CONFIG_TARGET_x86`。
3. Actions → **Immortalwrt-天灵** → 等 **编译主程序** 成功。
4. 下载 **`*cudy_tr3000-256mb-v1*sysupgrade.bin`** 刷机。
5. 刷后 SSH 自检：`wifi status`、`opkg list-installed | grep wpad`。

## 相关仓库

- 云编译：`ku891/build-actions`
- 公共脚本：`ku891/common`
