# Mac OS 9 编程初体验

![00-cover](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/00-cover.png)

## 前言

MPW，即 [Macintosh Programmer's Workshop][1]，是 Classic Mac OS 下的软件开发环境，适用于 System 7.x ，Mac OS 8.x 和 Mac OS 9.x。MPW 中包含了命令行环境 [MPW Shell][2]，68k 和 PowerPC 汇编器，以及 Pascal，C 和 C++ 的编译器。

## MPW Shell

MPW Shell 类似于 UNIX Shell，但命令不同，如 `Files` 即为 `ls`，`Directory` 命令不接收参数类似于 `pwd`，接目标目录即为 `cd some_dir`，另外 MPW Shell 中使用 `:` 作为目录分隔符，而不是 `/`，但注释也同样是 `#`。

例如要进入到 `'Macintosh HD'` 目录下的 `'Desktop Folder'` 中，并查看其中的文件，命令即为（注释后为 UNIX Shell 版本）：


|                 MPW Shell                 |             UNIX Shell             |
| ----------------------------------------- | ---------------------------------- |
| `Directory 'Macintosh HD:Desktop Folder'` | `cd Macintosh\ HD/Desktop\ Folder` |
|                `Directory`                |               `pwd`                |
|                `Files -l`                 |              `ls -l`               |


另外 MPW Shell 中已经执行过的命令可以删除修改，这一点不同于 UNIX Shell，运行命令是在当前一行按 <key>cmd</key> + <key>enter</key> 键。

更详细的内容请参考附录中的资料。

## 用 C 写一个 Hello World

### 创建工程

首先打开 MPW Shell，是这样一个窗口，就是运行上面介绍的 MPW Shell 的地方。

![01-MPW-Shell-Window](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/01-MPW-Shell-Window.jpg)

新建 Project 是在从左上角的 **Project** 选择 **New Project**，就会出现这样一个窗口，可以设置程序的名称和目录。

![02-Create-Project](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/02-Create-Project.jpg)

创建完成后，打开该工程的文件夹，包含一个 `ProjectorDB` 文件，点击打开。

![03-ProjectorDB-File](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/03-ProjectorDB-File.jpg)

ん？怎么打开的还事 MPW Shell （恼）

![04-Open-an-MPW-Shell](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/04-Open-an-MPW-Shell.jpg)

现在得到的项目是一个空项目，没有源码，不像现在的 Xcode 直接给一个模板。

### 写代码

点击左上角的 **File** 选项，创建一个 ~~mian.c~~ `main.c` 文件， 保存在 `ProjectorDB` 文件相同目录下。

![05-Code-Editor](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/05-Code-Editor.jpg)

然后怎么又事 MPW Shell（再度恼）。但注意这个 Shell 上的目录为 `Macintosh HD:Desktop Folder:Hello:main.c`，即刚刚创建的文件。在这个里面就可以愉快地写代码啦（没有提示，有限的高亮）。

```c
#include <stdio.h>

int main() {
    printf("Hello, Macintosh Programmer's Workshop!\n");
    return 0;
}
```

把以上代码写到文件中，保存即可。

### 配置编译命令

现在需要添加一个编译命令，实际上是通过点击选项让 MPW 帮忙构建好 Make 脚本实现编译。

![06-Generate-Compilation-Commands](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/06-Generate-Compilation-Commands.jpg)

配置选项选项的界面如下。

![07-Comfigure-Compilation-Options](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/07-Configure-Compilation-Options.jpg)

简单看一下，Program Type 里的 Application 应该是带 GUI 的程序，而 SIOW App 应该是命令行程序，这里选择 SIOW App。Target 里可以选择两种架构，m68k 和 PowerPC，Fat Binary 即同时包含 m68k 和 PowerPC 两种架构，历史上的 Fat Binary 曾经有 m68k + PowerPC，PowerPC + Intel ，而现在有 Intel + ARM64。

在 Source Files 处选择要编译的源文件，而 Include Search Paths 处是指定搜索头文件的路径，此处没有添加别的头文件，可不设置。这里这要添加刚刚的 `main.c`。

![08-Add-Source-File](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/08-Add-Source-Files.jpg)

配置完成后就生成了一个 Makefile ，如下图

![09-Makefile](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/09-Makefile.jpg)

点击 **Build** 选项中的 **Build** 即可编译，在编译时又会跳出来一个 MPW Shell 窗口（三度恼），这个窗口内会给 build 过程中的信息。

![10-Compiling](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/10-Compiling.jpg)

编译完成后，就在工程目录有了一个 `hello` 可执行文件。

### 运行

点击这个 `hello` 就可以运行啦，会跳出来一个窗口，打印出刚刚的 Hello World。

![11-Hello-World](https://github.com/mizu-bai/Articles-from-Zhihu/blob/main/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C/Mac%20OS%209%20%E7%BC%96%E7%A8%8B%E5%88%9D%E4%BD%93%E9%AA%8C.assets/11-Hello-World.jpg)

至此，达成成就，在 Mac OS 9 下用 C 写了个 Hello World！

## 参考资料

1. Macintosh Programmer's Workshop, https://en.wikipedia.org/wiki/Macintosh_Programmer%27s_Workshop
2. MPW Shell, https://web.archive.org/web/20161021140941/http://www.geek-central.gen.nz/MPW/intro.html

[1]: https://en.wikipedia.org/wiki/Macintosh_Programmer%27s_Workshop
[2]: https://web.archive.org/web/20161021140941/http://www.geek-central.gen.nz/MPW/intro.html
