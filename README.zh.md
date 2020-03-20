# MuseDashModLoader
Muse Dash 插件加载器

[![Build status](https://ci.appveyor.com/api/projects/status/x6u9uqyk0cvrnoa5?svg=true)](https://ci.appveyor.com/project/mo10/musedashmodloader)

## 与修改游戏文件或第三方启动器有何不同？

安装MuseDashModLoader仅需要复制几个文件到游戏目录下即可，该过程中不会覆盖任何文件。

MuseDashModLoader将自动跟随游戏一同运行，无需您修改任何启动参数，与您平常启动游戏一样。

因为MuseDashModLoader不会修改您的游戏文件，所以就算游戏更新也不会影响到MuseDashModLoader的运行。

## 安装MuseDashModLoader

首先，[在这里](https://ci.appveyor.com/project/mo10/musedashmodloader/build/artifacts)下载Dist Release.zip

然后，解压里面的文件到Muse Dash游戏目录下

最后，运行游戏，MuseDashModLoader会随着您游戏自动运行

### 安装mod

将您的mod放在Mods文件夹即可。

如果您是第一次安装，没有找到Mods文件夹，可以手动创建或运行一次游戏。如果MuseDashModLoader工作正常，则会自动创建Mods文件夹。

### 卸载mod

将您要卸载的mod从Mods文件夹中移除即可。

### 如何找到我的Muse Dash游戏目录

打开Steam，在左侧游戏列表中找到Muse Dash，按下您的鼠标右键，点击"属性"，在属性窗口中的"本地文件"选项卡中点击"浏览本地文件"，就会打开Muse Dash所在目录。

## 听起来有点香，如何开发新插件呢？

MuseDashModLoader的插件开发非常简单：您只需要按照步骤操作即可快速上手：

需要的开发工具：Visual Studio (推荐使用2017或者2019)

创建插件工程：

1. 打开Visual Studio
2. 克隆本仓库或使用现有`IMod.dll`文件均可
3. 新建工程 -> 类库(.NET Framework) 框架版本选择.NET Framework 3.5
4. 在创建好的工程中，找到解决方案资源管理器，  
然后将本仓库的`IMod项目`添加到您的解决方案中，最后在您的插件项目中引用IMod项目即可。  
如果您使用IMod.dll进行开发，只需在引用中选择该DLL即可。  
切记不要直接复制`IMod.cs`文件到您的工程中。这样编译出的插件MuseDashModLoader无法加载！
5. 新建一个插件入口类，类名随您喜欢，只需实现IMod Interface接口即可。
6. 此处省略十万行代码，由您自行发挥想象力。
7. 开发完后的分发插件：您的输出目录可能会存在很多个DLL文件，比如IMod.dll。  
这些文件都是不需要的（MuseDashModLoader附带了Harmony与IMod），唯一有价值的就是您项目名.dll，将它复制到Mods文件夹下启动游戏即可自动运行。

## IMod接口说明

string Name:插件名  
string Description:插件描述  
string Author:作者  
string HomePage:项目地址  
以上接口为选填项目，可以部分留空  
string RequireAssembly:在特定Assembly加载后执行DoPatching方法。  
如"Assembly-CSharp"，不填写则不会执行DoPatching方法。

void DoPatching():插件执行方法，可以在这里进行您的操作，如修改内置方法。

## 异常

如果您的插件在执行DoPatching方法时抛出异常则可以在ModLoader.log找到报错信息。其他情况需要您自己实现异常捕捉。

## 鸣谢

MuseDashModLoader的诞生离不开许多开源项目。

Proxy:https://github.com/NeighTools/UnityDoorstop  
Harmony:https://github.com/pardeike/Harmony