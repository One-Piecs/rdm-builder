![CI for redis desktop manager](https://github.com/One-Piecs/rdm-builder/workflows/CI%20for%20redis%20desktop%20manager/badge.svg)

# rdm-builder

Redis Desktop Manager Builder for windows and macOS

Official Download: [https://resp.app](https://resp.app)

一个编译Windows版和macOS版Redis Desktop Manager的Github Action。

有条件的同学请支持官方版本: [https://resp.app](https://resp.app)

其他版本：

- [RedisDesktopManager-Windows](https://github.com/lework/RedisDesktopManager-Windows)
- [RedisDesktopManager-Mac](https://github.com/onewe/RedisDesktopManager-Mac)

## Release & Pre-release

- [Windows 版](https://github.com/One-Piecs/rdm-builder/releases)
- [macOS 版](https://github.com/One-Piecs/rdm-builder/releases)（Apple Silicon / arm64）
- [Pre-release](https://github.com/One-Piecs/rdm-builder/releases/tag/2022-weekly) [___Weekly___] 🎉

## 版本说明

预发布标签固定为 `2022-weekly`，每次构建直接覆盖更新，不新增版本号。

| 产物 | 平台 / 架构 | 系统要求 | 额外依赖 | 体积 |
| --- | --- | --- | --- | --- |
| `resp-2022.99.0.exe` | Windows x64 | Windows | 无 | 约 20 MB |
| `RESP.dmg` | macOS arm64 | macOS 15 及以上 | 无（自带精简后的 Python 运行时） | 约 46 MB |
| `RESP-nopython.dmg` | macOS arm64 | macOS 15 及以上 | 需先安装 Homebrew `python@3.14`（Apple Silicon 版 Homebrew） | 约 29 MB |

- **该下哪个**：Mac 用户直接用 `RESP.dmg`，开箱即用。只有本机已经用 Homebrew 装了 `python@3.14` 的，才建议选 `RESP-nopython.dmg` 省下那 17 MB——缺少该 Python 时程序会直接启动失败。
- **源码**：上游 [redis/RedisDesktopManager](https://github.com/redis/RedisDesktopManager) 的 `2022` 分支（末端提交 `15f6d855`，2023-04-18）
- **应用版本号**：`2022.99.0`，表示 2022 线的最新开发态；上游最后一个 tag 是 `2022.5.1`（2023-03-01）
- **架构**：macOS 仅提供 arm64（Intel 版已停更，macOS 后续版本也不再支持 x86_64 应用）；Windows 为 x64

## 构建方式

上游源码已经冻结（停在 `2022` 分支末端，2023-04），所以构建改为**手动触发**，不再定时运行。

1. 打开 [Actions](https://github.com/One-Piecs/rdm-builder/actions) → `CI for redis desktop manager` → `Run workflow`
2. 跑完后产物会更新到 [Pre-release](https://github.com/One-Piecs/rdm-builder/releases/tag/2022-weekly)

> 默认分支就是 `pre-release`，`Run workflow` 会默认基于它运行，无需手动切换分支。
> 一次构建约 10 分钟（Windows 与 macOS 两侧都会全量编译）。

## Credits & 感谢

- [RedisDesktopManager](https://github.com/redis/RedisDesktopManager)
- [Build from source](http://docs.redisdesktop.com/en/latest/install/)
- [rdm编译打包的github Action配置](https://onew.me/2020/07/01/rdm-action/)
- [Qt使用github-Actions自动化发行](https://zhuanlan.zhihu.com/p/95926317)
- [源码编译Redis Desktop Manager](https://kany.me/2019/10/10/compile-redis-desktop-manager/)
- [JetBrains Open Source Support](https://www.jetbrains.com/community/opensource/#support)
