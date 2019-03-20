# chap0x02 From GUI to CLI
## 实验内容

* 在asciinema注册一个账号，并在本地安装配置好asciinema
* 确保本地已经完成asciinema auth，并在asciinema成功关联了本地账号和在线账号
* 上传本人亲自动手完成的vimtutor操作全程录像
* 在自己的github仓库上新建markdown格式纯文本文件附上asciinema的分享URL
* vimtutor完成后的自查清单

## 实验准备
* 虚拟机环境：Ubuntu 18.04 Server 64bit
* 宿主机使用git bash远程登录虚拟机
* asciinema
    ```bash
    # 更新缓存
    sudo apt update

    # 安装asciinema
    sudo apt install asciinema

    # 关联本地账号和在线账号
    asciinema auth

    # asciinema开始录屏
    asciinema rec

    # 结束录屏
    # Ctrl-D也可
    exit

    # 将录屏上传到asciinema.org
    <ENTER>

    # 保存到本地
    <CTRL-C>

    # 本地上传
    asciinema upload xxx.cast
    ```

## vimtutor操作录像
### lesson1
[![asciicast](https://asciinema.org/a/djJaBngQgWHmwdMc3WkjPhxTo.svg)](https://asciinema.org/a/djJaBngQgWHmwdMc3WkjPhxTo)
### lesson2
[![asciicast](https://asciinema.org/a/AR26YhPCwH1JKwLChFgb5H1eQ.svg)](https://asciinema.org/a/AR26YhPCwH1JKwLChFgb5H1eQ)
### lesson3
[![asciicast](https://asciinema.org/a/ypdNeJfsm0Wy3ebWWNwts2rde.svg)](https://asciinema.org/a/ypdNeJfsm0Wy3ebWWNwts2rde)
### lesson4
[![asciicast](https://asciinema.org/a/sbHxkQpUvkhdHwlexDuz90rsz.svg)](https://asciinema.org/a/sbHxkQpUvkhdHwlexDuz90rsz)
### lesson5
[![asciicast](https://asciinema.org/a/Acvrt3ZDqo1eIg9h4NRbOxmFl.svg)](https://asciinema.org/a/Acvrt3ZDqo1eIg9h4NRbOxmFl)
### lesson6
[![asciicast](https://asciinema.org/a/iyRiwWE19KQgbP5hN8PXdBUXD.svg)](https://asciinema.org/a/iyRiwWE19KQgbP5hN8PXdBUXD)
### lesson7
[![asciicast](https://asciinema.org/a/Fl9RjGkXTz540iUXEI5yGifHP.svg)](https://asciinema.org/a/Fl9RjGkXTz540iUXEI5yGifHP)

## 自查清单

1. 你了解vim有哪几种工作模式？
    1. 插入模式 Insert
    2. 普通模式 Normal
    3. 可视模式 Visual
2. Normal模式下，从当前行开始，一次向下移动光标10行的操作方法？如何快速移动到文件开始行和结束行？如何快速跳转到文件中的第N行？
    * 一次向下移动光标10行：`10j`
    * 快速移动到文件开始行：`gg`
    * 快速移动到文件结束行：`G`
    * 快速跳转到文件中的第N行：`NG`或`Ngg`

3. Normal模式下，如何删除单个字符、单个单词、从当前光标位置一直删除到行尾、单行、当前行开始向下数N行？
    * 删除单个字符：`x`
    * 删除单个单词：`dw`
    * 从当前光标位置一直删除到行尾：`d$`
    * 从当前光标位置一直删除到单行：`dd`
    * 从当前光标位置一直删除到当前行开始向下数N行：`dNd`
4. 如何在vim中快速插入N个空行？如何在vim中快速输入80个-？
    * 快速插入N个空行：Insert模式下，`No`（光标所在行下方插入）或`NO`（上方插入）
    * 快速输入80个-：Insert模式下，`80i-`
5. 如何撤销最近一次编辑操作？如何重做最近一次被撤销的操作？
    * 撤销最近一次编辑操作：`u`
    * 重做最近一次被撤销的操作：`CTRL-R`
6. vim中如何实现剪切粘贴单个字符？单个单词？单行？如何实现相似的复制粘贴操作呢？
    * 剪切粘贴单个字符：`dx`-`p`
    * 剪切粘贴单个单词：`dw`-`p`
    * 剪切粘贴单行：`dd`-`p`
    * 相似的复制粘贴操作：`v`-方向键选中指定部分-`y`(复制)-`p`(粘贴)
7. 为了编辑一段文本你能想到哪几种操作方式（按键序列）？
    * `i`/`o`/`O` 插入
    * `a` 添加
    * `R` 替换
    * `x`/`dw`/`dd`/`d$` 删除
    * `v`-`y`-`p` 复制粘贴
8. 查看当前正在编辑的文件名的方法？查看当前光标所在行的行号的方法？
    * 均为`CTRL-G`
9. 在文件中进行关键词搜索你会哪些方法？如何设置忽略大小写的情况下进行匹配搜索？如何将匹配的搜索结果进行高亮显示？如何对匹配到的关键词进行批量替换？
    * 文件中进行关键词搜索：正向搜索：`/xxx`；反向搜索：`?xxx`，再按`<ENTER>`
    * 设置忽略大小写的情况下进行匹配搜索：`:set ic`
    * 将匹配的搜索结果进行高亮显示：`:set hls is`
    * 对匹配到的关键词进行批量替换：`:%s/old/new/g`
10. 在文件中最近编辑过的位置来回快速跳转的方法？
    * `CTRL-O`/`CTRL-I`
11. 如何把光标定位到各种括号的匹配项？例如：找到(, [, or {对应匹配的),], or }
    * 光标置于待定位括号，按`%`
12. 在不退出vim的情况下执行一个外部程序的方法？
    * `:!<外部程序>`
13. 如何使用vim的内置帮助系统来查询一个内置默认快捷键的使用方法？如何在两个不同的分屏窗口中移动光标？
    * 查询一个内置默认快捷键的使用方法：`:help <快捷键>`
    * 在两个不同的分屏窗口中移动光标：`CTRL-W` 翻屏