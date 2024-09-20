Shell 语法
# 一 IF使用详解
## 1 格式
### 1.1 单分支语句结构
```shell
if [ 条件表达式 ]; then
    指令 
fi
```

### 1.2 双分支语句结构
```shell
if [ 条件表达式 ]; then 
    指令一 
else 
    指令二 
fi
```

### 1.3 多分支语句结构
```shell
if [ -f file ]; then
   echo "yes yes yes"
elif [ -z file ]; then
   echo "yes yes"
else
   echo "nonono"
fi
```

上面直接给出了多分支if语句的一个实例。从上面三个结构中可以看出，条件表达式的左右都要有空格。

2 条件表达式的内容
2.1 字符串的判断
str1 = str2　　　　　　当两个串有相同内容、长度时为真 
str1 != str2　　　　　 当串str1和str2不等时为真 
-n str1　　　　　　　 当串的长度大于0时为真(串非空) 
-z str1　　　　　　　 当串的长度为0时为真(空串) 
str1　　　　　　　　   当串str1为非空时为真
1
2
3
4
5
2.2 数字的判断
int1 -eq int2　　　　两数相等为真 
int1 -ne int2　　　　两数不等为真 
int1 -gt int2　　　　int1大于int2为真 
int1 -ge int2　　　　int1大于等于int2为真 
int1 -lt int2　　　　int1小于int2为真 
int1 -le int2　　　　int1小于等于int2为真
1
2
3
4
5
6
2.3 文件的判断
-r file　　　　　用户可读为真 
-w file　　　　　用户可写为真 
-x file　　　　　用户可执行为真 
-f file　　　　　文件为正规文件为真 
-d file　　　　　文件为目录为真 
-c file　　　　　文件为字符特殊文件为真 
-b file　　　　　文件为块特殊文件为真 
-s file　　　　　文件大小非0时为真 
-t file　　　　　当文件描述符(默认为1)指定的设备为终端时为真
1
2
3
4
5
6
7
8
9
2.4 复杂逻辑判断
条件表达式中可能有多个条件，需要使用与或非等逻辑操作。

-a 　 　　　　　 与 
-o　　　　　　　 或 
!　　　　　　　　非
1
2
3
2.5 一个实例
if [ $score -ge 0 ]&&[ $score -lt 60 ];then
        echo "sorry,you are lost!"
elif [ $score -ge 60 ]&&[ $score -lt 85 ];then
        echo "just soso!"
elif [ $score -le 100 ]&&[ $score -ge 85 ];then
        echo "good job!"
else
        echo "input score is wrong , the range is [0-100]!"
fi
1
2
3
4
5
6
7
8
9
当然，上面的实例也可以用 -a 来改写：

if [ $score -ge 0 -a $score -lt 60 ];then
        echo "sorry,you are lost!"
elif [ $score -ge 60 -a $score -lt 85 ];then
        echo "just soso!"
elif [ $score -le 100 -a $score -ge 85 ];then
        echo "good job!"
else
        echo "input score is wrong , the range is [0-100]!"
fi
1
2
3
4
5
6
7
8
9
二 &&与||的使用
有时候，我们可以直接使用&&和||的组合来代替if表达式。

2.1 &&运算符
command1  && command2
1
命令之间使用 && 连接，实现逻辑与的功能。
只有在 && 左边的命令返回真，&& 右边的命令才会被执行。
只要有一个命令返回假（命令返回值 $? == 1），后面的命令就不会被执行。
2.2 ||运算符
command1 || command2
1
命令之间使用 || 连接，实现逻辑或的功能。
只有在 || 左边的命令返回假，|| 右边的命令才会被执行。
只要有一个命令返回真，后面的命令就不会被执行。
比如在ARM的uboot的mkconfig文件中的如下语句：

[ "${BOARD_NAME}" ] || BOARD_NAME="$1"
1
这条语句的意思是如果BOARD_NAME这个变量是空的话（即前半部分条件判断返回为假），执行后边的赋值语句。
