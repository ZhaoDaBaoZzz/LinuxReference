**Shell问题笔记**

- 井!/bin/bash

指定了shell脚本解释器的路径，只能放在文件的第一行

- 输出空行: echo " " >> temp （自动换行）

输出空格:echo -n " " >> temp （不换行）

- liunx按行和按列追加文件内容

按列: paste a b > c 将文件a b 以列的形式合并

按行:cat a>>b 将文件a追加到文件b的尾部

- 查找文件中特定关键字所在行

cat -n file | grep 'keywords'

- 取特定关键字所在的行号

num=`cat file | grep -n 'kewords'| awk -F":" '{print $1}'`

ps:第一对为键盘左上角的点号

- 写if语句时注意左右方括号中间要空一格，否则报错

if [ -f $content ]

- sed使用变量

cat $content | sed -n "$num,$(($num+10))p"

- if中整数比较和字符串比较

整数比较： if [ "$a" -eq "$b" ] a,b为整数

字符串比较：if [ "$a" = "$b" ] a,b为字符串

- awk输出换行or不换行

cat file | awk '{print $0}' print有换行

cat file | awk '{printf $0}' printf不换行

- 插入换行符

echo $'\n' >>file

- 替换文本字段，并打印替换后的整行文本

awk -F":" '{$1="Demo:";print $0}' file

- 从文件中读取程序命令

awk -F":" -f script file

script内容

{

$1=“Demo:”

print $0

}

- awk取字符串前几位

cat file | awk '{print substr($1,1,5)}' 分别是第1个字段，第1个字符到第5个字符

- sed中使用变量，使用双引号

sed "/$x/d/" file 或 sed -n "$i"p file

- awk中使用变量，双引号包单引号

awk -F" " '{print $"'$i'"}'

- 行转列

cat file | awk -F" " '{for(i=1;i<=NF;i++) print $i}'