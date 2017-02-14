#文本处理
------

##cut命令
获取每行的第三个字母
```
cut -c3 fileName
```
获取每行的第三至第五个字母
```
cut -c3-5 fileName
```
获取每行的第三和第五个字母
```
cut -c3,5 fileName
```
获取每行的前三个字母
```
cut -c-3 fileName
```
获取每行的第五个字母往后的字母
```
cut -c5- fileName
```
获取文本中的前三个字段
```
cut -f1-3 fileName   			//默认的文本分隔符为\t
//输入
1   New York, New York[10]  8,244,910   1   New York-Northern New Jersey-Long Island, NY-NJ-PA MSA  19,015,900  1   New York-Newark-Bridgeport, NY-NJ-CT-PA CSA 22,214,083
2   Los Angeles, California 3,819,702   2   Los Angeles-Long Beach-Santa Ana, CA MSA    12,944,801  2   Los Angeles-Long Beach-Riverside, CA CSA    18,081,569
3   Chicago, Illinois   2,707,120   3   Chicago-Joliet-Naperville, IL-IN-WI MSA 9,504,753   3   Chicago-Naperville-Michigan City, IL-IN-WI CSA  9,729,825
4   Houston, Texas  2,145,146   4   Dallas-Fort Worth-Arlington, TX MSA 6,526,548   4   Washington-Baltimore-Northern Virginia, DC-MD-VA-WV CSA 8,718,083
5   Philadelphia, Pennsylvania[11]  1,536,471   5   Houston-Sugar Land-Baytown, TX MSA  6,086,538   5   Boston-Worcester-Manchester, MA-RI-NH CSA   7,601,061
//输出
1   New York, New York[10]  8,244,910
2   Los Angeles, California 3,819,702
3   Chicago, Illinois   2,707,120
4   Houston, Texas  2,145,146
5   Philadelphia, Pennsylvania[11]  1,536,471
```

获取输入文本的第四个字段
```
cut -d' ' -f4 fileName

**input**
Hello
World
how are you

**output**
Hello
World
//输入的三行最大字段都不超过4个，为什么只输出Hello和World呢？这题不太靠谱
```

输出某个字段或字段范围和输出某个字母或字符范围类似，不再重复

##head命令
输出前20行
```
head -n20  fileName             //不存在20行的话有多少行算多少行
```
输出第11到第20行
```
head -n20  fileName | tail -n10         
```
输出前20个字符
```
head -c20  fileName             //不存在20个字符的话有多少算多少
```
输出后20行
```
tail -n20  fileName             //不存在20行的话有多少行算多少行
```
输出后20个字符
```
tail -c20  fileName             //不存在20个字符的话有多少算多少
```

##tr命令
将文本中的一些字母按先后顺序替换为另外一些字母
```
tr '()' '[]' fileName
**Input**
int i=(int)5.8
(23 + 5)*2
**Output**
int i=[int]5.8
[23 + 5]*2

tr '[a-z]' '[A-Z]' fileName   //将文本中的小写字母替换为大写字母
```
删除文本中存在的小写字母
```
tr -d '[a-z]' fileName
**Input**
Hello
World
how are you
**Output**
H
W
```
将多个连续出现的给定字符合并为一个
```
tr -s ' ' fileName  //合并多个空格为一个
**Input**
He  llo
Wor  ld
how  are  you
**Output**
He llo
Wor ld
how are you
```

##排序
对文本行进行排序
```
sort fileName
**Input**
Dr. Rajendra Prasad     January 26, 1950    May 13, 1962
Dr. S. Radhakrishnan        May 13, 1962    May 13, 1967
Dr. Zakir Hussain       May 13, 1967    August 24, 1969
Shri Varahagiri Venkata Giri        August 24, 1969 August 24, 1974
Shri Fakhruddin Ali Ahmed       August 24, 1974 February 11, 1977
Shri Neelam Sanjiva Reddy       July 25, 1977   July 25, 198
**Output**
Dr. Rajendra Prasad     January 26, 1950    May 13, 1962
Dr. S. Radhakrishnan        May 13, 1962    May 13, 1967
Dr. Zakir Hussain       May 13, 1967    August 24, 1969
Shri Fakhruddin Ali Ahmed       August 24, 1974 February 11, 1977
Shri Neelam Sanjiva Reddy       July 25, 1977   July 25, 198
Shri Varahagiri Venkata Giri        August 24, 1969 August 24, 1974

sort -r fileName   //降序排序

```
对数字进行排序
sort -rn fileName  //对数字进行降序排序  -n对数字排序

