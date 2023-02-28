＃中文
>**警告**\
不要使用你的主要苹果账户！更喜欢第二个Apple帐户\
>如果您的苹果账户发生任何事情，我不负责。
这是什么？
Provision是一套与Linux上的Apple服务器交互的工具。
它包括：
-*libprovision*，用于在Apple服务器上注册设备的库。
-*anisette-server*，用于其他软件的anisette配置服务器，如
[altserver linux]（https://github.com/NyaMisty/AltServer-Linux）的。
-*retrieve-headers*，将设备注册为libprovision，并在终端中返回
JSON用于在未来请求中识别设备的标头。
-*sideload-ipa*，如何使用libprovision和continue requests安装应用程序的示例
我们有一台苹果设备。
注：*侧加载IPA*尚未完成。
更准确地说，libprovision将设备注册到Apple服务器，并为您的设备检索ADI数据。
一旦您登录到您的机器，您的机器将被Apple使用此数据安全记住
小心只登录受信任的机器，不要泄露存储在~/.adi/adi.pb中的adi数据。
＃Downloads
您可以在[操作]中下载可执行文件（https://github.com/Dadoum/Provision/actions）项目选项卡。
Docker
如果您希望在Docker中运行Anisette以托管公共或私有服务器。确保安装docker/podman并运行以下命令：

```bash
docker run -d -v lib_cache:/opt/lib/ --restart=always -p 6969:6969 --name anisette dadoum/anisette-server:latest
```

上述命令将拉出图像并在背景中运行。卷（lib-cache:/opt/lib/）将缓存运行时获取的所需库。这样做不是为了重新分发AppleMusic库。
＃依赖关系
在运行时，libprovision需要一些Apple库作为可执行文件的旁边。你应该
下载Apple Music APK（如果您愿意，只需为您的设备提供架构切片），然后提取
可执行文件旁边的lib/folder。如果您想进一步缩小尺寸，可以在库中删除/
文件夹除libstoreservicescore.so和libcoreadi.so之外的所有库，因为它们是唯一的库需要运行应用程序。
要构建这些项目中的任何一个，您需要CMake，一个C和C++编译器，D SDK，以及编译器以及dub和libplist开发包（如果可能的话）（您可以在没有它的情况下编译大多数项目）。
要构建*sideload.ipa*，您还需要gtk+、libimobiledevice和libgmp开发包。
＃汇编
克隆项目并使用CMake编译：

```bash
git clone https://github.com/Dadoum/Provision --recursive
cd Provision
mkdir build
cd build
cmake -G Ninja .. -DCMAKE_BUILD_TYPE=Release 
ninja
```

此存储库包括Boost许可下的arsd/jni.d。请参阅[原始repo]（https://github.com/adamdruppe/arsd）更多信息。
