---
layout: post
title: OpenGL to implement Animation of Solar System
subtitle: Final Project of CS104, Fundamentals of Computer Graphics
date: 2020-12-12
author: Zaki
header-img: img/solar.jpg
catalog: true
tags:
     - OpenGL
     - Computer Graphics
---

> This is the final project of course CS104, Fundamentals of Computer Graphics, FIT, MUST. 


# Introduction

This project mainly illustrates the implementaion of solar system by using OpenGL, The report is divided into two main parts, Part one contains the design of the program, the output, and an explanation of some of the code; Part two is my comments and summary. The purpose of the program is to simulate the orbital diagram of a complete solar system with eight planets, including the rotation of the planets. The focus of the experiment is on how to integrate a complete solar system program from matrix stack, sphere drawing, texture mapping, ADS lighting, etc. using what we learned in class.

The whole program has been successfully complied on <strong>Visual Studio 2017</strong> (Version 15)  Win 32 with <strong>OpenGL</strong> (version 4.3). 

# Design of Solar System

The design of the program is divided into four parts. The first part is the sphere creation (Report 3.2), where we start from designing a sphere, referring to the textbook 6.1, to complete the basic idea of drawing a planetary sphere. The second part is the generation of the solar system. After the sphere creation process, we draw the eight planets of the solar system, including their positions, rotations, and scaling, using a matrix stack, referring mainly to program 4.4. 
the procedure explanation is in report 3.4. The third part is texture mapping (Report 3.3), where we add textures for each planet, referring to chapter5, to make them more realistic. 
In addition, we also added a skybox(Report 3.5) to make the program more complete and beautiful. The last part is lighting (Report 3.6). After the first three parts, the solar system is now taking shape, and we added a light source to the sun in the last part to give it a light/dark contrast. 

# Output 

Here is a screenshot of output, want to see the complete program and Report? check my <a href="https://github.com/Zaki-Mao/OpenGL-to-implement-Solar-System">Github</a>.

![](https://tva1.sinaimg.cn/large/0081Kckwgy1glnijrzkjtj30l80bugnw.jpg)

# Github Address

If you want to check complete program, click here. <a href="https://github.com/Zaki-Mao/OpenGL-to-implement-Solar-System">Solar System</a>


