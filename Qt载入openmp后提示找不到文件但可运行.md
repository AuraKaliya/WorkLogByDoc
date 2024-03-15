## 问题描述

Qt Creator在通过CMake配置Openmp后，在引入<omp.h>头文件时提示找不到，但程序可正常编译运行。

![image-20240308100452995](C:/Users/Aura/AppData/Roaming/Typora/typora-user-images/image-20240308100452995.png)

## 解决过程

关掉Qt的ClangCodeModel插件

Qt-帮助-插件相关-关闭C++下的ClangCodeModel插件

关闭后可正常使用补全等功能。



## 其他





