---
layout: post
title: Vim常用命令
category: blog
catalog: yes
description: 归纳，方便自查
tags:
   - IT
---

## 1 切换输入模式

命令模式下

|a | (小写)光标之后进行插入|
|A | (大写)光标所在行尾进行插入|
|i | (小写)光标前开始进行插入|
|I | (大写)光标所在行首进行插入|
|o | (小写)光标所在行后新插入一空行进行插入|
|O | (大写)光标所在行前新插入一空行进行插入|

## 2 保存文件

命令模式下

|\:w |(小写)保存文件|
|​\:wq |(小写)保存并退出vim|
|\:w 文件名1 |将文件另存为文件名1|
|\:ZZ |(大写)保存文件并退出,相当于:wq|
|\:wq! |(小写)文件所有者强制保存只读文件,如果不是文件所有者进行此操作,不能成功|
|\:q! | 退出不保存文件|

## 3 复制

命令模式下

yy或 Y | 复制光标所在整行
y^ | 复制到光标所在行行首,不包括光标位置字符
y$ | 复制到光标所在行行尾,包括光标位置字符
yw | 复制一个单词,光标必须在单词首部
yG | 复制到文件尾
y1G | 复制到文件首
nyy | 复制光标所在行开始的n行

## 4 粘贴

命令模式下

p | (小写)粘贴到光标后
P | (大写)粘贴到光标前

## 5 删除

命令模式下

x | (小写)删除光标前一个字符
X | (大写)删除光标后一个字符
dd | (小写)删除光标所在整行
dw | (小写)删除光标所在处一个单词
dG | 删除光标所在整行到文件尾
dgg | 删除光标所在整行到文件首
D | (大写)删除到行尾,包含光标处的字符
d$ | 与D效果相同
d0 | 删除到行首，不包含光标处的字符
d^ | 与d0效果相同
:n1,n2d | 命令模式下，删除n1-n2行

## 6 撤销

命令模式下

u | (小写)无限次保存前撤销(大概500多次)
ctrl+r | redo

## 7 字符替换

命令模式下

r | (小写)替换光标所在处一个字符
R | (大写)开始替换,直到按ESC键退出替换,相当于按下键盘上到insert键
cc | (小写)取代光标所在整行
S | (大写)与ss(小写)效果相同
C | (大写)取代到行尾,包括光标处字符
c0 | (小写,数字0)取代到行首,不包括光标处字符
c^ | (小写)与c0(小写,数字0)效果相同

## 8 字符串查找和替换

命令模式下

| /string | 从光标处开始向下开始查找字符串string | |
| /查找模式下 | 按n(小写)查找下一个,按N(大写)查找上一个|
| ?string | 从光标处开始向上开始查找字符从string|
| ?查找模式下 | 按n(小写)查找上一个,按N(大写)查找下一个|
| * | 向下完整匹配光标下的单词|
| # | 向上完整匹配光标下的单词|
| g* | 向下部分匹配光标下的单词|
| g# | 向上部分匹配光标下到单词|

命令模式下

:set ic | 查找时,忽略大小写
:set noic | 取消查找时忽略大小写
:f string | (小写f与string有空格)搜索一行中匹配到的string
:%s/old/new/g | 全文将old替换为new,不提示
:%s/old/new/c | 全文将old替换为new,提示是否替换
:n1,n2s/old/new/g | n1-n2行中,将old替换为new,不提示
:n1,n2s/old/new/c | n1-n2行中,将old替换为new,提示是否替换

在替换文本old或new中有/字符时,需要用\进行转义 |

## 9 显示行号

命令模式下

:set nu(mber) | 显示行号
:set nonu | 取消显示行号
:set nu! | 取消显示行号

## 10 简单排版

命令模式下

:ce(nter) | 居中显示光标所在行
:ri(ght) | 靠右显示光标所在行
:le(ft) | 靠左显示光标所在行

命令模式下

J | 将光标所在下一行合并到光标所在行
>> | 光标所在行增加缩进(一个tab)
<< | 光标所在行减少缩进(一个tab)
n>> | 光标所在行开始的n行增加缩进
n<< | 光标所在行开始的n行减少缩进

## 11 光标移动方式

命令模式下

H | (大写,Head)移动到屏幕顶第一个非空白字符
M | (大写,Mid)移动到屏幕中间第一个非空白字符
L | (大写,Last)移动到屏幕底部第一个非空白字符
( | (左小括号)移动到上一个句子首
) | (右小括号)移动到下一个句子首
{ | (左大括号)移动到上一个段落首
} | (右大括号)移动到下一个段落首
% | 光标跳转到匹配到括号处,支持{}()
[[ | 光标跳转到代码块开头即{处,要求{独占一行
gD | 光标跳转到局部变量定义处
'' | (两个单引号)光标跳转到上次停靠处
h | (小写)光标左移一个字符,相当于左方向键
l | (小写)光标右移一个字符,相当于右方向键
k | (小写)光标垂直上移一行,相当于上方向键
j | (小写)光标垂直下移一行,相当于下方向键
ctrl+f | (forword)向下整页翻页
ctrl+b | (backward)向上整页翻页
ctrl+u | (up)向上翻半页
ctrl+d | (down)向下翻半页
zz | (小写)让光标所在行居于屏幕中央
zt | (小写)让光标所在行居于屏幕最顶部
zb | (小写)让光标所在行居于屏幕底部

编辑模式下

:n | 指定移动到第n行

## 12 数字前缀与重复

命令模式下

将数字加在命令前,标示该命令处理几次 | 如5dd标示执行5次dd(删除光标所在整行)操作。
\. | 为命令重复命令，按下一次执行一次上一次执行过的命令。

## 13 vim技巧

**技巧1** 导入文件或shell命令执行结果

编辑模式下

:r 文件名1 | 将文件1内容引入到本文件中
:!shell命令 | 在vim中执行shell命令,执行完后按回车会到vim界面
**:r !shell命令** | (r与!之间有空格)将shell命令执行的结果导入到本文件中

**技巧2** 自定义快捷键操作

编辑模式下

:map ^x 命令 | (map与^之间、x与命令之间有空格,此处到^并非键盘上的^,而是按下ctrl+v出现到快捷键,表示ctrl键,后面到x为任意字母)按下ctrl+x后会执行对应到命令

例:

:map ^p I#<ESC> 当按下ctrl+p快捷组合键时,在光标所在行行首添加一个#号,并回到命令模式

**技巧3** 连续行注释

编辑模式下

:n1,n2/^/#/g | (#号为注释符号,在shell中注释符号为#,C++中为//)
:n1,n2/^/\/\//g | C++源文件多行连续注释

**技巧4** 替换

| :ab string1 string2 | 在vim中输入string1按空格或回车后,string1会自动替换为string2|
| :unab string1 | 取消string1的替换|
