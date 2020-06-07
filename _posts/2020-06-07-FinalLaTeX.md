---
layout: post
title: 肝期末报告中LaTeX使用的总结
subtitle: Summary of LaTeX use in the final report
date: 2020-06-07
author: Zaki
header-img: img/home-bg-o.jpg
catalog: true
tags:
     - LaTeX
     - 效率
     - Report
    
---




> 今天终于也是正式了结束了大二的最后的一个学期，在赶着ddl刚刚递交了最后一份期末报告后，也发现这学期过的也是转瞬即逝。已经好长时间没有写博客了，在这里，就随便记录下自己使用LaTeX写报告的总结的一些东西。以。

# LaTeX图片居中的问题

在写第一份泊松分布的概率报告时，我便遇到了这样的问题，如果我想要在LaTeX的文本中将插入的图片等居中，用了\centering命令之后，图片是居中了，但是底下的所有文字
也跟着居中了，这就很烦。但最终，我还是找到了只将图片居中，文本保持原样的代码，如下


####      

          \begin{figure}[h]
	        \centering \includegraphics[scale=0.2]{picture.pdf}
          \end{figure}
          
          
 # LaTeX插入图片的方法
 
 
而对于图片的插入，我所使用的编辑器是Texstudio，我所使用的方法如下：

首先，我们要将要插入图片转换成pdf格式，转换pdf图片的在线网站有很多种，这儿就不做推荐。

之后，我们要找到你在写的这份文本的.tex文件所在的文件夹。

把pdf图片丢在里面，使用如上代码，把pdf图片的名称填到上面picture那个位置，形式如：名称.pdf。

然后，就大功告成了！


# LaTeX制作封面


同时，对于一份实验报告或者是论文报告，我们通常会在开篇制作出它的封面和目录，这对于laTeX来说制作不要太爽，我所使用的代码如下，该代码同时包含了所需的学校，
课程编号和名称，到学校的logo以及你的个人信息，很方便就可以制作出来。对于一份常用报告所需要的宏包，这里也都加了上去，以及更新了目录的自动插入。


以下是我所使用的代码


####  

      \documentclass[10pt,english, openany]{book}。%book类型

      %%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Loading packages that alter the style
      \usepackage[]{graphicx}
      \usepackage[]{color}
      \usepackage{alltt}
      \usepackage[T1]{fontenc}
      \usepackage[utf8]{inputenc}
      \setcounter{secnumdepth}{3}
      \setcounter{tocdepth}{3}
      \setlength{\parskip}{\smallskipamount}
      \setlength{\parindent}{0pt}
      \usepackage{enumerate}


      % Set page margins
      \usepackage[top=100pt,bottom=100pt,left=68pt,right=66pt]{geometry}

      % Package used for placeholder text
      \usepackage{lipsum}

      % Prevents LaTeX from filling out a page to the bottom
      \raggedbottom

      % Adding both languages
      \usepackage[english, italian]{babel}

      % All page numbers positioned at the bottom of the page
      \usepackage{fancyhdr}
      \fancyhf{} % clear all header and footers
      \fancyfoot[C]{\thepage}
      \renewcommand{\headrulewidth}{0pt} % remove the header rule
      \pagestyle{fancy}

      % Changes the style of chapter headings
      \usepackage{titlesec}
      \titleformat{\chapter}
      {\normalfont\LARGE\bfseries}{\thechapter.}{1em}{}
      % Change distance between chapter header and text
      \titlespacing{\chapter}{0pt}{50pt}{2\baselineskip}

      % Adds table captions above the table per default
      \usepackage{float}
      \floatstyle{plaintop}
      \restylefloat{table}

      % Adds space between caption and table
      \usepackage[tableposition=top]{caption}

      % Adds hyperlinks to references and ToC
      \usepackage{hyperref}
      \hypersetup{hidelinks,linkcolor = black} % Changes the link color to black and hides the hideous red border that usually is created

      % If multiple images are to be added, a folder (path) with all the images can be added here 
      \graphicspath{ {Figures/} }

      % Separates the first part of the report/thesis in Roman numerals
      \frontmatter
      \makeatletter %使\section中的内容左对齐
      \renewcommand{\section}{\@startsection{section}{1}{0mm}
     	{-\baselineskip}{0.5\baselineskip}{\bf\leftline}}
      \makeatother
      \usepackage{indentfirst}
      \setlength{\parindent}{2em}
      %%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Starts the document
      \begin{document}

     %%% Selects the language to be used for the first couple of pages
     \selectlanguage{english}

      %%%%% Adds the title page
     \begin{titlepage}
	   \clearpage\thispagestyle{empty}
	   \centering
	   \vspace{1cm}

	    % Titles
    	% Information about the University
	    {\normalsize Macau University of Science and Technology\\ %学校名称
	    CE001  \\%课程编号
	   	Electric Circuits Analysis\par}%课程名称
	  	\vspace{3cm}
	    {\Huge \textbf{Vertification of Frequency Response of a Linear System}} \\
	    %\vspace{1cm}
	    %{\large \textbf{xxxxx} \par}
	    \vspace{4cm}
	    {\normalsize Li Hua \\ %姓名
	    % \\ specifies a new line
	             18098531-i0xx-00xx\\ %学号
	             D1\par}%班级编号
	    \vspace{5cm}
    
      \centering \includegraphics[scale=0.1]{logo.pdf}%logo
   
      \vspace{0.5cm}
		
	   % Set the date
	  {\normalsize 29-05-2020 \par}%日期
	
	   \pagebreak

    \end{titlepage}

     % Adds a table of contents
     \tableofcontents{}%目录

     %Text body starts here!
     \mainmatter
     %正文部分在这，可使用\chapter{title}以章节开始
     \end{document}
     
# LaTeX特殊字符的输入

想要输入诸如%,$等特殊字符，在这些字符前面加 \ 即可。





