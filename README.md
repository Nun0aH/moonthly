# moonthly
这是一个用以记录每月订阅的应用软件，你可以通过他来提醒每月的订阅清单和分析每月的订阅支出/"This app helps you track your monthly subscriptions — it reminds you of what you're subscribed to each month and breaks down your monthly subscription spending."
[README.md](https://github.com/user-attachments/files/35211271/README.md)
# moonthly · 每月订阅清单

Android 原生订阅管理 App：记录订阅、到期滚动、提醒、月度统计。本地优先，不联网、无账号。
Kotlin + Jetpack Compose (Material 3) + Room，minSdk 26 / compileSdk 36 / targetSdk 34。

**当前版本 0.1.3（versionCode 4）**：大纲第一版功能全部完成，MuMu 模拟器 + 小米 真机实测通过。


## 构建

1. 装 JDK 17 + Android SDK（platforms;android-36、build-tools;36.0.0、platform-tools），见《环境搭建记录》
2. `moonthly/local.properties` 写本机 `sdk.dir=...`（该文件 gitignore）
3. `cd moonthly && ./gradlew assembleDebug`（Gradle wrapper 8.14.8，distributionUrl 已指腾讯镜像）
4. 单元测试：`./gradlew testDebugUnitTest`（22 项）
5. **出安装包必须补 v1 签名**（国产 ROM 扫描器需要）：
   `apksigner sign --ks <keystore> --v1-signing-enabled true --v2-signing-enabled true --v3-signing-enabled true --out moonthly-x.y.z.apk app/build/outputs/apk/debug/app-debug.apk`
   当前用本机 debug keystore（`~/.android/debug.keystore`，口令 android）；**换钥匙会导致无法覆盖升级**，正式分发前决定是否迁 release keystore
6. 字体再生成：`python design/_tools/build_misans.py`（需 fonttools+brotli；MiSans GB2312 子集四档字重）

## 安装与测试

- 模拟器：MuMu 12，`adb connect 127***0.1:16384`；分辨率 custom 1080×2400@480
- 真机（国产 ROM）：APK 经微信传输后**保存到存储、从文件管理安装**（微信内直接装会报解析错误 33）；覆盖安装保留数据
- 真机必测四项见《第一版开发记录》§8

## 许可

字体：MiSans（小米免费商用）、Noto Serif SC（SIL OFL 1.1），全文见 app/src/main/assets/licenses.txt。
参考项目 capllen/Subnook 仅借鉴框架思路（MIT），未复制其内容。
