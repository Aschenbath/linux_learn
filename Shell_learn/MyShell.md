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
/etc/profile
    ↳ /etc/profile.d/*.sh （可能由 /etc/profile 引用）
~/.bash_profile
    ↳ ~/.bash_login
    ↳ ~/.profile
```



shell非登陆环境-->只执行命令不需要用户的参与

```
~/.bashrc
```
