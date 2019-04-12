# chap0x04 shell脚本编程基础
## 实验内容
* 任务一：用bash编写一个图片批处理脚本，实现以下功能： 
    * 支持命令行参数方式使用不同功能
    * 支持对指定目录下所有支持格式的图片文件进行批处理
    * 支持以下常见图片批处理功能的单独使用或组合使用
    * 支持对jpeg格式图片进行图片质量压缩
    * 支持对jpeg/png/svg格式图片在保持原始宽高比的前提下压缩分辨率
    * 支持对图片批量添加自定义文本水印
    * 支持批量重命名（统一添加文件名前缀或后缀，不影响原始文件扩展名）
    * 支持将png/svg图片统一转换为jpg格式图片

* 任务二：用bash编写一个文本批处理脚本，对以下附件分别进行批量处理完成相应的数据统计任务： 
    * [2014世界杯运动员数据](http://sec.cuc.edu.cn/huangwei/course/LinuxSysAdmin/exp/chap0x04/worldcupplayerinfo.tsv)
        * 统计不同年龄区间范围（20岁以下、[20-30]、30岁以上）的球员**数量**、**百分比**
        * 统计不同场上位置的球员**数量**、**百分比**
        * 名字最长的球员是谁？名字最短的球员是谁？
        * 年龄最大的球员是谁？年龄最小的球员是谁？
   *  [Web服务器访问日志](http://sec.cuc.edu.cn/huangwei/course/LinuxSysAdmin/exp/chap0x04/web_log.tsv.7z)
        * 统计访问来源主机TOP 100和分别对应出现的总次数
        * 统计访问来源主机TOP 100 IP和分别对应出现的总次数
        * 统计最频繁被访问的URL TOP 100
        * 统计不同响应状态码的出现次数和对应百分比
        * 分别统计不同4XX状态码对应的TOP 10 URL和对应出现的总次数
        * 给定URL输出TOP 100访问来源主机


## 实验环境
* 虚拟机环境：Ubuntu 18.04 Server 64bit
* 宿主机使用git bash远程登录虚拟机
* bash版本：`version 4.4.19(1)-release (x86_64-pc-linux-gnu)`

## 实验代码及统计数据结果
* 任务一
    * [代码 - image.sh](image.sh)
        * [测试图片](images)
* 任务二：
    * [代码 - player.sh](player.sh)
        * [世界杯运动员统计数据](log/player_output.log)
    * [代码 - weblog.sh](weblog.sh)
        * web服务器日志统计数据
            * [host_top_100.log](log/host_top_100.log)
            * [IP_top_100.log](log/IP_top_100.log)
            * [URL_top_100.log](log/URL_top_100.log)
            * [status_code.log](log/status_code.log)
            * [4xx_top10_url.log](log/4xx_top10_url.log)
            * [specified_URL_host.log](log/specified_URL_host.log)

    ```bash
    # 脚本运行命令
    # image.sh: 调用全部参数（除去-h）
    bash image.sh -i images/ -q 50% -r 90 -w cuc -p prefix -s suffix -c
    
    # player.sh：调用全部参数（除去-h）
    bash player.sh -ar -p -ac -n

    # weblog.sh: -o可替换为-i/-u/-s/-u4/-uh <URL>，详见代码
    bash weblog.sh -o >>output.log
    ```

## 实验问题
1. 单引号与双引号

    在类似`oldst_name_column=$(awk -F '\t' '{if($6=='${max_age}') {print $9}}' "$1");`这样一条命令里，awk脚本中的赋值语句用单引号包围`max_age`变量时，`shellcheck`提示`SC2086: Double quote to prevent globbing and word splitting.`。
    
    解决：将语句改为`if($6=='"${max_age}"'`即可，参考[这里](http://bbs.chinaunix.net/forum.php?mod=viewthread&tid=218853&page=4#pid1511745)。
2. awk中的內建变量NF
    
    想用`NF>1`这个条件来忽略待处理文件的第一行，没成功，还是用了`sed '1d'`。

3. svg格式图片处理

    svg图片经质量压缩、分辨率压缩、添加水印后，用IE 10打开，看起来损坏了，且转化成jpeg格式时有的会失真，不清楚是找的svg图源问题还是程序的问题，暂未解决。
    
## 参考文献
* [sec.cuc.edu.cn/chap0x04](http://sec.cuc.edu.cn/huangwei/course/LinuxSysAdmin/chap0x04.md.html#/shell)
* [2015-linux-public-JuliBeacon](https://github.com/CUCCS/2015-linux-public-JuliBeacon/blob/524f60f68f2315623231db132df03313ab3df72a/实验%204/实验4.md)
* [3c1rp4c/TravisBasedOJ](https://github.com/3c1rp4c/TravisBasedOJ/tree/master/ex4)
* [2017-1/TJY](https://github.com/CUCCS/linux/tree/master/2017-1/TJY/bash)
* [shift](https://unix.stackexchange.com/questions/174566/what-is-the-purpose-of-using-shift-in-shell-scripts)
* [How to Convert Images Using Linux](https://www.lifewire.com/convert-linux-command-unix-command-4097060)
* [Loop over file names from 'find'](https://stackoverflow.com/questions/9391003/loop-over-file-names-from-find)
* [linux find -regex 使用正则表达式](http://www.cnblogs.com/jiangzhaowei/p/5451173.html)
* [Linux awk 命令](http://www.runoob.com/linux/linux-comm-awk.html)
* [Linux sed命令](http://www.runoob.com/linux/linux-comm-sed.html)
* [Linux uniq 命令](http://www.runoob.com/linux/linux-comm-uniq.html)
* [shell 十三问](http://bbs.chinaunix.net/thread-218853-1-1.html)
* [grep和egrep正则表达式 ](https://www.cnblogs.com/python-gm/p/6940756.html)
    
    
