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
推送到 `1.21.1-NeoForge` 分支或手动运行该分支时，构建成功后自动创建
GitHub Release 并附上可安装的 JAR；可以直接从仓库 Releases 页面下载。
Release 标签格式为 `v<mod_version>-build.<构建编号>`，无需每次更新版本号。
重新运行同一构建会更新该 Release 的附件，不创建重复 Release。
Pull request 只执行构建，不发布 Release。其他分支手动运行也不会发布。
Actions 运行页面仍保留 `kaleidoscope-compat-mc1.21.1-<commit>` artifact，
下载并解压也能获取 JAR。Release 与 artifact 都排除 sources、javadoc 和 dev JAR。

在 XMCL 中禁用旧版 `kaleidoscope_compat`，再导入新 JAR。
同一个实例中只能启用一份该模组。编译成功不代表所有可选模组联动均经过游戏测试；
仍需验证启动、进入世界和磨盘功能。
