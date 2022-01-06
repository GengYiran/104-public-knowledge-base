---
title: 构建基本脚本
type: operations
---

[toc]
# 11 构建基本脚本
前置：
- [[6-env]]
- [[7-permissions]]
- [[10-editting]]

本篇是[[0-metadata]]读书笔记第11章部分。
我们大致了解 #Linux 的 #shell 脚本的编写方式，方便做 #自动化
## 11.1 使用多个命令
简单的顺序结构（连续使用多个命令）：`<命令>; <命令>`
一行不能超过255个字符
如果要换行：比如这个片段
```
echo "
channels:
 - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/peterjc123/
custom_channels:
 pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
" >> ~/.condarc; \
apt update; \
apt-get install -y vim curl openssh-server \
ffmpeg;
```
可以看到一些典型的换行的使用方式
- 引号未配对，则会等待配对
- `; \`表示命令写完了，换行，下一条命令
- `\`表示命令没写完。这样可以写一行特别长的命令。比如`apt-get install <一大堆包名>`
## 11.2 创建shell脚本文件
用[[10-editting]]创建文本文件，将命令（逐行）输入到文件中
第一行`#!`指定要使用的shell，而其它`#`用于注释
写好`.sh`脚本文件，怎么运行？`./<.sh文件名>`表示当前目录下的（一般这么用）。而不加的话自动在环境变量`PATH`里找（往往找不到）
为了可以运行，还需要参考[[7-permissions]]加权限
## 11.3 显示消息
- 一般字符串直接`echo`
- 只有一种引号（比如单引号）就用另一种括起来（比如双引号）
  - 末尾需要空格，那也需要引号括起来
- `-n`参数可以不换行
  - 应用：`echo -n 'date: '; date`
## 11.4 使用变量
- `set`：显示所有环境变量（参考[[6-env]]）
- `$<变量名>`：使用变量（可以是环境变量）
  - `${<变量名>}`很常见，更明显标出变量名
- 双引号中的`$`仍表示变量。`\$`才是原始的符号`$`
  - 单引号中的`$`就是原始符号
- 区分大小写，数字字母下划线组成，长度不超过20
- 自己的变量？
  - 定义变量不需要`$`（取用需要）
  - 等号赋值
  - 等号前后无空格
  - 脚本运行结束时自动删除
- 
