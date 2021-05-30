# 一 权限管理命令chmod

## 1.1 文件目录权限

| 代表字符 | 权限 |                对文件的含义                |                   对目录的含义                   |
| :------: | :--: | :----------------------------------------: | :----------------------------------------------: |
|    r     |  读  | 可以查看文件内容(/cat/more/head/tail/less) |            可以列出目录中的内容(/ls)             |
|    w     |  写  |           可以修改文件内容(vim)            | 可以在目录中创建、删除文件(touch/mkdir/rmdir/rm) |
|    x     | 执行 |        可以执行文件(script command)        |                 可以进入目录(cd)                 |

## 1.2 命令简介

- 命令名称：chmod
- 英文原意：change the permissions mode of a file
- 所在路径：/bin/chmod
- 执行权限：所有用户
- 语法：

```
chmod 	[{ugoa}{+-=}{rwx}] [文件或目录] 
		[mode=421] [文件或目录]
```

- -R 递归修改

- 功能描述：改变文件或目录权限

## 1.3 用法示例

​	文件的权限只有文件所有者和管理员root可以更改。

- {ugoa}：u表示所有者，g表示所属组，o表示其他人，a表示所有人。
- {+-=}：+表示增加权限，-表示减少权限，=表示不管之前的权限重新赋予权限。
  - ```chmod g+w,o-r test.list```
  - ```chmod o=rwx test.list```

- [mode=421]：将三个权限位使用数字表示，即r--4、w--2、x--1。
  - ```rwxrw-r--    mode=764```
  - ```chmod 640 test.list```
- -R：修改目录及其子目录下所有文件的权限
  - ```chmod -R 777 /tmp/a/b```

# 二 其它权限管理命令

## 2.1 ```chown```

- 命令名称：chown
- 英文原意：change file wonership
- 所在路径：/bin/chown
- 执行权限：所有用户
- 语法：```chown [用户] [文件或目录]```
- 功能描述：改变文件或目录的所有者，只有管理员root可以修改所有者
- 范例：```chown shenchao liming.list```：将文件liming.list的所有者改为shenchao。

## 2.2 ```chgrp```

- 命令名称：chgrp
- 英文原意：change file group ownership
- 所在路径：/bin/chgrp
- 执行权限：所有用户
- 语法：```chgrp [用户组] [文件或目录]```
- 功能描述：改变文件或目录的所属组

## 2.3 ```umask```

- 命令名称：umask
- 英文原意：the user file-creation mask
- 所在路径：Shell内置命令
- 执行权限：所有用户
- 语法：umask [-S]
  - -S 以rwx形式显示新建文件缺省权限
- 范例：
  - ```umask -S```：运行结果为```u=rwx,g=rx,o=rx```，表示新建文件夹的默认权限，新建文件的权限将在此基础上去掉x。
  - ```umask```：不带-S参数则运行结果为0022，第一个0表示特殊权限，随后022表示rwx rx rx所表示的755取反。

