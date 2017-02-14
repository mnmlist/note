##Arrays in bash

1.将多行文本合并为一行
```
i=0
while read line
do
arr[$i]=$line
((i++))
done
echo ${arr[@]}       //echo ${arr[@]}输出所有的数组元素

**Input**
Namibia
Nauru
Nepal
Netherlands
NewZealand
Nicaragua
Niger
Nigeria
NorthKorea
Norway
**Output**
Namibia Nauru Nepal Netherlands NewZealand Nicaragua Niger Nigeria NorthKorea Norway
```
2.将包含‘a'字母的文本行删掉
```
i=0
while read line
do
arr[$i]=$line
((i++))
done
echo ${arr[@]/*[aA]*/}

**Input**
Namibia
Nauru
Nepal
Netherlands
NewZealand
Nicaragua
Niger
Nigeria
NorthKorea
Norway
**Output**
Niger

**Output2**
echo ${arr[@]/*[aA]*/hello}  //使用hello替换掉所有包含a的文本行
hello hello hello hello hello hello Niger hello hello hello
```
3.将上述输入文本重复输出三次
```
X=$(paste -sd' ' fileName)
echo $X $X $X

X=$(cat fileName)
echo $X $X $X

**Output**
Namibia Nauru Nepal Netherlands NewZealand Nicaragua Niger Nigeria NorthKorea Norway Namibia Nauru Nepal Netherlands NewZealand Nicaragua Niger Nigeria NorthKorea Norway Namibia Nauru Nepal Netherlands NewZealand Nicaragua Niger Nigeria NorthKorea Norway
```

4.输出某个元素
```
echo ${arr[3]}
```

5.统计输入文本有多少行
```
a.使用wc命令
wc -l

b.使用echo命令
arr=($(cat))
echo ${#arr[@]}

c.使用for循环
i=0
while read line
do
arr[$i]=$line
((i++))
done
echo "$i"
```
6.将每行第一个大写字母替换为.
```
a.使用sed命令仅替换第一个大写字母为.
sed 's/[A-Z]/./' | paste -sd ' '

b.使用数组的替换来实现
X=($(cat)) 
echo "${X[@]/[A-Z]/.}"

**Output**
.amibia .auru .epal .etherlands .ewZealand .icaragua .iger .igeria .orthKorea .orway
```
7.找出一组数据中落单的数
```
a.首先将' '替换为换行，然后对每行数据排序，获取只出现一次的数字
tr ' ' '\n' | sort | uniq -u
```

