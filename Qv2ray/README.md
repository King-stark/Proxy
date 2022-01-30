# 有关于 Qv2ray 不再维护的通知

> _终版 [Qv2ray 2.7.0 - The End](https://github.com/Qv2ray/Qv2ray/releases/tag/v2.7.0)_

## Qv2ray 组织下其他项目均正常维护

这包括 gun, mmp-go, mochi, rc4md5cry, v2ray-rust, gun-lite, shadowboom, mmp-rs, qvrelease-bot 等

## 插件说明

目前 Qv2ray 支持的所有插件： [SS](https://github.com/Qv2ray/QvPlugin-SS/releases/tag/v3.0.0) / [SSR](https://github.com/Qv2ray/QvPlugin-SSR/releases/tag/v3.0.0) / [NaiveProxy](https://github.com/Qv2ray/QvPlugin-NaiveProxy/releases/tag/v3.0.0) / [Trojan](https://github.com/Qv2ray/QvPlugin-Trojan/releases/tag/v3.0.0) / [Trojan-Go](https://github.com/Qv2ray/QvPlugin-Trojan-Go/releases/tag/v3.0.0) / [Command](https://github.com/Qv2ray/QvPlugin-Command/releases/tag/v3.0.0) 均以完成最终版本发布。

需要注意的是，由于长时间无人维护：

- Linux 版本已无法再在 GitHub Actions 环境编译，
- 部分插件 Windows 版本因 GitHub Actions 环境变动较大编译失败，有需求的用户建议自行编译

## \#使用方式
### 1、选择对应自己的系统版本下载软件
### 2、下载 v2 or xray 核心

> _V2ray核心_</br>
> _https://github.com/v2fly/v2ray-core/releases_

> _Xray核心_ </br>
> _https://github.com/XTLS/Xray-core/releases_

### 3、在 Qv2ray 中配置 V2Ray Core
打开 Qv2ray 并转到首选项窗口。在 内核设置 中，配置以下选项：
* 核心可执行文件路径: 将此设置为您的 V2Ray 可执行文件存在的地方。这可能是您在 Windows 上的 v2ray.exe 的完整路径，或者 v2ray 在 Linux / macOS 上的可执行文件。
* V2Ray 资源目录: 将此设定为 geoip.dat 和 geosite.dat 所在位置。

配置后，您可以点击 检查 V2Ray 核心设置 按钮来验证您的 V2Ray 核心设置。重复尝试，直到检查通过。
> ***注意可用的 V2Ray Core 可执行文件看起来就像 v2ray、v2ray.exe 或 wv2ray.exe，而不是 qv2ray、qv2ray.exe 或 v2rayN.exe！***

将 v2ray 核心文件提取到一个固定路径。建议将文件提取到 $QV2RAY_CONFIG_PATH/vcore，其中 $QV2RAY_CONFIG_PATH 是 Qv2ray 存储数据的目录。
vcore 可能提取到的位置示例：
* ./config/ （这里的 config 指在 Qv2ray 可执行文件旁边的 config 子目录，Windows 用户推荐）
* ~/.qv2ray/ （在您的 home 文件夹的专用子目录中）
* ~/.config/qv2ray/ (标准 XDG 配置路径)

请确保这些文件存在于您的 vcore 目录中：
* 1、v2ray / v2ray.exe: 核心可执行文件
* 2、v2ctl / v2ctl.exe: 核心控制程序
* 3、geoip.dat: IP 规则数据库
* 4、geosite.dat: 域规则数据库

```
给 Linux / macOS 用户的特殊提示

你应该始终给予 v2ray 和 v2ctl 可执行权限。这通常是需要对这些文件执行一次 chmod +x 。

在 macOS 上，如果您使用 Homebrew 安装 v2ray-core，您可以忽略此提示。
```

### 4、根据对应系统配置插件
