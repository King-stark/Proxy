# Clash .NET 非官方帮助

### 1.这是什么软件？

一个使用Clash开源版内核的图形客户端，下载地址。与CFW类似，是方便用户在电脑中通过图形界面使用Clash内核。目前仅有Windows版本，若开发顺利，将有可能开发MacOS版本。有限支持闭源版Clash内核，需要用户手动更换内核文件。

与CFW相比，内存占用更低（后台时仅占用10M左右内存，前台占用内存在80M以下），界面可能更迎合部分人的审美。

软件依赖于.Net 5，需要安装.NET5 runtime及其Desktop支持的运行环境：
[64位下载地址](https://dotnet.microsoft.com/download/dotnet/thank-you/runtime-desktop-5.0.9-windows-x64-installer)
[32位下载地址](https://dotnet.microsoft.com/download/dotnet/thank-you/runtime-desktop-5.0.9-windows-x86-installer)

>_注：如遇界面字体显示不正常，需要安装字体：NotoSansHans-Bold、NotoSansHans-Medium与NotoSansHans-Regular。从此处下载Fonts.7z文件，下载解压后，双击字体文件，点击安装。_


3.Clash分为开源版本与闭源版本（Premium版），有什么区别？

闭源版本（Premium版）比开源版本多以下功能：TUN、Script（脚本模式）、Rule Providers。详见[官方文档](https://github.com/Dreamacro/clash/wiki/Premium-Core-Features)

4.可以自己更换不同版本的Clash内核吗？

可以自己更换不同版本，替换方法：关闭软件，打开软件目录内的/bin文件夹，复制新内核到此处，删除原来的Clash.exe文件，将新内核更名为Clash.exe。

闭源版本内核（Premium版）下载地址 https://github.com/Dreamacro/clash/releases/tag/premium ，32位下载“clash-windows-386”，64位下载“clash-windows-amd64”，下载后解压

>_注：使用闭源版内核时，因Clash .NET的界面不完善，无法切换该内核特有的Script模式。_</br>

>_注：为配合premium core 使用 TUN 模式需要以下内容： _</br>
>_下载最新的 wintun.dll 复制到Clash内核所在文件夹内  访问 https://www.wintun.ne_

5.配置文件夹
默认（xxxx.setup.exe）位于C:/user/用户名/.config/cdn，便携模式（xxx.7z）为软件目录内的/data文件夹。

其中/clash文件夹包含clash所使用的默认配置、GeoIP数据等clash运行所使用的文件；/logs包含了所有日志文件；/profiles包含了用户添加的clash配置；/settings中为Clash .NET软件自身的配置。

7.修改代理端口（clash默认配置）

代理端口会使用clash的默认配置文件中的设置。步骤：进入软件的配置文件夹内（默认为C:/user/用户名/.config/cdn，便携模式为软件目录内的data文件夹），打开clash文件夹内的config.yaml，修改第二行的mixed-port。重启软件生效

8.添加本地clash配置

直接拖动配置文件到软件的配置界面即可，如果失败，考虑使用管理员模式启动软件。


9.增强模式

目前提供进程代理以及Pcap代理2种增强模式。

进程代理类似TUN/TAP，可以方便的代理所有软件，使用简介：在设置-驱动中安装NetFilter驱动后，在设置-代理页面启用增强模式，增强模式选择Proc。注：该模式下会直接使用IP发起连接，基于域名的分流规则将失效。

Pcap代理类似于游戏加速器，可为局域网内其他设备提供Full Cone NAT代理服务。使用简介：在设置-驱动中安装Pcap驱动后，在设置-代理页面启用增强模式，增强模式选择Pcap。Pcap模式提供2种预设配置：Tencent（腾讯游戏加速器）和Netease（网易UU加速器）。具体参见https://github.com/zhxie/pcap2socks

10.日志

日志位于软件的配置文件夹（默认为c:/user/用户名/.config/cdn，便携模式为软件目录内的data文件夹）内的logs文件夹

Application.log为Clash .NET的日志（默认为c:/user/用户名/.config/cdn/logs/Application.log），Clash.log为Clash内核的日志
