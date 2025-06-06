# MyShell

开头写

```vim
#!/bin/bash       --->shell会去找这个路径
```



## 一 . 语法



### 条件判断

| 比较                     | 含义     |
| ------------------------ | -------- |
| `-eq`                    | 等于     |
| `-ne`                    | 不等于   |
| `-gt`---->greater than   | 大于     |
| `-lt`----->less than     | 小于     |
| `-ge`      greater equal | 大于等于 |
| `-le`-------->less equal | 小于等于 |





### if

```bash
if [ 条件 ]
then
    命令1
    命令2
fi


紧凑型
if [ 条件 ]; then
    命令
fi


多条件
if 条件
then 
elif 条件
then 
	条件
	......
fi


实例
#!/bin/bash

read -p "请输入一个值: " num

if ((num<60))
then
        echo "不及格"
elif ((num>60 && num<80))
then
        echo "不错啊"
elif ((num>80 && num<=100))
then
        echo "666"
else
        echo "输入错误"
fi
```





1. `elif` 是 `else if` 的缩写，Shell 里必须用它。

2. `then` 是 **必须的关键字**，每个 `if` 和 `elif` 后都要带。

3. `[[]]` 里面 **空格必须有**，比如 `[[ $a -eq $b ]]`。

4. `number=$(shuf -i 1-50 -n 1)`，中间 **不能有空格**，不然 Shell 会误解。



#### 退出状态码

大多数情况下命令状态码0表示成功 , 非0表示失败

> diff命令比较两个文件的不同除外
>
> 无差别 0 
>
> 找到差别 1
>
> 无效文件名 2









### while

```bash


while [ 条件 ]; do
    命令1
    命令2
    ...
done

例
#!/bin/bash

i=1
while [ $i -le 5 ]; do
    echo "当前数字是 $i"
    ((i++))  # 注意是双括号：自增写法
done


无限循环1
while :
do
	
done


无限循环2
while true
do

done
```



```bash
实例
#!/bin/bash

echo "欢迎 $myname 进入游戏"

# 生成一个 1 到 50 之间的随机数
number=$(shuf -i 1-50 -n 1)

echo "我想了一个 1 到 50 的数字，开猜吧！"

while true; do
    read -p "你的猜测是: " guess

    if [[ $guess -eq $number ]]; then
        echo "666啊，猜对了！"
        break
    elif [[ $guess -gt $number ]]; then
        echo "太大了 bigger ⬆️"
    elif [[ $guess -lt $number ]]; then
        echo "太小了 smaller ⬇️"
    fi
done


```



#### 





### for

```bash
for var in val1 val2 val3
do
    命令
done

范围打印
for i in {1..5}
do
    echo "$i"
done


//c风格
for (( i=1; i<=5; i++ ))
do
    echo "$i"
done


//遍历参数
for arg in "$@"
do
    echo "参数：$arg"
done
	
```



### case

```bash
case 变量 in
  模式1)
    命令1
    ;;
  模式2)
    命令2
    ;;
  模式N)
    命令N
    ;;
  *)
    默认命令
    ;;
esac


in：进入匹配分支

)：分隔模式与命令

;;：表示该分支结束

*：通配符，类似于 C++ 的 default

esac：case 的反过来拼写，是结束标志
```









### until

> 只要“条件为假”，`do` 里的内容就一直执行；**条件为真就停止循环**。

```bash
until 条件
do


done


i=0
until i>5 ----------->直到大于5时停止!
do


done
```



### select

> 交互式 , 常与case in搭配

``` bash
select var in menu1 menu2 ...
do
	case $var in menu1)
	echo ...
	break 		---->注意一定要break不然会继续
	;; 


done


eg.
select name in "KOBE" "Black" "黑"
do
	echo $name
done

echo $name //可以获取得到


会像列表一样展示
1) KOBE
2) Black
3) 黑

```







## 二 . 脚本命令的三种执行方式

1. sh 文件名.sh
2. bash 文件名.sh
3. ./文件名.sh             -->当前目录下的脚本文件







## 多命令处理

在shell脚本文件中编写多个shell命令

```bash
#!/bin/bash

echo "Hello World" >> /nash/one.txt   //---->重定向符
```







## 环境变量



### Shell的配置文件分类

