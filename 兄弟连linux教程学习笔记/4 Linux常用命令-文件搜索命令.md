# 一 文件搜索命令```find```

## 1.1 命令简介

- 命令名称：find
- 命令所在路径：/bin/find
- 执行权限：所有用户
- 语法：```find [搜索范围] [匹配条件]```
- 功能描述：文件搜索

## 1.2 匹配条件

- ```find /etc -name init```：在/etc目录中查找文件init，不包括文件名包含init的文件；
  - ```find /etc -name *init*```：*为通配符，匹配任意字符，查找文件名中包含init的文件；
  - ``find /etc -name init???``：？用于匹配单个字符；
  - ``find /etc -iname init``：不区分大小写
- ``find / -size +204800``：在根目录下查找大于100MB的文件。数字单位为数据块，Linux中一个数据块的大小为0.5K，即512字节。
  - -n 大于	-n 小于	n 等于
  - ``find /etc -size +163840 -a -size -204800``：在/etc下查找大于80MB小于100MB的文件。-a表示and，即两个条件同时满足；-o表示or，两个条件满足任意一个即可。
- ``find /home -user shenchao``：在根目录下查找所有者为shenchao的文件
  - -group 根据所属组查找
- ``find /etc -cmin -5``：在/etc下查找5min内被修改过属性的文件和目录
  - -amin 访问时间
  - -cmin 文件属性
  - -mmin 文件内容
- ``find /etc -name inittab -exec ls -l {} \;``：在/etc下查找inittab文件并显示其详细信息
  - ``-exec/-ok 命令 {} \;``表示对搜索结果执行操作，“{}”表示find查找的结果，“\”为转义字符，“；”表示结束。使用-ok将对执行操作进行确认，可用于查找删除文件。

- ``find /etc -name init* -a -type f``：在/etc文件夹中查找名称以init开头的文件类型文件
  - f 文件 	d 目录 	l 软链接文件
- ``find . -inum 31531 -exec rm {} \;``：在当前目录下查找inode为31531的文件并删除。可用于查找硬链接文件，因为硬链接文件和原文件有相同的inode。

# 二 其它搜索命令

## 2.1 ``locate``

- 命令名称：locate
- 命令所在路径：/usr/bin/locate
- 执行权限：所有用户
- 语法： ``locate 文件名``
  - ``locate -i test``不区分大小写查找test文件
  - ``updatedb`` 更新文件资料库（不收录/tmp目录下的文件）
- 功能描述：在文件资料库中查找文件

## 2.2 ``which``

- 命令名称：which
- 所在路径：/usr/bin/which
- 执行权限：所有用户
- 语法：``which 命令``
  - ``whereis [命令]`` 可以找到命令及配置文件所在绝对路径及其帮助文档
- 功能描述：搜索命令所在目录及别名信息

## 2.3 ``grep``

- 命令名称：grep
- 所在路径：/bin/grep
- 执行权限：所有用户
- 语法：``grep -iv [指定字串] [文件]``
- 功能描述：在文件中搜寻字符串匹配的行并输出
  - i 不区分大小写
  - -v 排除执行字符串

- 示例：``grep -v ^# /etc/inittab`` 排除以#开头的行，^表示行首。