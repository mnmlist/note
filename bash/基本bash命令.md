# bash shell

@(我的第一个笔记本)[shell, bash]

-------------------

**1.for循环输出1，3，5，7，9...97，99**
``` bash
for((i=1;i<100;i+=2))
do
	echo $i;
done
//更喜欢这种for循环
```
**2.计算从控制台读取的两个数的和、差、积和商**
算术运算有三种方式：使用 expr 外部程式、使用$[ ]、使用$(( ))和let表达式，个人更喜欢$(( )).
```
read x
read y
echo $((x + y))
echo $((x - y))
echo $((x * y))
echo $((x / y))
```
**3.if else条件判断表达式**
比较从控制台输入的两个整数的大小
```
read x
read y
if [ $x -gt $y ]; then
echo "X is greater than Y"
elif [ $x -lt $y ]; then
echo "X is less than Y"
else
echo "X is equal to Y"
fi
//要注意在'['后面和']'前面都必须要有空格;
```
判断字符串的是否相等
```
read ch
if [ $ch = 'Y' -o $ch = 'y' ]; then
echo "YES"
else
echo "NO"
fi
//字符串判断用"="判断两个字符串是否相等，而不是"==";
```
判断三角形的形状：等边、等腰或不等边
```
read a
read b
read c
if [ $a = $b -a $a = $c -a $b = $c ]; then
echo "EQUILATERAL"
elif [ $a = $b -o $a = $c -o $b = $c ]; then
echo "ISOSCELES"
else
echo "SCALENE"
fi
//使用-o或-a来连接不同的逻辑判断条件
```


字符串判断
[ -z str ] 如果str的长度为零则返回为真，即空是真
[ str ]　 如果字符串不为空则返回为真,与-n类似
[ str1 = str2 ] 如果两个字符串相同则返回为真
[ str1 != str2 ] 如果字符串不相同则返回为真
[ str1 < str2 ] 如果 str1字典排序在str2前面则返回为真。

数值判断
[ num1 -eq num2 ] 等于
[ num1 -ne num2 ] 不等
[ num1 -gt num2 ] 大于
[ num1 -ge num2 ] 大于等于
[ num1 -lt num2 ] 小于
[ num1 -le num2 ] 小于等于


逻辑判断
[ ! EXPR ] 逻辑非
[ EXPR1 -a EXPR2 ] 逻辑与
[ EXPR1 -o EXPR2 ] 逻辑或
[ ] || [ ] 用OR来合并两个条件
[ ] && [ ] 用AND来合并两个条件

**4.数学表达式的计算 **
计算输入的数学表达式的值
```
read str							//从控制台读取数学表达式
printf "%.3f" $(echo $str | bc -l)  //计算数学表达式 
//"%.3f"输出浮点数，在小数点第三位进行四舍五入
//echo $str | bc -l  计算数学表达式，如echo "5/3" | bc -l，输出1.66666666666666666666
```
从控制台读取一定数目的数字，然后计算器平均值
```
read count
sum=0
for((i=0;i<count;i++))
do
read num
sum=$((sum+num))
done
printf "%.3f" $(echo "$sum/$count" | bc -l)
```
count用来表示读取数字的数量，sum表示和，然后通过echo "$sum/$count" | bc -l计算其平局值
