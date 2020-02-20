---
layout: post
title: 更新：TXS“编译失败”及pdf无法生成的问题
subtitle: Update："Build&view" compile failed on TXS and pdf file save failed.
date: 2020-02-20
author: Zaki
header-img: img/home-bg-o.jpg
catalog: true
tags:
     - LaTeX
     - Mac
     - 效率
     - 终端
     - Debug
---




> TeXStudio不能生成pdf文件格式以及编译失败等问题的跟踪记录。（Update：Solved)

# 关于“编译失败”

<strong>Environment</strong>

TeXstudio: 2.12.14 (git 2.12.14)

Qt: 5.11.2

OS: MacOS

TeX distribution: texlive

<strong>TeXStudio编译失败的问题</strong>

问题追踪：我遇到这个问题是在用TeXStudio完成一份文档后，不知是TXS哪里抽风了给了我一个突如其来的“编译失败”，具体的error提示如下

#### warning


      "Could not start Build & View:PdfLaTeX:
      pdflatex -synctex=1 -interaction=nonstopmode "my pdf file ".tex."


# 问题解决


后来我便在github中<strong>TeXStudio-org/TeXStudio</strong>里的<a href="https://github.com/texstudio-org/texstudio/issues">issue</a>中寻求帮助。

后来得到其中一位仁兄这样的建议

![](https://tva1.sinaimg.cn/large/0082zybply1gc33wjcauoj30lu08bgmr.jpg)

也就是在mac的终端里敲如下指令看是否编译成功

#### 指令

     pdflatex -synctex=1 -interaction=nonstopmode <name of your tex file>
     
如不成功，在TeXStudio中，按照<strong>option->configure</strong>的顺序点击。

依次确保以下信息被勾选

默认编译器： XeLateX

默认认查看器 ： PDf查看器

PD查看器内置： PDF查看器(内嵌)


# 生成PDF无法打开的情况

在TeXStudio成功编译并且生成的pdf文件，在外部无法打开。

#### Error如下


      “无法打开。它可能已损坏，或者可能使用了“预览”无法识别的文件格式”
      

# 问题解决


对于文档损坏或应用无法打开的情况，按“标准解决方案”，应该是

（MacOS）在<strong>系统偏好设置-安全性及隐私-允许从以下位置下载的应用</strong>勾选<strong>“任何来源”</strong>

MacOS 10.12及以上用户可能没有这个选项。在终端敲击以下指令输入密码回车即可。

#### 指令

      sudo spctl --master-disable
      
      
而即便我在TexStudio切换到了tools-command-PDFLaTeX，可最终还是碰到了一点问题。结果就是我发现确保了一切工作之后还是无法生成。

最终，我发现既然不用编译后不用按常规那样”生成PDF文件“，在预览界面的上面最左边，有一个小红书一样的按钮

![](https://tva1.sinaimg.cn/large/0082zybply1gc34o7yo0dj30c702lq36.jpg)

这个是tex文档pdf的外部查看器，所以直接点击它并且点击你的文件名，就可以将它生成在你指定的位置了。

pdf文件可以成功生成了，但是对于为什么走“常规操作”反而生成不了的问题还是没有找到一个答案，希望以后可以解决。

     
