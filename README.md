# jetson_nano
work on jetson_nano
# 为 Jetson Nano 配置烧录 RT 内核

## 1. 加载 WSL 环境

参考 [微软官方 WSL 文档](https://learn.microsoft.com/zh-cn/windows/wsl/install)。

## 2. 交叉编译 RT 内核并烧录

参考 [NVIDIA 论坛指南](https://forums.developer.nvidia.com/t/applying-a-preempt-rt-patch-to-jetpack-4-5-on-jetson-nano/168428/4) 和英伟达官方文档。

```

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
