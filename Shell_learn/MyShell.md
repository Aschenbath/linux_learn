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

```





1. `elif` 是 `else if` 的缩写，Shell 里必须用它。

2. `then` 是 **必须的关键字**，每个 `if` 和 `elif` 后都要带。

3. `[[]]` 里面 **空格必须有**，比如 `[[ $a -eq $b ]]`。

4. `number=$(shuf -i 1-50 -n 1)`，中间 **不能有空格**，不然 Shell 会误解。



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







#### 比较运算符

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













