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

- [windows](https://github.com/One-Piecs/rdm-builder/releases)
- [macOS](https://github.com/One-Piecs/rdm-builder/releases)（Apple Silicon / arm64，需 macOS 15 及以上），两种打包方式：
  - `RESP.dmg` — 自带精简后的 Python 运行时，换任何一台 Mac 都能直接跑（推荐，约 50 MB）
  - `RESP-nopython.dmg` — 不打包 Python，体积更小（约 30 MB），但**要求目标 Mac 已安装 Homebrew `python@3.14`**，否则无法启动
- [Pre-release](https://github.com/One-Piecs/rdm-builder/releases/tag/2022-weekly) [___Weekly___] 🎉

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
