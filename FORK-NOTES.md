# LaoDong fork：森罗厨房 1.6.0 兼容修复

适用环境：Minecraft 1.21.1、NeoForge、Kaleidoscope Cookery 1.6.0。

旧兼容扩展的磨盘 Mixin 使用 `canBindEntity(Mob)`，而森罗厨房 1.6.0
已将该方法参数改为 `LivingEntity`。这会在模组加载时触发
`InvalidInjectionException`，随后可能出现 Sodium 配置未初始化的连锁错误。

本 fork 将注入参数和编译依赖更新到 1.6.0，并提高最低本体版本要求，
避免旧版本体与新版注入接口混用。女仆磨盘任务的判断逻辑保持原样。

## 构建与下载

使用 JDK 21 执行 `./gradlew build`（Windows 为 `gradlew.bat build`）。
GitHub Actions 支持 push、pull request 和手动运行。
在成功的 Build 运行页面中，下载 `kaleidoscope-compat-mc1.21.1-<commit>`
artifact 并解压，即可获得 `build/libs` 下的 JAR。

在 XMCL 中禁用旧版 `kaleidoscope_compat`，再导入新 JAR。
同一个实例中只能启用一份该模组。编译成功不代表所有可选模组联动均经过游戏测试；
仍需验证启动、进入世界和磨盘功能。
