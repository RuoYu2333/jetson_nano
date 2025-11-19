# jetson_nano
work on jetson_nano
# 为 Jetson Nano 配置烧录 RT 内核

## 1. 加载 WSL 环境

参考 [微软官方 WSL 文档](https://learn.microsoft.com/zh-cn/windows/wsl/install)。

## 2. 交叉编译 RT 内核并烧录

参考 [论坛指南]https://chipnbits.github.io/content/projects/RLUnicycle/rtkernel/rtpatch.html)

```
~~
在 `make -j4` 之前，修改以下文件：

**`scripts/dtc/dtc-lexer.lex.c_shipped`**，找到：
```c
YYLTYPE yylloc;
```
修改为：
```c
extern YYLTYPE yylloc;
```

**`Kbuild.include`**，找到：
```make
the-space :=
the-space +=
```
修改为：
```make
E =
the-space = $E $E
```

`j4` 修改为 `j16`：
```

其他步骤严格按照参考博客进行。
以上方案问题很大，在安装完后发现不明原因会开不了机
~~



```
**`NEW`**


# jetson_nano配置tensorflow

## 目前教研室的nano只支持jetpack4.6.1，注意版本！！！！！

## 参考博客：https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html

注意修改：官方直接使用了developer.nvidia里边的最新tensorflow，注意修改nano版本号为v461，不要使用官方的命令直接install，进入网址的目录，使用wget或者点击下载tensorflow1.15，否则不兼容实验室的nano

直接安装的话h5py一定会报错，建议单独安装：https://forums.developer.nvidia.com/t/failed-building-wheel-of-h5py/263322，

其他情况可能会有工具链setuptools==65.5.0这一步的版本问题，自行搜索nvidia官方论坛解决

安装好tensorflow后会有illegal 的报错，记得设置环境变量export OPENBLAS_CORETYPE=ARMV8，想一劳永逸就把它加入到bashrc里边

