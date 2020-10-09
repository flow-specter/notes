# vcpkg配置、使用、踩坑全记录

## 1. 搭配vs2019 配置

我的vs版本本身是2013的，但是下载的vcpkg仿佛不能够使用vs2013，于是我又换了vs2019（事实上vcpkg只支持vs2015以上的版本），但是语言包只安装了中文的，而vcpkg需要其变换为英文，我又将其变成了英文，具体的问题描述及语言包安装见 [vcpkg报错 could not locate a complete toolset](https://zhuanlan.zhihu.com/p/120183174)  以及[Visual Studio 2019 更改语言包](https://zhuanlan.zhihu.com/p/120183174)两个参考链接。

## 2. 搭配cmake使用

[参考链接： github vcpkg说明](https://github.com/microsoft/vcpkg/blob/master/docs/examples/installing-and-using-packages.md#cmake-toolchain-file)

[参考链接： 微软官方文档](https://docs.microsoft.com/en-us/cpp/build/vcpkg?view=vs-2019)

搭配cmake使用安装的库的最好的方式就是通过toolchain文件，scripts\buildsystems\vcpkg.cmake（本地位置在：E:\vcpkg\scripts\buildsystems\vcpkg.cmake）。

为了使用这个文件，有两种方式：

1. 直接在CMake的命令行中设置`-DCMAKE_TOOLCHAIN_FILE=D:\src\vcpkg\scripts\buildsystems\vcpkg.cmake`

2. 利用Open Folder的方式使用的Cmake，那么可以通过添加一个变量section在CMakeSettings.json中，具体可参考[微软下的说明文档](https://github.com/microsoft/vcpkg/blob/master/docs/examples/installing-and-using-packages.md#cmake-toolchain-file)。

   ```cmake
   {
     "configurations": [{
       "name": "x86-Debug",
       "generator": "Visual Studio 15 2017",
       "configurationType" : "Debug",
       "buildRoot":  "${env.LOCALAPPDATA}\\CMakeBuild\\${workspaceHash}\\build\\${name}",
       "cmakeCommandArgs": "",
       "buildCommandArgs": "-m -v:minimal",
       "variables": [{
         "name": "CMAKE_TOOLCHAIN_FILE",
         "value": "D:\\src\\vcpkg\\scripts\\buildsystems\\vcpkg.cmake"
       }]
     }]
   }
   ```

   （我在.json文件中加入变量后去`include`库的时候，仍然提示找不到错误，我一度以为是vcpkg出了什么问题，或者是cmake哪里没搞懂，但事实上是我include的地方错了，所以小白读者或许可以和我一样去查看一下include的位置到底有没有那个库。）

