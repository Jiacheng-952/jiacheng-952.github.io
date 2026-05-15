---
title: 如何在VS Code 导入万能头`#include <bits/stdc++.h>` ？
date: 2026-05-02 20:00:00 +0800
categories: [C, MinGW]
tags: [C, 万能头,环境变量,MinGW]
author: Jiacheng  # 可选，如果想指定不同作者
math: true            # 可选，如果文章里有数学公式，设为 true
mermaid: true         # 可选，如果文章里有流程图，设为 true
pin: false            # 可选，设为 true 可以把文章置顶
---

> `#include <bits/stdc++.h>` 找不到，这是 GCC/MinGW 编译器专属的万能头文件，微软官方的 MSVC 编译器不支持这个头文件，所以我们需要配置 MinGW 编译器，以下是保姆级教程。

### 1. 下载正确的预编译版

打开这个地址下载官方预编译包：[mingw-w64-v8.1.0-release-posix-seh-rt_v6-rev0.7z](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/seh/x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z/download)
- `x86_64`：支持 64 位系统（现在电脑基本都是 64 位）
- `posix`：线程模型，对 C++ 标准支持更好
- `seh`：异常处理模型，兼容性最好

![打开MinGW网站等待大约5s自动下载](/assets/img/post/2026-5-2-all-need-head/MinGW_website.png)

---

### 2. 解压到固定路径

把下载好的 `.7z` 压缩包解压到一个**没有中文、没有空格**的路径，比如：

```bash
C:\mingw64
```

解压后，你会看到里面有 `bin`、`include`、`lib` 这些文件夹，就对了！
![MinGW64文件目录](/assets/img/post/2026-5-2-all-need-head/mingw64.png "MinGW64文件目录")

### 3. 配置系统环境变量（关键步骤）

1. 右键「此电脑」→「属性」→「高级系统设置」→「环境变量」
2. 在「系统变量」里找到 `Path`，双击打开
3. 点击「新建」，添加你的 MinGW `bin` 目录路径，比如：

```plaintext
    C:\mingw64\bin
```

4. 一路点「确定」保存所有设置

不要在系统变量中添加变量"MinGW"(像图中第二行，这是错误示例❌)，而是在这里找到"path"，双击之后修改。
![系统变量窗口](/assets/img/post/2026-5-2-all-need-head/system_variables.png "系统变量")

之后会弹出"编辑环境变量"的窗口，之后新建添加新的路径。操作完之后一直点确定保存设置。
![编辑环境变量窗口](/assets/img/post/2026-5-2-all-need-head/edit_environment_variables.png "编辑环境变量窗口")


### 4. 验证安装是否成功

按 `Win + R` 输入 `cmd` 打开命令提示符，输入：

```bash
gcc -v
```

如果输出一大串版本信息（比如 `gcc version 8.1.0`），就说明安装成功了！

![检查gcc版本](/assets/img/post/2026-5-2-all-need-head/gcc_version.png "cmd窗口")

### 5. 配置 VSCode 让它识别 MinGW

打开你的 C++ 代码文件，按 `Ctrl + Shift + P`，输入：

```plaintext
C/C++: Edit Configurations (JSON)
```

打开 `c_cpp_properties.json` 文件，修改里面的配置：

```json
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**",
                "C:/mingw64/include/**",
                "C:/mingw64/x86_64-w64-mingw32/include/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "compilerPath": "C:/mingw64/bin/gcc.exe",
            "cStandard": "c17",
            "cppStandard": "c++17",
            "intelliSenseMode": "windows-gcc-x64"
        }
    ],
    "version": 4
}
```

保存后，你之前的 `bits/stdc++.h` 报错就会消失了！
![修改c_cpp_properties.json文件对应的字段](/assets/img/post/2026-5-2-all-need-head/c_cpp_properties.png "修改c_cpp_properties.json文件对应的字段")

---

### 6. 配置 VSCode 编译任务（可选，推荐）

再按 `Ctrl + Shift + P`，输入：

```plaintext
Tasks: Configure Default Build Task
```

选择 `C/C++: g++.exe build active file`，VSCode 会自动生成 `tasks.json` 文件，之后按 `Ctrl + Shift + B` 就能一键编译运行你的 C++ 代码了。
