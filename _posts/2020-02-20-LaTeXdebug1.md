---
layout: post
title: Debug:LaTeX Error "there's no line here to end"
subtitle: Updating the latest solutions[TexStudio git 2.12.14]
date: 2020-02-20
author: Zaki
header-img: img/home-bg-o.jpg
catalog: true
tags:
     - LaTeX
     - Mac
     - Debug
     - 效率
---

>自己在使用LaTeX的过程发现的报错信息以及尝试的解决办法都会在此博客做一个跟踪记录。

# 问题发现

<strong>Environment</strong>

TeXstudio: 2.12.14 (git 2.12.14)</p>
Qt: 5.11.2</p>
OS: MacOS</p>
TeX distribution: texlive


####  Error
      
        there's no line here to end
        
![](https://tva1.sinaimg.cn/large/0082zybply1gc32qhg0p9j30du00p3yj.jpg)

报错位置是当我在\paragraph{...}后面想要使后面内容换行到下一行加了"\\"导致。

![](https://tva1.sinaimg.cn/large/0082zybply1gc32pw1ufej30s303omxt.jpg)

同等类型的错误包括不限于：
####   
     
      \centerline{ ... } \\
      \end{...} \\
      \section{..} \\
      
 # 问题解决
 
 在上述情形下使用\\一般是为了插入一个空行。因此可以输入一个空格(\quad), 此时光标已经到了下一行，然后再终止该行
 
 #### 
      \quad\\

 
