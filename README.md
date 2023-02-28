准备

>警告
>不要使用您的苹果主帐户！首选辅助苹果帐户。
>如果您的Apple帐户出现问题，我概不负责。

这是怎麽？
Provisioning 是一组与 Linux 上的 Apple 服务器交互的工具。

它包括：

libprovision，一个用于在 Apple 服务器上注册设备的库。
anisette_server，用于其他软件（如AltServer-Linux）的Anisette配置服务器。
retrieve_headers，它将设备注册到 libprovision 并在终端中返回 JSON 用于在将来的请求中标识设备的标头。
sideload_ipa，有关如何使用 libprovisioning 并继续请求安装应用程序的示例 在苹果设备上。
注意：sideload_ipa尚未完成。

更准确地说，libprovisioning 将设备注册到 Apple 服务器，并检索设备的 ADI 数据。 使用机器登录一次后，Apple会使用此数据记住您的计算机是安全的 请注意，仅在受信任的计算机上登录，并且不要泄露存储在 中的 ADI 数据。~/.adi/adi.pb

下载
您可以在项目的“操作”选项卡中下载可执行文件。

码头工人
如果您希望在 docker 中运行 Anisette 以公共或私有方式托管服务器。确保安装 docker/podman 并运行以下命令：

docker run -d -v lib_cache:/opt/lib/ --restart=always -p 6969:6969 --name anisette dadoum/anisette-server:latest
上面的命令将拉取图像并在后台运行它。卷 （lib_cache：/opt/lib/） 将缓存在运行时获取的所需库。这样做是为了不重新分发Applemusic库。

依赖
在运行时，libprovision 要求一些 Apple 库位于可执行文件旁边。你应该 下载苹果音乐APK（或者如果您愿意，也可以只是设备的架构切片），然后提取 可执行文件旁边的 lib/ 文件夹。如果你想进一步减小大小，你可以在lib/ 文件夹除 libstoreservicescore.so 和 libCoreADI.so 之外的所有库，因为它们是唯一的库 需要运行应用。

若要生成这些项目中的任何一个，需要 CMake（一个 C 和 C++ 编译器、D SDK）和编译器 如果可能的话，以及 dub 和 libplist 开发包（您可以在没有它的情况下编译大多数项目）。

要构建sideload_ipa，您还需要 GTK+、libimobiledevice 和 libgmp 开发包。

汇编
克隆项目并使用 CMake 编译它：

git clone https://github.com/Dadoum/Provision --recursive
cd Provision
mkdir build
cd build
cmake -G Ninja .. -DCMAKE_BUILD_TYPE=Release 
ninja
此存储库包括 arsd/jni.d，在 Boost 许可证下。有关详细信息，请参阅原始存储库。


# Provision

English ⋅ [Français](LISEZMOI.md)

> **Warning**  \
> Don't use your main Apple account! Prefer a secondary Apple account.  \
> I am NOT responsible if something happens with your Apple account.

## What is this ?

Provision is a set of tools interracting with Apple servers on Linux.

It includes:

- *libprovision*, a library used to register device on Apple servers.
- *anisette_server*, an Anisette provisioning server for other software such as
  [AltServer-Linux](https://github.com/NyaMisty/AltServer-Linux).
- *retrieve_headers*, which registers the device with libprovision and returns in the terminal in
  JSON the headers to use to identify the device on future requests.
- *sideload_ipa*, an example on how to use libprovision and continue requests to install application
  on an Apple device.

Note: *sideload_ipa* isn't finished yet.

More precisely, libprovision registers the device to Apple servers and retrieve ADI data for your device.
Once you logged in once with your machine, your machine is remembered as safe by Apple using this data
Be careful to log-in only on trusted machines, and don't leak your ADI data, which is stored in `~/.adi/adi.pb`.

## Downloads

You can download the executables in the [Actions](https://github.com/Dadoum/Provision/actions) tab of the project.

## Docker

If you wish to run Anisette within docker to host a server public or privately. Make sure to install docker/podman and run the following command:

```bash
docker run -d -v lib_cache:/opt/lib/ --restart=always -p 6969:6969 --name anisette dadoum/anisette-server:latest
```

The above command will pull the image and also run it in the background. The volume (lib_cache:/opt/lib/) will cache the libraries needed that are fetched at runtime. This is done as to not redistribute Applemusic lib's.

## Dependencies

At runtime, libprovision requires some Apple libraries to be next to the executables. You should
download Apple Music APK (or just the architecture slice for your device if you prefer), and extract
the lib/ folder next to the executables. If you want to reduce further the size, you can remove in the lib/
folder all the libraries except libstoreservicescore.so and libCoreADI.so, since they are the only one
needed to run the app.

To build any of these projects, you need CMake, a C and C++ compiler, the D SDK, with the compiler
and dub and libplist development packages if possible (you can compile most projects without it).

To build *sideload_ipa*, you also need GTK+, libimobiledevice and libgmp development packages.

## Compilation

Clone the project and compile it with CMake:

```bash
git clone https://github.com/Dadoum/Provision --recursive
cd Provision
mkdir build
cd build
cmake -G Ninja .. -DCMAKE_BUILD_TYPE=Release 
ninja
```

This repository include arsd/jni.d, under Boost license. See [original repo](https://github.com/adamdruppe/arsd) for further info.
