## 准备

中文 ⋅ [English](English.md) ⋅ [Français](LISEZMOI.md)

> ️️️️️️警告  \
>不要使用您的苹果主帐户！首选辅助苹果帐户。  \
>如果您的Apple帐户出现问题，与我无关。

## 这是怎麽？
Provisioning 是一组与 Linux 上的 Apple 服务器交互的工具。

它包括：

- *libprovision，一个用于在 Apple 服务器上注册设备的库。
- *anisette_server，用于其他软件（如AltServer-Linux）的Anisette配置服务器[AltServer-Linux](https://github.com/NyaMisty/AltServer-Linux)。
- *retrieve_headers，它将设备注册到 libprovision 并在终端中返回 JSON 用于在将来的请求中标识设备的标头。
- *sideload_ipa，有关如何使用 libprovisioning 并继续请求安装应用程序的示例 在苹果设备上。  

注意：sideload_ipa尚未完成。

更准确地说，libprovisioning 将设备注册到 Apple 服务器，并检索设备的 ADI 数据。 使用机器登录一次后，Apple会使用此数据记住您的计算机是安全的 请注意，仅在受信任的计算机上登录，并且不要泄露存储在 中的 ADI 数据。~/.adi/adi.pb

## 下载
您可以在项目的“操作[Actions](https://github.com/Dadoum/Provision/actions)”选项卡中下载可执行文件。

## 容器
<h1 align="center">Watt Toolkit 🧰 (原名 Steam++)</h1>

<div align="center">

[English](./README.en.md) | 简体中文

「Watt Toolkit」是一个开源跨平台的多功能游戏工具箱，此工具的大部分功能都是需要您下载安装 Steam 才能使用。

![Release Download](https://img.shields.io/github/downloads/BeyondDimension/SteamTools/total?style=flat-square)
[![Release Version](https://img.shields.io/github/v/release/BeyondDimension/SteamTools?style=flat-square)](https://github.com/BeyondDimension/SteamTools/releases/latest)
[![GitHub license](https://img.shields.io/github/license/BeyondDimension/SteamTools?style=flat-square)](LICENSE)
[![GitHub Star](https://img.shields.io/github/stars/BeyondDimension/SteamTools?style=flat-square)](https://github.com/BeyondDimension/SteamTools/stargazers)
[![GitHub Fork](https://img.shields.io/github/forks/BeyondDimension/SteamTools?style=flat-square)](https://github.com/BeyondDimension/SteamTools/network/members)
![GitHub Repo size](https://img.shields.io/github/repo-size/BeyondDimension/SteamTools?style=flat-square&color=3cb371)
[![GitHub Repo Languages](https://img.shields.io/github/languages/top/BeyondDimension/SteamTools?style=flat-square)](https://github.com/BeyondDimension/SteamTools/search?l=c%23)
[![NET 7.0](https://img.shields.io/badge/dotnet-7.0-purple.svg?style=flat-square&color=512bd4)](https://learn.microsoft.com/zh-cn/dotnet/core/whats-new/dotnet-7)
[![C# 11](https://img.shields.io/badge/c%23-11-brightgreen.svg?style=flat-square&color=6da86a)](https://learn.microsoft.com/zh-cn/dotnet/csharp/whats-new/csharp-11)

[![爱发电](https://img.shields.io/badge/爱发电-软妹币玩家-blue.svg?style=flat-square&color=ea4aaa&logo=github-sponsors)](https://afdian.net/@rmbgame)
[![Kofi](https://img.shields.io/badge/Kofi-RMBGAME-orange.svg?style=flat-square&logo=kofi)](https://ko-fi.com/rmbgame)
[![Patreon](https://img.shields.io/badge/Patreon-RMBGAME-red.svg?style=flat-square&logo=patreon)](https://www.patreon.com/rmbgame)

[![Build Status](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Factions-badge.atrox.dev%2FSteamTools-Team%2FSteamTools%2Fbadge%3Fref%3Ddevelop&style=flat-square)](https://actions-badge.atrox.dev/BeyondDimension/SteamTools/goto?ref=develop)
[![GitHub Star](https://img.shields.io/github/stars/BeyondDimension/SteamTools.svg?logo=github)](https://github.com/BeyondDimension/SteamTools)
[![Gitee Star](https://gitee.com/rmbgame/SteamTools/badge/star.svg)](https://gitee.com/rmbgame/SteamTools)
[![Rebder](https://img.shields.io/badge/bilibili-软妹币玩家-blue.svg?style=flat-square&logo=bilibili)](https://space.bilibili.com/797215)
[![QQ群](https://img.shields.io/badge/QQ群-960746023-blue.svg?style=flat-square&color=12b7f5&logo=qq)](https://jq.qq.com/?_wv=1027&k=3JKPt4xC)

</div>
- [![Render](./render.svg?style=flat-square&logo=Render)](https://dashboard.render.com/register)

如果您希望在 docker 中运行 Anisette 以公共或私有方式托管服务器。确保安装 docker/podman 并运行以下命令：
```bash
docker run -d -v lib_cache:/opt/lib/ --restart=always -p 6969:6969 --name anisette dadoum/anisette-server:latest
```
上面的命令将拉取图像并在后台运行它。卷 （lib_cache:/opt/lib/） 将缓存在运行时获取的所需库。这样做是为了不重新分发Applemusic库。

##依赖
在运行时，libprovision 要求一些 Apple 库位于可执行文件旁边。你应该 下载苹果音乐APK（或者如果您愿意，也可以只是设备的架构切片），然后提取 可执行文件旁边的 lib/ 文件夹。如果你想进一步减小大小，你可以在lib/ 文件夹除 libstoreservicescore.so 和 libCoreADI.so 之外的所有库，因为它们是唯一的库 需要运行应用。

若要生成这些项目中的任何一个，需要 CMake（一个 C 和 C++ 编译器、D SDK）和编译器 如果可能的话，以及 dub 和 libplist 开发包（您可以在没有它的情况下编译大多数项目）。

要构建sideload_ipa，您还需要 GTK+、libimobiledevice 和 libgmp 开发包。

## 汇编
克隆项目并使用 CMake 编译它：

```bash
git clone https://github.com/Dadoum/Provision --recursive
cd Provision
mkdir build
cd build
cmake -G Ninja .. -DCMAKE_BUILD_TYPE=Release 
ninja
```
此存储库包括 arsd/jni.d，在 Boost 许可证下。有关详细信息，请参阅原始存储库[original repo](https://github.com/adamdruppe/arsd)。
