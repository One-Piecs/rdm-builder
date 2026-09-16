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
- [macOS](https://github.com/One-Piecs/rdm-builder/releases) (Apple Silicon / arm64，需 macOS 15 及以上)
- [Pre-release](https://github.com/One-Piecs/rdm-builder/releases/tag/2022-weekly) [___Weekly___] 🎉

## 构建方式

上游源码已经冻结（停在 `2022` 分支末端，2023-04），所以构建改为**手动触发**，不再定时运行。

1. 打开 [Actions](https://github.com/One-Piecs/rdm-builder/actions) → `CI for redis desktop manager` → `Run workflow`
2. 在 "Use workflow from" 下拉里选择 **pre-release** 分支
3. 跑完后产物会更新到 [Pre-release](https://github.com/One-Piecs/rdm-builder/releases/tag/2022-weekly)

> 注意：GitHub 只在**默认分支**上存在 `workflow_dispatch` 时才会显示 `Run workflow` 按钮，而本仓库默认分支目前是内容较旧的 `master`。若按钮不可见，把 Settings → General → Default branch 改成 `pre-release` 即可。

## Credits & 感谢

- [RedisDesktopManager](https://github.com/redis/RedisDesktopManager)
- [Build from source](http://docs.redisdesktop.com/en/latest/install/)
- [rdm编译打包的github Action配置](https://onew.me/2020/07/01/rdm-action/)
- [Qt使用github-Actions自动化发行](https://zhuanlan.zhihu.com/p/95926317)
- [源码编译Redis Desktop Manager](https://kany.me/2019/10/10/compile-redis-desktop-manager/)
- [JetBrains Open Source Support](https://www.jetbrains.com/community/opensource/#support)