对输入文本中第二个字段数字进行降序排序
```
sort -t$'\t' -nr fileName
//-t$'\t' 以tab分割文本
//-nr 数字降序排序
**Input**
Albany, N.Y.    22.2    46.6    71.1    49.3    38.60    136    64.4    57
Albuquerque, N.M.    35.7    55.6    78.5    57.3    9.47    60    11.0    64
Anchorage, Alaska    15.8    36.3    58.4    34.1    16.08    115    70.8    39 / 60
Asheville, N.C.    35.8    54.1    73.0    55.2    47.07    126    15.3    39
Atlanta, Ga.    42.7    61.6    80.0    62.8    50.20    115    2.1    69 / 65
Atlantic City, N.J.    32.1    50.6    75.3    55.1    40.59    113    16.2    60 / 54
Austin, Texas    50.2    68.3    84.2    70.6    33.65    85    0.9    62 / 58
Baltimore, Md.    32.3    53.2    76.5    55.4    41.94    115    21.5    53
Baton Rouge, La.    50.1    66.6    81.7    68.1    63.08    110    0.2    52 / 46
Billings, Mont.    24.0    46.1    72.0    48.1    14.77    96    56.9    69
Birmingham, Ala.    42.6    61.3    80.2    62.9    53.99    117    1.5    60
Bismarck, N.D.    10.2    43.3    70.4    45.2    16.84    96    44.3    64
Boise, Idaho    30.2    50.6    74.7    52.8    12.19    89    20.6    64
Boston, Mass.    29.3    48.3    73.9    54.1    42.53    127    42.8    52 / 66
Bridgeport, Conn.    29.9    48.9    74.0    54.7    44.15    119    26.2    55 / 49
**Output**
Austin, Texas    50.2    68.3    84.2    70.6    33.65    85    0.9    62 / 58
Baton Rouge, La.    50.1    66.6    81.7    68.1    63.08    110    0.2    52 / 46
Atlanta, Ga.    42.7    61.6    80.0    62.8    50.20    115    2.1    69 / 65
Birmingham, Ala.    42.6    61.3    80.2    62.9    53.99    117    1.5    60
Asheville, N.C.    35.8    54.1    73.0    55.2    47.07    126    15.3    39
Albuquerque, N.M.    35.7    55.6    78.5    57.3    9.47    60    11.0    64
Baltimore, Md.    32.3    53.2    76.5    55.4    41.94    115    21.5    53
Atlantic City, N.J.    32.1    50.6    75.3    55.1    40.59    113    16.2    60 / 54
Boise, Idaho    30.2    50.6    74.7    52.8    12.19    89    20.6    64
Bridgeport, Conn.    29.9    48.9    74.0    54.7    44.15    119    26.2    55 / 49
Boston, Mass.    29.3    48.3    73.9    54.1    42.53    127    42.8    52 / 66
Billings, Mont.    24.0    46.1    72.0    48.1    14.77    96    56.9    69
Albany, N.Y.    22.2    46.6    71.1    49.3    38.60    136    64.4    57
Anchorage, Alaska    15.8    36.3    58.4    34.1    16.08    115    70.8    39 / 60
Bismarck, N.D.    10.2    43.3    70.4    45.2    16.84    96    44.3    64
sort -r fileName   //降序排序

```

##Uniq命令
```
uniq  fieName//如果相邻行文本重复，只保留一行
**Input**
00
00
01
01
00
02
02
**Output**
00
01
00
02 

uniq -u fileName   fieName//获取行中与前后行都不同的行文本
**Output**
00

uniq -d fileName   fieName//获取文本中前后相同的行文本
**Output**
00
01
02

uniq -c | cut -c7-  fieName//获取文本中的字段统计
**Output**
2 00
2 01
1 00
2 02

uniq -ci | cut -c7-  fieName//获取文本中的字段统计，不区分大小写
如输入
**Input**
aA
Aa
AA
aa
**output**
4 aA
```
##paste
```
paste -d':' fileName1 fileName2  //将两个文件按行合并，以':'分割

paste -s fileName  //将文本以'\t'为分隔符进行合并
**Input**
Albany, N.Y.
Albuquerque, N.M.
Anchorage, Alaska
Asheville, N.C.
Atlanta, Ga.
Atlantic City, N.J.
Austin, Texas
Baltimore, Md.
Baton Rouge, La.
Billings, Mont.
Birmingham, Ala.
Bismarck, N.D.
Boise, Idaho
Boston, Mass.
Bridgeport, Conn.

**Output**
Albany, N.Y.    Albuquerque, N.M.   Anchorage, Alaska   Asheville, N.C.Atlanta, Ga. Atlantic City, N.J. Austin, Texas   Baltimore, Md.  Baton Rouge, La.    Billings, Mont. Birmingham, Ala.    Bismarck, N.D.  Boise, Idaho    Boston, Mass.   Bridgeport, Conn.
```

```
paste - - - -d$'\t'  fileName  //将文本以'\t'为分隔符进行合并，每行三列
**Input**
Albany, N.Y.
Albuquerque, N.M.
Anchorage, Alaska
Asheville, N.C.
Atlanta, Ga.
Atlantic City, N.J.
Austin, Texas
Baltimore, Md.
Baton Rouge, La.
Billings, Mont.
Birmingham, Ala.
Bismarck, N.D.
Boise, Idaho
Boston, Mass.
Bridgeport, Conn.

**Output**
Albany, N.Y.    Albuquerque, N.M.   Anchorage, Alaska
Asheville, N.C. Atlanta, Ga.    Atlantic City, N.J.
Austin, Texas   Baltimore, Md.  Baton Rouge, La.
Billings, Mont. Birmingham, Ala.    Bismarck, N.D.
Boise, Idaho    Boston, Mass.   Bridgeport, Conn.

paste -d';' -s fileName    //将文本合并为一行，用';'分割
**Output**
Albany, N.Y.;Albuquerque, N.M.;Anchorage, Alaska;Asheville, N.C.;Atlanta, Ga.;Atlantic City, N.J.;Austin, Texas;Baltimore, Md.;Baton Rouge, La.;Billings, Mont.;Birmingham, Ala.;Bismarck, N.D.;Boise, Idaho;Boston, Mass.;Bridgeport, Conn.

paste - - - -d';'     //将文本合并为一行，用';'分割，每行三列

**Output**
Buffalo, N.Y.;Burlington, Vt.;Caribou, Maine
Casper, Wyo.;Charleston, S.C.;Charleston, W.Va.
```
