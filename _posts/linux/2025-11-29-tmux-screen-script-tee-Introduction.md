---
title: "tmux/screen/screen/tee介绍"
categories:
  - linux
tags:
  - tmux
  - screen
  - script
  - tee

toc: true
---

## tmux

tmux 是一个终端复用器：它允许创建、访问和控制多个终端，所有这些都可以在单个屏幕上进行。tmux 可以从屏幕中分离出来，在后台继续运行，稍后可以重新连接。

* tmux(terminal multiplexer): <https://github.com/tmux/tmux>
* tmux: <https://www.man7.org/linux/man-pages/man1/tmux.1.html>
* Tmux 使用教程: <https://www.ruanyifeng.com/blog/2019/10/tmux.html>

## screen

会话恢复，多窗口，会话共享，与tmux功能类似，兼容一些老系统，新系统上用tmux的比较多。

* Screen: <https://www.gnu.org/software/screen/>

## Byobu

Byobu 是一个功能强大的开源文本终端窗口管理器，它基于 tmux 或 GNU Screen 提供了一个增强的用户体验。

* Byobu: <https://www.byobu.org/>

## script

记录所有终端活动，包括输入和输出（所以记录的日志中包含很多特殊字符，不方便直接查看），可以通过`scriptreplay`工具进行回放。

* script — Linux manual page: <https://www.man7.org/linux/man-pages/man1/script.1.html>
* script command in Linux with Examples: <https://www.geeksforgeeks.org/linux-unix/script-command-in-linux-with-examples/>

## tee

从标准输入中获取数据然后同时写到标准输出和文件。

* tee — Linux manual page: <https://www.man7.org/linux/man-pages/man1/tee.1.html>
