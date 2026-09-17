# Qt 6 迁移记录

分支：`codex/qt6`
基线：上游 `redis/RedisDesktopManager` 的 `2022` 分支，提交 `15f6d85`（2023-04-18）
工具链：Qt 6.11.2（Homebrew，含 `qtcharts` 与 `qt5compat`）

## 现状

- ✅ **C++ 部分已能用 Qt 6 编译并链接**（本机实测：arm64、链接 QtCore / QtCharts / QtCore5Compat 6.11.2，0 错误）
- ❌ **QML 部分尚未迁移**，界面加载不了，应用启动后随即退出

## 已完成（见 `patches/qt6/0001-qt6-cpp-port.patch`，25 个文件）

| 问题 | 处理 |
| --- | --- |
| Qt6 要求 C++17 | `resp.pro` 里 `c++11` → `c++17` |
| `QRegExp` / `QTextCodec` 移出 QtCore | 引入 `core5compat` 模块；Qt6 不再隐式转换 QString→QByteArray，涉及处显式 `toUtf8()` |
| `QString::indexOf(QRegExp)`、`QByteArray::contains(QRegExp)` 移除 | 改用 `QRegularExpression`（通配符经 `wildcardToRegularExpression`） |
| `QSortFilterProxyModel::filterRegExp` 移除 | 改用 `filterRegularExpression`，并保留 `FilterSyntax`（RegExp / Wildcard / FixedString）语义 |
| `QtConcurrent::run(obj, &Cls::m, args…)` 与 `run(fn, args…)` 移除 | 改成 `run(&Cls::m, obj, args…)` / 包一层 lambda |
| `QAbstractSocket::error` 变成重载 | 信号指针改用 `&QAbstractSocket::errorOccurred` |
| `QSslSocket::addCaCertificates` 移除 | 改为取 `sslConfiguration()` 加证书后 `setSslConfiguration()` |
| `QQuickWindow::setSceneGraphBackend(enum)` | 改用 `setGraphicsApi()` |
| Qt Charts 去掉了 `QtCharts::` 命名空间 | 去掉命名空间前缀 |
| `QWeakPointer::data()` | 改用 `toStrongRef().data()` |
| pyotherside：`QJSValue::engine()` 移除 | 采用上游同款宏（`qjsEngine(this)`） |
| pyotherside：Qt 6.5 起 `Q_RETURN_ARG` 不再是 `QGenericReturnArgument` | 采用上游同款手写 `QGenericReturnArgument`（QTBUG-113147） |
| AsyncFuture 0.4.1 与 Qt6 不兼容 | `QVariant(QMetaType,…)`、去掉 `QRegExp`；回调 trait 改为区分「回调接收 QFuture」与「回调接收结果值」（与上游维护分支一致） |

## 待办（第二步的前置）

1. **32 个 QML 文件使用 Qt Quick Controls 1 / `Controls.Styles`** —— 该模块在 Qt6 中已删除，必须重写为 Controls 2。
   主要集中在 `qml/value-editor/`（17）、`qml/settings/`（5），其余散落在 `qml/common/` 等。
2. **83 个 QML 文件的 import 需要去掉版本号**（`import QtQuick 2.3` → `import QtQuick`，`import QtQuick.Controls 2.13` → `import QtQuick.Controls`）。
3. 界面外观迁移（深浅双主题、macOS 原生风格）与第 1 项是同一批文件，应一并完成。
4. 迁移后需实际启动验证；随后才把 Qt6 构建接入 CI。

## 复现方式

```bash
brew install qt qtcharts qt5compat          # Qt 6.11.2
git clone --branch 2022 --recursive https://github.com/redis/RedisDesktopManager.git rdm
cd rdm && git apply <此仓库>/patches/qt6/0001-qt6-cpp-port.patch
# 3rdparty 静态库（lz4/zstd/snappy/brotli）按 CI 步骤构建
export PATH="$(brew --prefix qt)/bin:$PATH"
cd src && qmake6 resp.pro CONFIG-=debug "VERSION=2022.99.0" && make -j8
```
