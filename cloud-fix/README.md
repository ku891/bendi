# 云编译配置参考

本目录是 [ku891/build-actions](https://github.com/ku891/build-actions) 中 **Immortalwrt / x86_64** 配置的本地镜像，便于对照与备份。

## 目录

| 文件 | 说明 |
|------|------|
| `build/Immortalwrt/seed/x86_64` | 默认选中的软件包 |
| `build/Immortalwrt/diy-part.sh` | 编译前环境变量、旁路由、主题等 |

## 当前 x86_64 默认插件

- OpenClash（含 Ruby 依赖）
- MosDNS
- DDNS（含 Cloudflare）
- SQM
- KMS（vlmcsd）

**不包含** fileshare（已移除，避免 node 编译失败）。

## 修改后如何生效

1. 将改动同步到 GitHub：`ku891/build-actions` 对应路径  
2. 本地编译：删除 `~/operates` 后重新运行 `local.sh`  
3. 云编译：Actions → **Immortalwrt-天灵** → `x86_64`

## 相关仓库

- 云编译流程：`ku891/build-actions`
- 公共脚本：`ku891/common`
- 本地一键编译：本仓库 `local.sh`
