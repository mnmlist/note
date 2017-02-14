##awk sed grep

###awk
1.输出字段不全的文本行
```
a.通过第四列是否为空来判断
awk '{
    if( $4 == "") {
        print "Not all scores are available for "$1
    }
}'
b.通过列数是否小于4来判断
awk '{
    if( NF < 4) {
        print "Not all scores are available for "$1
    }
}'

输入：
A 25 27 50
B 35 75
C 75 78 
D 99 88 76

输出：
Not all scores are available for B
Not all scores are available for C
```
2.判断一个学生的成绩是否几及格

```
描述：
A student is considered to have passed if (s)he has a score  or more in each of the three subjects.
输入：
A 25 27 50
B 35 37 75
C 75 78 80
D 99 88 76
输出：
A : Fail
B : Fail
C : Pass
D : Pass
程序：
a.循环遍历每一个元素，小于50，输出Fail
awk '{
    flag=1;
    for(i=2;i<NF;i++) {
        if($i < 50) {
            print $1" : Fail";
            flag=0;
            break;
        }
    }
    if(flag==1) {
       print $1" : Pass";
    }
}'
b.几乎相同的方法，awk对每一行的文本进行处理
awk '{
    if( $1 < 50 || $2 < 50 || $3 < 50) {
        print $1" : Fail"
    } else {
        print $1" : Pass"
    }
}'
```

3.统计平均分，根据平均分输出A、B、C或Fail
描述：Your task is to identify the performance grade for each student. If the average of the three scores is 80 or more, the grade is 'A'. If the average is 60 or above, but less than 80, the grade is 'B'. If the average is 50 or above, but less than 60, the grade is 'C'. Otherwise the grade is 'FAIL'.
输入：
A 25 27 50
B 35 37 75
C 75 78 80
D 99 88 76
输出：
A 25 27 50 : FAIL
B 35 37 75 : FAIL
C 75 78 80 : B
D 99 88 76 : A
代码：
```
//a.对每一行做处理
awk '{
    avg = ($4 + $2 + $3)/3;
    printf $0;printf" : ";
    if(avg < 50) print "FAIL";
    else if(avg < 60) print "C";
    else if(avg < 80) print "B";
    else print "A";
}'
//$0表示整行，$1表示第一列，$2表示第二列
```
4.格式化输出文本行
输入：
A 25 27 50
B 35 37 75
C 75 78 80
D 99 88 76
输出：
A 25 27 50;B 35 37 75
C 75 78 80;D 99 88 76
代码：
```
a.使用awk偶数行输出文本行回车，奇数行输出文本和';'
awk '{
    if( NR%2 == 0 ) {
        printf $0"\n";
    } else {
        printf $0";";
    }
}'
b.使用paste命令来实现
paste - - -d';' fileName
```

###sed

1.将文本中首次出现的the替换为this
```
sed s/"the "/"this "/ fileName   //"the "是因为防止将these替换为thisse

sed 's/thy /your /gi' //替换所有的thy，不区分大小写
```
2.将thy不区分大小写地加{}强调表示
```
sed 's/thy/{&}/gi' fileName   //{&} 加{}且输出其本身
```
3.文本替换
```
将部分文本替换为****
输入：
1234 5678 9101 1234  
2999 5178 9101 2234  
9999 5628 9201 1232  
8888 3678 9101 1232
输出：
**** **** **** 1234
**** **** **** 2234
**** **** **** 1232
**** **** **** 1232
a.sed -r -e 's/[0-9]{4} /**** /g'  fileName  将四个数字和一个空格组成的子串替换为"**** "
```
4.将部分子串颠倒位置
```
输入：
1234 5678 9101 1234  
2999 5178 9101 2234  
9999 5628 9201 1232  
8888 3678 9101 1232
输出：
1234 9101 5678 1234  
2234 9101 5178 2999  
1232 9201 5628 9999  
1232 9101 3678 8888
sed -r 's/(.+ )(.+ )(.+ )(....)/\4 \3\2\1/' fileName
```

###grep

1.使用grep获取匹配整个单词的某行
```
grep -w "the" fileName      //-w 匹配整个单词

grep -iw "the" fileName     //不区分大小写

grep -ivw 'that' fileName   //-v
```
2.匹配文本中包含the 、that 、then 和those的文本
```
grep -iw -e 'th[e,at,en,ose]' fileName

或者grep -iw -e 'the' -e 'that' -e 'then' -e 'those'  fileName
``` 