1.全局配置文件
/etc/profile
/etc/profile.d/*.sh
/etc/bashrc

2.个人配置文件
当前用户/.bash_profile
当前用户/.bashrc

一般情况下，我们都是直接针对全局配置进行操作。





### 环境变量分类

系统级环境变量：全局共享
用户级环境变量：Shell环境加载==个人配置文件==中的变量共享给当前用户的Shell程序使用, 登录用户使用



### 常用变量

| 变量名称 | 含义                                                         |
| -------- | ------------------------------------------------------------ |
| PATH     | 与windows环境变量PATH功能一样，设置命令的搜索路径，以冒号为分割 |
| HOME     | 当前用户主目录：/root                                        |
| SHELL    | 当前shell解析器类型：/bin/bash                               |
| HISTFILE | 显示当前用户执行命令的历史列表文件：/root/.bash_history      |
| PWD      | 显示当前所在路径：/root                                      |
| OLDPWD   | 显示之前的路径                                               |
| HOSTNAME | 显示当前主机名：itheima                                      |
| HOSTTYPE | 显示主机的架构，是i386、i686、还是x86、x64等：x86_64         |
| LANG     | 设置当前系统语言环境：zh_CN.UTF-8                            |







### 查看命令

1. env--->查看系统级 , 用户级
2. set--->查看所有变量







### 分类

#### 环境变量

.bashrc 文件中------------------->可以自己加 记得变化后刷新文件



#### 自定义

​	局部变量 : 在脚本文件中的变量

##### 	查询变量值

1. 直接使用变量名查询

2. 使用花括号---->适合拼接字符串

   ${name}此处可以加其他

   ```
   ${name}aaa
   ```



##### 删除变量

unset name

- 等号两边==不能加空格==

 - bash环境中变量默认是String类型 , 无法直接进行数值运算

   

#### 自定义常量

readonly name=sth

​	



#### 自定义全局变量

```bash
临时的
export name=val

永久的
vim .bashrc   --->进入
export name=val --->导入
. .bashrc  --->刷新

//如果要删除除了在文件中删掉对应的变量还要unset!!!!!!!!!!!!!然后刷新

shell里面执行shell

demo2.sh:
export var1=泪眼问花花不语
sh demo3.sh

demo3.sh
echo $var1

sh demo2.sh--------->得到结果 : 泪眼问花花不语
```







#### 特殊符号变量

| 符号              | 含义                                                         |
| ----------------- | ------------------------------------------------------------ |
| `$0`              | 当前脚本的文件名（不包含路径）                               |
| `$1` `$2` ...`$n` | 第 1、第 2 ... 个**位置参数**，即执行脚本时传的参数          |
| `$#`              | **所有参数的个数**（不包括 `$0`）                            |
| `$@`              | 以 `"$1" "$2" ...` 的形式展开所有参数（保留引号）            |
| `$*`              | 以 `"$1 $2 ..."` 的形式展开所有参数（变成一个字符串）        |
| `$$`              | 当前脚本的 **进程号（PID）**                                 |
| `$!`              | 最近一个**后台运行的命令的进程号**                           |
| `$?`              | 最近一次命令的**退出状态码**<br />（0 表示成功）<br />非零表示失败 |



```bash
demo4.sh

#!/bin/bash

echo "第一个参数$1"
echo "第10个参数${10}"  ----------->不带花括号就会编程 第一个参数名+0

sh demo4.sh 参数1~10
```







| 写法   | 含义                                        |
| ------ | ------------------------------------------- |
| `$*`   | 把所有参数拼成一个字符串，用空格隔开        |
| `$@`   | 把每个参数保留成独立的字符串                |
| `"$*"` | 所有参数 → 一个字符串，整体作为一个参数传递 |
| `"$@"` | 所有参数 → 各自是一个独立参数（最常用 ✅）   |

```bash
#!/bin/bash

echo '===== 无引号 $* ====='
for arg in $*; do
    echo "[$arg]"
done

echo '===== 无引号 $@ ====='
for arg in $@; do
    echo "[$arg]"
done

echo '===== 加引号 "$*" ====='
for arg in "$*"; do
    echo "[$arg]"
done

echo '===== 加引号 "$@" （推荐）====='
for arg in "$@"; do
    echo "[$arg]"
done


===== 无引号 $* $@=====
[Alice]
[Bob]
[Charlie]
[Brown]

===== 加引号 "$*" =====
[Alice Bob Charlie Brown]


===== 加引号 "$@" （推荐）=====
[Alice]
[Bob]
[Charlie Brown]
```





## 三 . 环境变量加载流程

### 1.工作环境

#### 交互式Shell 与 非交互式Shell



#### 登录Shell 与 非登录Shell

> 前者需要用户名/密码登录的环境执行
>
> 后者不需要登录就可以执行
>
> 两者加载环境变量的流程不一样





#### 环境变量初始化流程

shell登录环境

```bash
/etc/profile----------->登录状态环境变量装在这里
    ↳ /etc/profile.d/*.sh （可能由 /etc/profile 引用）
~/.bash_profile
    ↳ ~/.bash_login
    ↳ ~/.profile
```



shell非登陆环境-->只执行命令不需要用户的参与

```bash
~/.bashrc ------->只能看这里的变量
```



## Shell登录环境执行脚本文件语法

```shell
sh/bash -l/--login 脚本文件
```

> 含义: 先加载Shell登录环境流程初始化环境变量, 再执行脚本文件

## Shell非登录环境变量执行脚本文件语法

```shell
bash # 加载Shell非登录环境
sh/bash 脚本文件 # 直接执行脚本文件
```

> 含义: 先执行加载Shell非登录环境流程初始化环境变量, 再执行脚本文件





## 使用$0识别环境语法

```shell
echo $0
```

> 输出 `-bash` 代表：shell登录环境
>
> 输出 `bash` 代表：  shell非登录环境
>
> 注意：这个 `$0` 环境变量如果用在子shell中(shell脚本文件)输出Shell脚本本身的文件名 

bash命令语法

```shell
bash
```

> bash命令：用于切换为Shell非登录环境





## su切换用户登录

语法1 

```bash
su name --login
su name -l
#切换到指定用户 并且加载Shell登录环境变量
```



语法2

```bash
su name
#切换到指定用户 并且加载Shell非登录环境变量
```



## Shell提示符

```bash
[用户名@主机名 当前目录]$/#---->$是普通用户  而 #是root用户

root用户在主目录下
[root@aschenbath ~]#


如果你进入了某个子目录，比如 /etc，提示符就变了：
[root@aschenbath etc]#
```







## shell字符串

### 三种表示方式

1. 无引号
   不能有空格

2. 单引号

   单引号不会解析出变量val , 只会打印变量名

   ![image-20250529095911963](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250529095911963.png)

3. 双引号 (推荐)

   这个可以解析变量!!!!!!!!!!!!!

   

### 获取长度

```bash
${#字符串变量名}
```





### 拼接

1. 无符号拼接

   ```
   var1=666
   var2=hhhh
   var3=${var1}${var2} ---------->666hhhh
   ```

2. 双引号拼接

   ```bash
   var3="${var1}${var2}"
   ```

3. 混合拼接

   ```bash
   var3= ${var1}'&'${var2}
   /
   var3= ${var1}"&"${var2}
   ```

   

### 截取

| 格式                       | 说明                                                         |
| -------------------------- | ------------------------------------------------------------ |
| `${变量名:start:length}`   | 从 string 字符串的左边第 start 个字符开始， 向右截取 length 个字符。start从0开始 |
| `${变量名:start}`          | 从 string 字符串的左边第 start 个字符开始截取，直到最后。    |
| `${变量名:0-start:length}` | 从 string 字符串的右边第 start 个字符开始， 向右截取 length 个字符。start从1开始, 代表右侧第一个字符 |
| `${变量名:0-start}`        | 从 string 字符串的右边第 start 个字符开始截取，直到最后。    |
| `${变量名#*chars}`         | 从 string 字符串左边第一次出现 *chars 的位置开始， 截取 *chars 右边的所有字符。 |
| `${变量名##*chars}`        | 从 string 字符串左边最后一次出现 *chars 的位置开始， 截取 *chars 右边的所有字符。 |
| `${变量名%chars*}`         | 从 string 字符串右边第一次出现 chars* 的位置开始， 截取 chars* 左边的所有字符。 |
| `${变量名%%chars*}`        | 从 string 字符串右边最后一次出现 chars* 的位置开始， 截取 chars* 左边的所有字符 |



## shell索引数组

### 数组的定义

#### 语法

在 Shell 中，用==括号`( )`==来表示数组，数组元素之间用==空格==来分隔. 语法为：

可以装==多种不同==类型!!!

```shell
array_name=(item1  item2 ...)  # 方式1
array_name=([索引下标1]=item1  [索引下标2]=item2  ...)  # 方式2
```

> 注意，赋值号 `=` 两边不能有空格

#### 演示

1.定义数字存储100,3,22,58,77,17,20

```shell
nums=(29 100 13 8 91 44)
```

2.Shell 是弱类型的，它并不要求所有数组元素的类型必须相同

```shell
arr=(20 56 "http://www.itcast.cn/")
```

Shell数组元素定义后不是固定的,  定义后还可以赋值

```shell
arr[6]=100
```

3.可以给指定元素赋值初始化

```shell
arr2=([0]=1 [2]=100 [4]=aa)
```

> 由于上面只赋值了3个元素, 所以数组的长度是3



### 数组的获取

#### 语法

1.通过下标==获取==元素值,index从0开始

```shell
${arr[index]}

arr_name=([1]=item1 [2] =item2)
```

> 注意使用`{ }`

2.获取值同时复制给其他变量

```shell
item=${arr[index]}
```

3.使用 `@` 或 `*` 可以获取数组中的所有元素

```shell
${arr[@]}
${arr[*]}
```

4.获取数组的长度或个数

```shell
${#arr[@]}
${#arr[*]}
```

5.获取数组指定元素的字符长度

```shell
${#arr[索引]}
```

6. 拼接两个数组

   ```bash
   arr3=(${arr1[*]} $arr2[@]) ------>注意一定是空格隔开才是数组
   
   [root@aschenbath /]# nums1=(1 2 5 45 6 846 4)
   [root@aschenbath /]# nums2=(${nums[*]} ${nums1[*]})
   [root@aschenbath /]# echo ${nums2[*]}
   666 1 2 33 str 1 2 5 45 6 846 4
   ```

7. 删除元素

   unset 数组[下标]

   ```bash
   unset nums[1]
   unset nums  ----->全删
   ```

   

## Shell内置命令

### type 命令

> 会打印是否为内置命令
>
> 内置命令执行得快
>
> 脚本命令执行得慢
>
> 通常来说，内置命令会比外部命令执行得更快，
>
> 执行外部命令时  不但会触发磁盘 I/O，
> 还需要 fork 出一个单独的进程来执行，执行完成后再退出。
>
> 而执行内置命令相当于调用当前 Shell 进程的一个函数, 还是在当前Shell环境进程内, 减少了上下文切换。





### alias起别名

```bash
alias -->会打印当前已设置的所有别名

alias newname="别名"
unalias 别名 ------>删除指定
unalias -a ----->删除当前shell环境中的所有别名
```





### read

```bash
read -op var1 var2 var3


read <enter>
123
echo $REPLY ---------->>输出最后一个读到的数据
123
```

-op选项

| 选项         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| -a array     | 把读取的数据赋值给数组 array，从下标 0 开始。                |
| -d delimiter | 用字符串 delimiter 指定读取结束的位置，而不是一个换行符（读取到的数据不包括 delimiter）。 |
| -e           | 在获取用户输入的时候，对功能键进行编码转换，不会直接显式功能键对应的字符。 |
| -n num       | 读取 num 个字符，而不是整行字符。                            |
| -p  prompt   | 显示提示信息，提示内容为==prompt==。                         |
| -r           | 原样读取（Raw mode），不把反斜杠字符解释为转义字符。         |
| -s           | ==静默模式==（Silent mode），不会在屏幕上显示输入的字符。 当输入密码和其它确认信息的时候，这是很有必要的。 |
| -t seconds   | 设置超时时间，单位为秒。如果用户没有在指定时间内输入完成， 那么 read 将会返回一个非 0 的退出状态，表示读取失败。 |
| -u fd        | 使用文件描述符 fd 作为输入源，而不是标准输入，类似于重定向。 |



只读取一个字符

```bash
read -p prompt -n 1 char
printf "\n"
echo char
```



### exit

> 用于退出当前shell环境进程 , 并且可以返回一个状态码

```bash
exit #默认返回状态码0 表示成功
     #一般是0~255
     exit `n` --->自定义返回状态码用于不同的业务处理
```





### declare

> 用于声明shell变量 

基本用法

| 用法                   | 描述                                     | 示例                                      |
| ---------------------- | ---------------------------------------- | ----------------------------------------- |
| `declare var=value`    | 声明一个普通变量                         | `declare myvar=123`                       |
| `declare -i var=value` | 将变量声明为**整数**（自动进行算术运算） | `declare -i num=5+3` → `num=8`            |
| `declare -r var=value` | 声明为**只读变量**，不可再修改           | `declare -r pi=3.14`                      |
| `declare -a var`       | 声明为==**数组变量**==                   | `declare -a fruits=(apple banana cherry)` |
| `declare -A var`       | 声明为**关联数组（字典）**               | `declare -A dict; dict[foo]=bar`          |
| `declare -x var=value` | 将变量**导出为==环境变量==**             | `declare -x PATH=$PATH:/my/bin`           |
| `declare -l var`       | 声明变量为**小写**（自动转小写）         | `declare -l name; name="HELLO"` → `hello` |
| `declare -u var`       | 声明变量为**大写**（自动转大写）         | `declare -u name; name="hello"` → `HELLO` |
| `declare -f`           | 显示所有**函数定义**                     | `declare -f`                              |
| `declare -F`           | 显示所有**函数名（不含函数体）**         | `declare -F`                              |
| `declare -p var`       | 显示变量的**声明信息**                   | `declare -p PATH`                         |



`+` 表示取消变量所设的属性

`-`表示指定变量的属性



## 关联数组

> 相当于map

### key-val

```bash
declare -A arr=([key1]=val1 [key2]=val2 [key3]=val3)
```







## 运算符







#### 算术运算符

##### 对于整型

> 必须是整型
>
> expr求值表达式
>
> +- \* /

```shell
res=`expr 算数运算符表达式`  

res=`expr 1 + 1` ----->注意必须空格!!!!!!!!!!!!!!!!!!
/
res=$(expr $a + $b)

expr 1 \* 2 ---->2
```



| 运算符 | 说明 | 举例                                                    |
| :----- | :--- | :------------------------------------------------------ |
| +      | 加法 | `expr $a + $b` 结果为 3                                 |
| -      | 减法 | `expr $a - $b` 结果为 -1                                |
| *      | 乘法 | `expr $a \* $b` 结果为  2    ---->>注意乘法要用转义字符 |
| /      | 除法 | `expr $b / $a` 结果为 2                                 |
| %      | 取余 | `expr $b % $a` 结果为 0                                 |
| =      | 赋值 | a=$b 将把变量 b 的值赋给 a                              |





##### 对于字符串

求长度

```bash
expr length 字符串
```



截取长度

```bash
expr substr 字符串 start end
```



获取第一个字符在字符串出现的位置

```
expr index 被查找到串 需要查找到字符
```



正则表达式匹配语法 1

```bash
expr "$string" : '正则表达式'

expr match "$String" "正则"



expr "hello123" : '.*'   # 返回 8

expr "hello123" : '.*\([0-9][0-9]*\)'  
# 提取结尾数字：123

if expr "$var" : '^[0-9][0-9]*$' > /dev/null; then
  echo "是数字"
else
  echo "不是数字"
fi
```

| 表达式    | 含义                                     |
| --------- | ---------------------------------------- |
| `.`       | 匹配任意单个字符                         |
| `*`       | 匹配前一个字符==零==次或==多==次         |
| `^`       | 匹配行首                                 |
| `$`       | 匹配行尾                                 |
| `[a-z]`   | 匹配小写字母                             |
| `\(` `\)` | 捕获组                                   |
| `\{n,m\}` | 重复 n 到 m 次（不是所有 `expr` 都支持） |



##### 更现代的写法

```bash
if [[ "$string" =~ 正则表达式 ]]; then
  echo "匹配成功"
else
  echo "匹配失败"
fi
```







#### 比较运算符

成立返回 0  ,  否则返回  1

> 注意只能比较整数

| 运算符 | 说明                                                         | 举例                     |
| :----- | :----------------------------------------------------------- | :----------------------- |
| `-eq`  | equals 检测两个数是否相等，相等返回 0, 否则返回1。           | `[ $a -eq $b ]` 返回 1。 |
| `-ne`  | not equals检测两个数是否不相等，不相等返回 true。            | `[ $a -ne $b ]` 返回 0。 |
| `-gt`  | greater than检测左边的数是否大于右边的, 是返回0, 否则1       | `[ $a -gt $b ]` 返回 1。 |
| `-lt`  | lower than检测左边的数是否小于右边的, 是返回0, 否则1         | `[ $a -lt $b ]` 返回 0。 |
| `-ge`  | greater equals检测左边的数是否大于等于右边的, 是返回0, 否则1 | `[ $a -ge $b ] `返回 1。 |
| `-le`  | lower equals检测左边的数是否小于等于右边的, 是返回0, 否则1   | `[ $a -le $b ] `返回 0。 |
| `<`    | 检测左边的数是否小于右边的, 是返回0, 否则1                   | `(($a<$b))` 返回0        |
| `<=`   | 检测左边的数是否小于等于右边的, 是返回0, 否则1               | `(($a<=$b))` 返回0       |
| `>`    | 检测左边的数是否大于右边的, 是返回0, 否则1                   | `(($a>$b))` 返回1        |
| `>=`   | 检测左边的数是否大于等于右边的, 是返回0, 否则1               | `(($a>=$b))` 返回1       |
| `==`   | 检测左边的数是否等于右边的, 是返回0, 否则1                   | `(($a==$b))` 返回1       |
| `!=`   | 检测左边的数是否不等于右边的, 是返回0, 否则1                 | `(($a!=$b))` 返回0       |



> 字符串比较

| 比较方式     | 表达式示例          | 说明                   |
| ------------ | ------------------- | ---------------------- |
| 等于         | `[ "$a" = "$b" ]`   | 两字符串相等           |
| 不等于       | `[ "$a" != "$b" ]`  | 两字符串不相等         |
| 非空（存在） | `[ -n "$a" ]`       | 字符串长度非零（非空） |
| 空字符串     | `[ -z "$a" ]`       | 字符串长度为零（空）   |
| 按字典序大于 | `[[ "$a" > "$b" ]]` | 字典序比较，a > b      |
| 按字典序小于 | `[[ "$a" < "$b" ]]` | 字典序比较，a < b      |



注意`[]`和`[[]]`的区别

> [ ] 比较 < >，记得加转义；
> [[ ]] 天生好，不用逃转义。

| 比较方式     | 表达式示例          | 说明                   |
| ------------ | ------------------- | ---------------------- |
| 等于         | `[ "$a" = "$b" ]`   | 两字符串相等           |
| 不等于       | `[ "$a" != "$b" ]`  | 两字符串不相等         |
| 非空（存在） | `[ -n "$a" ]`       | 字符串长度非零（非空） |
| 空字符串     | `[ -z "$a" ]`       | 字符串长度为零（空）   |
| 按字典序大于 | `[[ "$a" > "$b" ]]` | 字典序比较，a > b      |
| 按字典序小于 | `[[ "$a" < "$b" ]]` | 字典序比较，a < b      |







##### `()`,`(())`,`[]`,`[[]]`的区别

| 符号    | 类型     | 用途简述                       | 示例               |
| ------- | -------- | ------------------------------ | ------------------ |
| `()`    | 子 Shell | 创建子进程、命令组             | `(cd /tmp && ls)`  |
| `(())`  | 算术运算 | 数值计算、整数判断             | `((a = 3 + 5))`    |
| `[]`    | 测试命令 | 条件判断，字符串/整数/文件等   | `[ "$a" = "b" ]`   |
| `[[ ]]` | 扩展测试 | 更强的条件判断，支持模式匹配等 | `[[ "$a" == a* ]]` |

> Bash 在变量展开后自动按空格分词了。



> <= / >= 用&&拆分





#### 逻辑运算符

注意这个和其他高级语言不一样    0才是成立

| 运算符 | 说明                           | 举例                   |
| ------ | ------------------------------ | ---------------------- |
| !      | 取反,经常和test命令 , 必须有[] | [ ! 表达式 ]           |
| -o     | 布尔or                         | [ expr1 -o expr2 ]     |
| -a     | 布尔and                        | [ expr1 -a expr2 ]     |
| &&     | 逻辑与                         | [[ expr1 && expr2 ]]   |
| \|\|   | 逻辑或                         | [[ expr1 \|\| expr2 ]] |

> && 和 || 必须放在 [[]] or (()) 才能生效
>
> ! 可以用在[] [[]] 但不能在(())用





#### 文件测试运算符

| 运算符            | 作用说明                            | 示例                          |
| ----------------- | ----------------------------------- | ----------------------------- |
| `-e`              | 文件是否存在                        | `[ -e file.txt ]`             |
| `-f`              | 是否为普通文件（非目录、设备等）    | `[ -f file.txt ]`             |
| `-d`              | 是否为目录                          | `[ -d /home/user ]`           |
| `-L`              | 是否为符号链接                      | `[ -L mylink ]`               |
| `-r`              | 当前用户是否对文件有读权限          | `[ -r file.txt ]`             |
| `-w`              | 当前用户是否有写权限                | `[ -w file.txt ]`             |
| `-x`              | 当前用户是否有执行权限              | `[ -x script.sh ]`            |
| `-s`              | 文件是否非空                        | `[ -s file.txt ]`             |
| `-b`              | 是否为块设备文件                    | `[ -b /dev/sda ]`             |
| `-c`              | 是否为字符设备文件                  | `[ -c /dev/tty ]`             |
| `-p`              | 是否为命名管道（FIFO）              | `[ -p mypipe ]`               |
| `-S`              | 是否为 socket 文件（套接字）        | `[ -S /var/run/docker.sock ]` |
| `-u`              | 是否设置了 SUID 位                  | `[ -u /usr/bin/passwd ]`      |
| `-g`              | 是否设置了 SGID 位                  | `[ -g /usr/bin/mail ]`        |
| `-k`              | 是否设置了 Sticky 位（粘滞位）      | `[ -k /tmp ]`                 |
| `file1 -nt file2` | file1 是否比 file2 新（newer than） | `[ file1 -nt file2 ]`         |
| `file1 -ot file2` | file1 是否比 file2 旧（older than） | `[ file1 -ot file2 ]`         |
| `file1 -ef file2` | 是否是同一个 inode 的文件           | `[ file1 -ef file2 ]`         |



##### 正则表达式

| 符号     | 含义                            |
| -------- | ------------------------------- |
| `*`      | 匹配任意长度的任意字符          |
| `?`      | 匹配一个任意字符                |
| `[abc]`  | 匹配 a、b 或 c 中的任意一个字符 |
| `[a-z]`  | 匹配小写字母 a 到 z             |
| `[^a-z]` | 匹配不在 a-z 范围内的字符       |





### 计算命令

#### expr表达式

> ((expr))用于计算
>
> 不需要加$ , (())可以自动解析变量名



1. 多表达式赋值

   ```bash
   ((a=1,b=a+1,c=3))-->比无括号方便多
   ```

2. 计算





#### let命令

> 赋值推荐使用这个

```bash
let a=b+1

多表达式
let b=1 a=b+12 c=a+b
```





#### $[]命令

```bash
只能放一个表达式
a=$[1+2]
/
a=$[b+c]
```







#### bc命令

语法

``` bash
bc -op 参数
```

| 功能       | 示例                    | 说明           |
| ---------- | ----------------------- | -------------- |
| 加减乘除   | `echo "5*6-2" | bc`     | 基础运算       |
| 浮点       | `scale=2; 5/3`          | 控制小数精度   |
| 数学库     | `echo "s(0.5)" | bc -l` | sin/cos/log 等 |
| shell 变量 | `echo "$a * $b" | bc`   | 与 shell 联动  |
| 多行       | `bc <<EOF ... EOF`      | 嵌入脚本       |



##### 内置变量

| 变量    | 含义                                              | 示例                      |
| ------- | ------------------------------------------------- | ------------------------- |
| `scale` | ==设置小数点后精度==（默认为 0，`bc -l` 默认 20） | `scale=5; 5/3`            |
| `ibase` | 输入进制（默认 10）                               | `ibase=16; A+1` 结果为 11 |
| `obase` | 输出进制（默认 10）                               | `obase=2; 5` 输出 `101`   |
| `last`  | 上一次计算的结果（自动保存）                      | `last + 2`                |

eg.

```bash
echo "scale=3; 7 / 3" | bc         # 输出 2.333
echo "ibase=16; A + 1" | bc        # 输出 11（十进制）
echo "obase=2; 7" | bc             # 输出 111（二进制）

ibase=2;111 ---->7

```



##### 内置函数 (需要加-l)

想要使用必须进来的时候加``-l`

| 函数      | 描述               | 示例                   |
| --------- | ------------------ | ---------------------- |
| `s(x)`    | 正弦函数           | `s(0)` → 0             |
| `c(x)`    | 余弦函数           | `c(0)` → 1             |
| `a(x)`    | 反正切（atan）     | `a(1)` → ≈ 0.785398... |
| `l(x)`    | 自然对数 ln(x)     | `l(2.71828)` → ≈ 1     |
| `e(x)`    | e 的 x 次方（e^x） | `e(1)` → ≈ 2.71828     |
| `sqrt(x)` | 平方根             | `sqrt(2)` → ≈ 1.41421  |

eg.

```bash
echo "scale=5; sqrt(2)" | bc -l          # 平方根
echo "scale=5; s(1.5708)" | bc -l        # sin(π/2) ≈ 1
echo "scale=8; l(10)" | bc -l            # ln(10)
赋值要用``或者$()

e(2)
```



###### 输入重定向

```bash
bc -op << EOF
expr1
expr2
expr3
EOF
```

## 







### test命令

```bash
test 条件表达式
```



#### 三个基本比较

1. 文件判断

| 表达式    | 含义           |
| --------- | -------------- |
| `-e file` | 文件是否存在   |
| `-f file` | 是否为普通文件 |
| `-d file` | 是否为目录     |
| `-r file` | 是否可读       |
| `-w file` | 是否可写       |
| `-x file` | 是否可执行     |

2. 整数比较

| 表达式    | 含义     |
| --------- | -------- |
| `a -eq b` | 相等     |
| `a -ne b` | 不相等   |
| `a -gt b` | 大于     |
| `a -lt b` | 小于     |
| `a -ge b` | 大于等于 |
| `a -le b` | 小于等于 |

3. 字符串比较

| 表达式         | 含义                   |
| -------------- | ---------------------- |
| `str1 = str2`  | 字符串是否相等         |
| `str1 != str2` | 字符串是否不等         |
| `-n str`       | 字符串是否非空         |
| `-z str`       | 字符串是否为空         |
| `str1 \< str2` | 字典序小于（注意转义） |
| `str1 \> str2` | 字典序大于（注意转义） |

```bash
test 1==1;echo $?  --->0表示成立 1表示不成立
```







## 函数

```
declare -F  --->可以查看所有函数
```



### 系统函数

#### 1.basename-->文件名

```
basename [string/pathname] [suffix]
```

> basename是用来获取文件名的函数 , 根据给出的文件路径截取文件名
>
> [string/pathname] 是提供文件路径
>
> suffix : 是截取的时候去掉指定的后缀名--->只获取文件名

#### 2.dirname-->目录名

> 从指定的文件绝对路径 , 去除文件名 , 返回剩下的前缀目录路径

```bash
dirname 绝对路径
```









### 自定义函数

```bash
[ function ] funcname ()  ---->[]表示可有可无
{
	command
	[return 返回值]
}

funcname var1 var2 var3



demo ()
{
echo "nihao"
}
demo

--->nihao


```



#### 区别shell程序与函数

> Shell程序命令 : 运行命令时==开启一个子进程==运行命令
>
> 函数 : 在当前Shell环境中运行 , ==没有==开启进程





## 重定向



### 标准输入

> 从键盘读取用户输入数据 再提供给Shell程序使用

标准输出

> shell程序产生的数据 , 呈现到硬件



### 默认输入输出文件

每个 Unix/Linux 命令运行时都会打开三个文件,  文件如下

| 文件名 | 类型                                  | 文件描述符(file description, fd) | 功能                     |
| ------ | ------------------------------------- | -------------------------------- | ------------------------ |
| stdin  | (standard input)<br>标准输入文件      | 0                                | 获取键盘的输入数据       |
| stdout | (standard output)<br/>标准输出文件    | 1                                | 将正确数据输出到显示器上 |
| stderr | (standard error)<br/>标准错误输出文件 | 2                                | 将错误信息输出到显示器上 |

> 每个文件都有一个唯一的 **文件描述符fd**,  后面会通过唯一 **文件描述符fd** 操作对应的信息

Shell程序操作输入输出时用到这3个文件

1. Shell程序默认会从stdin文件中读取输入数据
2. Shell程序默认会向stdout文件输出正确数据
3. Shell程序默认会项stderr文件中输出错误信息

这3个文件用于临时传输数据使用



### 重定向输入输出介绍

1. 标准输入是数据默认==从键盘流向程序==，如果改变了它的方向，数据就从其它地方流入，这就是输入重定向。

2. 标准输出是数据默认从==程序==流向==显示器==，如果改变了它的方向，数据就流向其它地方，这就是输出重定向。

   > Linux Shell 重定向分为两种，一种输入重定向，一种是输出重定向；



### 重定向语法

| 命令                  | 说明                                                         |
| :-------------------- | :----------------------------------------------------------- |
| 命令 > file           | 将正确数据重定向输出到 file 文件中, ==覆盖==方式             |
| 命令 < file           | 将输入重定向从 file 文件中读取数据                           |
| 命令 >> file          | 将正确数据重定向输出到 file 文件中, 追加方式                 |
| 命令 < file1 > file2  | 从file1文件读取数据, 将结果数据输出到file2文件中             |
| fd是012文件描述符     |                                                              |
| 命令 fd> file         | 根据指定的文件描述符fd 将数据重定向输出到 file 文件中, 覆盖方式 |
| 命令 fd>> file        | 根据指定的文件描述符fd 将数据重定向输出到 file 文件中, 追加方式 |
| 命令 > file fd1>& fd2 | 将 fd1 和 fd2 文件描述符合并 输出到文件。//==必须2前 1后==<br /><br />直接结论  data >>  file  2>&1 |
| fd1<& fd2             | 将 fd1 和 fd2 文件描述符合并 从文件读取输入.                 |
| << tag                | 读取终端输入数据,  将开始标记 tag 和结束标记 tag 之间的内容作为输入。<br>标记名tag可以任意 |

> 在输出重定向中，`>`代表的是覆盖输出，`>>`代表的是追加输出。
>
> fd是文件描述符 
>
> ​		0 通常是标准输入（STDIN），
>
> ​		1 是标准输出（STDOUT），
>
> ​		2 是标准错误输出（STDERR）。
>
> fd>  或  fd>>  中间不可以有空格

输出默认只会把正确的消息写入到文件

除非你加一个fd=2 即

```bash
假如没有这个文件 adddd
如果想把错误结果输入到file
那么直接这样:
ll addd >> file是没用的

必须要添加fd=2的文件描述符

ll addd 2>> file


想要正确&错误的结果都输入到文件中
那就必须fd=2 1都输进去

ll addd >> log.txt 2>>$1

一行一行读取

while read str; do echo $str; done < file
```





### 搭配wc使用

```bash
获取文件行数
wc -l < file

获取字符数
wc -c < file
```







## 实用

### cut

> 使用cut可以切割提取指定列 / 字符 / 字节 的数据

#### 语法

```shell
cut [options]  filename
```



options参数说明

| 选项参数        | 功能                                                         |
| --------------- | ------------------------------------------------------------ |
| -f 提取范围     | 列号，获取第几列                                             |
| -d 自定义分隔符 | 自定义分隔符，默认为制表符。                                 |
| -c 提取范围     | 以字符为单位进行分割                                         |
| -b 提取范围     | 以字节为单位进行分割。这些字节位置将忽略多字节字符边界，除非也指定了 -n 标志。 |
| -n              | 与“-b”选项连用，==不分割==多字节字符；                       |

提取范围说明

| 提取范围  | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| n-        | 提取指定第n列或字符或字节后面==所有数据==                    |
| n-m       | 提取指定第n列或字符或字节到第m列或字符或字节==中间的所有数据== |
| -m        | 提取指定第m列或字符或字节==前面所有数据==                    |
| n1,n2,... | 提前指定枚举列的所有数据                                     |



## sed

#### 语法

```sehll
sed [选项] '命令' 文件名

sed 's/旧/新/'      # 替换（默认只替换每行第一个）
sed 's/旧/新/g'     # 替换所有
sed '2d'           # 删除第2行
sed '/模式/d'      # 删除匹配的行
sed '3a\内容'      # 第3行后添加内容  append
sed '2i\内容'      # 第2行前插入内容  insert
sed '4c\新内容'    # 修改第4行为新内容
```

选项参数说明

| 选项参数                   | 功能                                                         |
| -------------------------- | ------------------------------------------------------------ |
| `-e`                       | 直接在指令列模式上进行sed的动作编辑。它告诉sed将下一个参数解释为一个sed指令，只有当命令行上给出多个sed指令时才需要使用-e选项;一行命令语句可以执行多条sed命令 |
| `-i`                       | 直接对内容进行修改，不加-i时默认只是预览，不会对文件做实际修改 |
| `-f`                       | 后跟保存了sed指令的文件                                      |
| `-n`                       | 取消默认输出，sed默认会输出所有文本内容，使用-n参数后只显示处理过的行 |
| `-r ruguler              ` | 使用扩展正则表达式，默认情况sed只识别基本正则表达式 *        |



sed程序命令功能描述

| 命令 | 功能描述                                      |
| ---- | --------------------------------------------- |
| `a`  | add新增，a的后面可以接字串，在下一行出现      |
| `c`  | change更改, 更改匹配行的内容                  |
| d    | delete删除, 删除匹配的内容                    |
| `i`  | insert插入, 向匹配行前插入内容                |
| `p`  | print打印, 打印出匹配的内容，通常与-n选项和用 |
| s    | substitute替换, 替换掉匹配的内容              |
| `=`  | 用来打印被匹配的行的行号                      |
| `n`  | 读取下一行，遇到n时会自动跳入下一行           |

特殊符号

| 命令                | 功能描述                                                     |
| ------------------- | ------------------------------------------------------------ |
| `!`                 | 就像一个sed命令，放在限制条件后面, 对指定行以外的所有行应用命令(取反) |
| {sed命令1;sed命令2} | 多个命令操作同一个的行                                       |
