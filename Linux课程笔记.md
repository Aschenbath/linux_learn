# Linux基础命令



## Linux的目录结构

![image-20221027214128453](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027214128.png)

- `/`，根目录是最顶级的目录了
- Linux只有一个顶级目录：`/`
- 路径描述的层次关系同样适用`/`来表示
- /home/itheima/a.txt，表示根目录下的home文件夹内有itheima文件夹，内有a.txt

出现在开头就是==根目录== , 否则就是==层级关系==


命令行为 + 选项 + 命令参数

command  + option + parameter





linux系统输入密码是不会有密码符显示的 , 所以只管输入吧

切换到root用户 su - root
用exit退出或者logout







## 快捷键

1. ctrl + l 清空屏幕 == clear	

2. ctrl + c 强制停止 / 退出当前命令的输入

3. ctrl + d 退出 

4. history

5. python

6. !前缀    自动执行上一次执行的命令  ---------->找近期的

7. ctrl r ----->加想要找到命令

8. ctrl a 跳到当前行命令的开头

   1. ctrl e 跳到命令行的结尾

9. ctrl 键盘左键 向左跳一个单词

10. ctrl 键盘右键 向右跳一个单词

    

    



















## ls命令

功能：列出文件夹信息

语法：`ls [-l -h -a] [参数]`

- 参数：被查看的文件夹，不提供参数，表示查看当前工作目录
  - -l，以==列表竖向==形式查看------------->==list==

- -h，配合-l，以更加人性化的方式显示文件大小----------->==必须配合l==
- -a，显示隐藏文件==(all)==

命令本体是平铺展示当前目录下的选项


可以==组合使用==

ls -l-a  
 ls -la  
ls -al





### 隐藏文件、文件夹

在Linux中==以`.`开头==的，均是==隐藏==的。

默认不显示出来，需要`-a`选项才可查看到。







## pwd命令

功能：展示当前工作目录------->相当于提供==绝对路径==

语法：`pwd`





## cd命令

功能：切换工作目录

语法：`cd [目标目录]`

参数：目标目录，要切换去的地方，==不提供参数==默认切换到`当前登录用户HOME目录`

/是根目录

绝对路径以==根目录==为起点

相对路径以==当前目录==为起点

./ 指的是当前目录

.. 表示上一级目录

cd ../.. 表示上上一级目录

cd ~ 表示回到home目录---->回到分叉路口





## HOME目录

每一个用户在Linux系统中都有自己的专属工作目录，称之为HOME目录。

- 普通用户的HOME目录，默认在：`/home/用户名`

- root用户的HOME目录，在：`/root`



FinalShell登陆终端后，默认的工作目录就是用户的HOME目录







## 相对路径、绝对路径

- 相对路径，==非==`/`开头的称之为相对路径

  相对路径表示以`当前目录`作为起点，去描述路径，如`test/a.txt`，表示当前工作目录内的test文件夹内的a.txt文件

- 绝对路径，==以==`/`开头的称之为绝对路径

  绝对路径从`根`开始描述路径



## 特殊路径符

- `.`，表示当前，比如./a.txt，表示当前文件夹内的`a.txt`文件
- `..`，表示上级目录，比如`../`表示上级目录，`../../`表示上级的上级目录
- `~`，表示用户的==HOME目录==，比如`cd ~`，即可切回用户HOME目录



## mkdir命令

功能：创建文件夹 ( make directory)

语法：`mkdir [-p] 参数`

- 参数：被创建文件夹的路径
- 选项：-p，可选，表示创建==前置==路径

mkdir  /home/nash/newone   -------->表示在nash下创建

mkdir  ../newone--------------->表示在上级目录创建

mkdir  ~/newone----------------->home目录创建文件夹



加-p是为了创建嵌套文件夹的深层文件 -->嵌套文件夹中存在没创建的-->自动创建不存在的父目录

mkdir -p /home/nash/newone/newone1





## touch命令

功能：创建文件

语法：`touch 参数`

- 参数：被创建的文件路径

touch /home/nash/newone------>创建





## cat命令

功能：查看文件内容

语法：`cat 参数`

- 参数：被查看的文件路径

cat /home/nash/newone/test.txt-------------->查看文件内容






## more命令

功能：查看文件，可以支持==翻页==查看

语法：`more 参数`

- 参数：被查看的文件路径
- 在查看过程中：
  - `空格`键==翻页==
  - `q`退出查看 ==quit==









## cp命令

功能：复制文件、文件夹

语法：`cp [-r] 参数1 参数2`

- 参数1，被复制的
- 参数2，要复制去的地方
- 选项：-r，可选，==复制文件夹==使用

示例：

- cp a.txt b.txt，复制当前目录下a.txt为b.txt
- cp a.txt test/，复制当前目录a.txt到test文件夹内
- cp -r test test2，复制文件夹test到当前文件夹内为test2存在

cp -r nice nice2







## mv命令

功能：移动文件、文件夹

语法：`mv 参数1 参数2`

- 参数1：被移动的

- 参数2：要移动去的地方，参数2如果不存在，则会将待移动的文件 进行 改名


  mv  test.txt  test1.txt------------>如果不存在test1.txt , 文件 test.txt直接改名为test1.txt









## rm命令

功能：删除文件、文件夹

语法：`rm [-r -f] 参数...参数`

- 参数：支持多个，每一个表示被删除的，空格进行分隔
- 选项：-r，==删除文件夹==使用
- 选项：-f，==强制删除==，不会给出确认提示，一般root用户会用到



> rm命令很危险，一定要注意，特别是切换到root用户的时候。

通配符 *
test* 表示匹配任何以test开头的

*test表示匹配任何以test结尾的
 *test  *表示匹配任何包含test的

千万别执行
rm -rf /

rm -rf /*  等价于windows C盘格式化







## which命令

功能：查看==命令的程序本体文件路径==

语法：`which 参数`

- 参数：被查看的命令



Linux命令本体都是二进制可执行程序
和windows的exe文件是一个意思

我们可以通过which查考一系列命令的程序文件存放在哪里

which cd

which pwd

which ls













## find命令

功能：搜索文件

语法1按文件名搜索：

1. `find 路径 -name 参数`
   2. find 路径 -size +-n单位  KMG

- 路径，搜索的起始路径
- 参数，搜索的关键字，支持通配符*， 比如：`*`test表示搜索任意以test结尾的文件

find 起始路径 -name "路径名"



为了搜索到最多的文件 , 我们切换到root获得最大权限

su - root 



​	find  起始路径  -size +-n单位

​	+, -分别表示大于小于

​	n表示大小













## grep命令

功能：过滤关键字----------------->提取关键字

语法：`grep [-n] 关键字 文件路径`

- 选项-n，可选，表示在结果中==显示匹配的行的行号==。
- 参数，关键字，必填，表示过滤的关键字，带有空格或其它特殊符号，建议使用==” ”==将关键字包围起来
- 参数，文件路径，必填，表示要过滤内容的文件路径，可作为内容输入端口



> 参数文件路径，可以作为管道符的输入



![image-20250527130928810](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250527130928810.png)













## wc命令

功能：统计

语法：`wc [-c -m -l -w] 文件路径`

- 选项，-c，统计bytes数量
- 选项，-m，统计字符数量------- 
- 选项，-l，统计行数 -------->line
- 选项，-w，统计单词数量 --- >word count
- 参数，文件路径，被统计的文件，可作为内容输入端口



> 参数文件路径，可作为管道符的输入













## 管道符|

写法：`|`

功能：将符号==左边的结果==，作为符号==右边的输入==

示例：

`cat a.txt | grep itheima`，将cat a.txt的结果，作为grep命令的输入，用来过滤`itheima`关键字



可以支持嵌套：

`cat a.txt | grep itheima | grep itcast`



![image-20250527131743547](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250527131743547.png)



这样wc / grep就可以省略后面的路径名

![image-20250527132419037](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250527132419037.png)



![image-20250527132507744](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250527132507744.png)



嵌套使用

![image-20250527133220746](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250527133220746.png)











## echo命令

功能：输出内容--- == print

语法：`echo 输出内容`

- 参数：被输出的内容

可以使用echo命令在命令行内输出指定内容

复杂内容看以用 ==" " 包围==

![image-20250527140511285](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250527140511285.png)











## `反引号

功能：被两个反引号包围的内容，会作为命令执行

示例：

- echo \`pwd\`，会输出当前工作目录



echo `命令`---->打印命令的内容



被包围的内容不会被当成普通的文本 , 而是被作为命令执行 



嵌套使用

![image-20250527142342663](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250527142342663.png)





## tail命令

功能：查看文件==尾部==内容---->默认查看10行

语法：`tail [-f] 参数`

- 参数：被查看的文件
- 选项：-f，持续跟踪文件修改--->追加后会再次显示追加到内容



tail test.txt

tail -num test.txt--->默认查看几行







## head命令

功能：查看文件头部内容

语法：`head [-n] 参数`

- 参数：被查看的文件
- 选项：-n，查看的行数













## 重定向符

功能：将符号==左边的结果==，==输出==到==右边==指定的文件中去

- `>`，表示覆盖输出  --->会把之前的覆盖掉
- `>>`，表示追加输出 ---->追加到文本中 











## VIM 编辑器

| 命令 | 类型                 | 含义             | 结果                   |
| ---- | -------------------- | ---------------- | ---------------------- |
| `$`  | motion（动作命令）   | 移动到当前行末尾 | 光标跳到行末           |
| `d`  | operator（操作命令） | 删除             | 等待你指定要删哪段     |
| `d$` | operator + motion    | 删除到行末       | 删除光标到行尾这段文字 |

### 基本流程

1. i 进入编辑模式

2. a 对当前行进行append

3.  h j k l 左下上右

4. d+w 删除单词以及后面的空格

5. de删除单词但是保留后面的空格

6. | 命令 | 名称 | 含义                            | 举例说明                           |
   | ---- | ---- | ------------------------------- | ---------------------------------- |
   | `w`  | word | 跳到 **下一个单词的开头**       | 从 `hello` 跳到 `world`            |
   | `e`  | end  | 跳到 **当前或下一个单词的末尾** | 从 `hello` 跳到 `o` 或下个词的末尾 |

   

7. d$ 删除光标后半行的所有内容

8. dd删除当前行

9. p表示粘贴上一次dd删除的那一行

10. r+字母 表示将光标下一个字母换成字母

11. `cw` 是删除到“单词边界”（包含分隔符，比如空格）；

    `ce` 是删除到“单词结尾”（更细致地停在字母尾部）。







#### 1.打开文件

```bash
vim 文件名
```

#### 2.按 `i` 进入 **插入模式**

（Insert）开始打字

现在你可以像正常编辑器一样输入内容。

#### 3.编辑完后按 `Esc`，

回到 **普通模式**（Normal）, 你现在不能打字了，但可以用键盘控制光标、删除、复制、粘贴等。

#### 4.输入命令（进入命令模式）

在普通模式下输入 `:`（冒号），你会看到光标跑到左下角，这时可以：

| 命令  | 功能               |
| ----- | ------------------ |
| `:w`  | 保存文件           |
| `:q`  | 退出文件           |
| `:wq` | 保存并退出         |
| `:q!` | 强制退出（不保存） |
| `:x`  | 同 `:wq`           |

normal模式下的常用快捷键

| 快捷键     | 功能                  |
| ---------- | --------------------- |
| `h j k l`  | 左 下 上 右（方向键） |
| `dd`       | 删除整行              |
| `yy`       | 复制整行              |
| `p`        | 粘贴                  |
| `/关键词`  | 向下搜索              |
| `n/N`      | 搜索结果下一个/上一个 |
| `u`        | 撤销                  |
| `Ctrl + r` | 反撤销                |



- 进入 Vim 不会编辑？按 `i`
- 无法退出？按 `Esc` 再输入 `:q`
- 打错一堆？按 `u` 撤销
- 粘贴出错？用 `p` 试试光标之后粘贴



### 命令模式快捷键

![image-20221027215841573](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027215841.png)

![image-20221027215846581](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027215846.png)

![image-20221027215849668](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027215849.png)









### 底线命令快捷键

![image-20221027215858967](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027215858.png)













## 命令的选项

我们学习的一系列Linux命令，它们所拥有的选项都是非常多的。

比如，简单的ls命令就有：-a -A -b -c -C -d -D -f -F -g -G -h -H -i -I -k -l -L -m -n -N -o -p -q -Q -r-R -s -S -t -T -u -U -v -w -x -X -1等选项，可以发现选项是极其多的。

课程中， 并不会将全部的选项都进行讲解，否则，一个ls命令就可能讲解2小时之久。

课程中，会对常见的选项进行讲解， 足够满足绝大多数的学习、工作场景。













### 查看命令的帮助

可以通过：`命令 --help`查看命令的帮助手册

![image-20221027220005610](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220005.png)

### 查看命令的详细手册

可以通过：`man 命令`查看某命令的详细手册

![image-20221027220009949](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220010.png)









# Linux常用操作

## 软件安装

- CentOS系统使用：
  - yum [install remove search] [-y] 软件名称
    - install 安装
    - remove 卸载
    - search 搜索
    - -y，自动确认
- Ubuntu系统使用
  - apt [install remove search] [-y] 软件名称
    - install 安装
    - remove 卸载
    - search 搜索
    - -y，自动确认

> yum 和 apt 均需要root权限











## systemctl

system control

功能：控制系统服务的启动关闭等

语法：`systemctl start | stop | restart | disable | enable | status 服务名`

- start，启动
- stop，停止
- status，查看状态
- disable，关闭开机自启
- enable，开启开机自启
- restart，重启

```vim
systemctl status app

```

部分软件安装后自动集成到systemctl种 , 所以可以命令行安装









## 软链接

功能：创建文件、文件夹软链接（快捷方式）

语法：`ln -s 参数1 参数2`

- 参数1：被链接的
- 参数2：要链接去的地方（快捷方式的名称和存放位置）



## 日期

语法：`date [-d] [+格式化字符串]`

- -d 按照给定的字符串显示日期，一般用于日期计算

- 格式化字符串：通过特定的字符串标记，来控制显示的日期格式
  - %Y   年%y   年份后两位数字 (00..99)
  - %m   月份 (01..12)
  - %d   日 (01..31)
  - %H   小时 (00..23)
  - %M   分钟 (00..59)
  - %S   秒 (00..60)
  - %s   自 1970-01-01 00:00:00 UTC 到现在的秒数



示例：

- 按照2022-01-01的格式显示日期

  ![image-20221027220514640](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220514.png)

- 按照2022-01-01 10:00:00的格式显示日期

  ![image-20221027220525625](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220525.png)

- -d选项日期计算

  ![image-20221027220429831](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220429.png)

  - 支持的时间标记为：

    ![image-20221027220449312](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220449.png)





## 时区

修改时区为中国时区

![image-20221027220554654](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027220554.png)



## ntp

功能：同步时间

安装：`yum install -y ntp`

启动管理：`systemctl start | stop | restart | status | disable | enable ntpd`



手动校准时间：`ntpdate -u ntp.aliyun.com`



## ip地址

格式：a.b.c.d

- abcd为0~255的数字



特殊IP：

- 127.0.0.1，表示本机
- 0.0.0.0
  - 可以表示本机
  - 也可以表示任意IP（看使用场景）



查看ip：`ifconfig`



## 主机名

功能：Linux系统的名称

查看：`hostname`

设置：`hostnamectl set-hostname 主机名`



## 配置VMware固定IP

1. 修改VMware网络，参阅PPT，图太多

2. 设置Linux内部固定IP

   修改文件：`/etc/sysconfig/network-scripts/ifcfg-ens33`

   示例文件内容：

   ```shell
   TYPE="Ethernet"
   PROXY_METHOD="none"
   BROWSER_ONLY="no"
   BOOTPROTO="static"			# 改为static，固定IP
   DEFROUTE="yes"
   IPV4_FAILURE_FATAL="no"
   IPV6INIT="yes"
   IPV6_AUTOCONF="yes"
   IPV6_DEFROUTE="yes"
   IPV6_FAILURE_FATAL="no"
   IPV6_ADDR_GEN_MODE="stable-privacy"
   NAME="ens33"
   UUID="1b0011cb-0d2e-4eaa-8a11-af7d50ebc876"
   DEVICE="ens33"
   ONBOOT="yes"
   IPADDR="192.168.88.131"		# IP地址，自己设置，要匹配网络范围
   NETMASK="255.255.255.0"		# 子网掩码，固定写法255.255.255.0
   GATEWAY="192.168.88.2"		# 网关，要和VMware中配置的一致
   DNS1="192.168.88.2"			# DNS1服务器，和网关一致即可
   ```





程序运行即进程 , 且每个进程有独有的进程ID

## ps命令

功能：查看进程信息

语法：`ps -ef`，查看全部进程信息，可以搭配grep做过滤：`ps -ef | grep xxx`



![image-20250528103233704](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250528103233704.png)





PID进程号 







## kill命令

![image-20221027221303037](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221303.png)



```vim
kill -9 进程id           (-9强制关进程)
```

![image-20250528104008171](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250528104008171.png)

第一列是进程号





查看端口占用 nmap netstat

## nmap命令

![image-20221027221241123](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221241.png)

```vim
nmap ip
```





## netstat命令

功能：查看端口占用

用法：`netstat -anp | grep xxx`

```vim
netstat -anp | grep xxx
```







## ping命令

测试网络是否联通

语法：`ping [-c num] 参数`

![image-20221027221129782](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221129.png)



```vim
ping -c num 域名  (查看是否连通)
```

















## wget命令

![image-20221027221148964](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221149.png)



```vim
wget -b url (url下载链接)    
-f持续跟踪
```













## curl命令

![image-20221027221201079](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221201.png)

![image-20221027221210518](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221210.png)



```
curl -O url  (-大O) --------------->下载

cip.cc获取我的主机的公网ip
```

![image-20250528100956193](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250528100956193.png)













## top命令

功能：查看主机运行状态

语法：`top`，查看基础信息



![image-20250528104342013](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250528104342013.png)



us : user 

sy : system



![image-20250528104930618](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250528104930618.png)



可用选项：

![image-20221027221340729](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221340.png)



交互式模式中，可用快捷键：

![image-20221027221354137](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221354.png)













## df命令

查看磁盘占用

![image-20221027221413787](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221413.png)



## iostat命令

查看CPU、磁盘的相关信息

![image-20221027221439990](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221440.png)

![image-20221027221514237](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221514.png)

rkb读

wkb写

util--->磁盘利用率





## sar命令

查看==网络统计==

![image-20221027221545822](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221545.png)

```vim
sar -n DEV num1 num2
```









## 环境变量

- 临时设置：export 变量名=变量值
- 永久设置：
  - 针对用户，设置用户HOME目录内：`.bashrc`文件
  - 针对全局，设置`/etc/profile`

![image-20250528121720452](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250528121720452.png)











### PATH变量

记录了执行程序的搜索路径

可以将自定义路径加入PATH内，实现自定义命令在任意地方均可执行的效果



![image-20250528122427855](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250528122427855.png)

注意这里是  美元PATH:  而不是直接赋值









## $符号

可以取出==指定的环境变量==的值

语法：`$变量名`

示例：

`echo $PATH`，输出PATH环境变量的值

`echo ${PATH}ABC`，输出PATH环境变量的值以及ABC

如果变量名和其它内容混淆在一起，可以使用${}

















## 压缩解压

### 压缩 

tar       gzip

`tar -zcvf 压缩包 被压缩1...被压缩2...被压缩N`

- -z表示使用gzip，可以不写



`zip [-r] 参数1 参数2 参数N`

![image-20221027221906247](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221906.png)



![image-20250528124336637](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250528124336637.png)



.gz才有体积压缩的功能



### 解压

`tar -zxvf 被解压的文件 -C 要解压去的地方`

- -z表示使用gzip，可以省略
- -C，可以省略，指定要解压去的地方，不写解压到当前目录







`unzip [-d] 参数`

![image-20221027221939899](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027221939.png)





## su命令

切换用户 switch user

语法：`su [-] [用户]`

![image-20221027222021619](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222021.png)

ctrl + d切换到上一个

exit退出root







## sudo命令

![image-20221027222035337](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222035.png)



比如：

```shell
itheima ALL=(ALL)       NOPASSWD: ALL //注意这里是NOPASSWD
```

在visudo内配置如上内容，可以让itheima用户，无需密码直接使用`sudo`



## chmod命令

修改==文件、文件夹==权限

仅限==root/当前用户==

语法：`chmod [-R] 权限 参数`

- 权限，要设置的权限，比如755，表示：`rwxr-xr-x`

  ![image-20221027222157276](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222157.png)

- 参数，被修改的文件、文件夹

- 选项==-R==，设置文件夹和其内部全部内容一样生效---->==对全部文件生效==

  u->user
  g->group

  o->other
  ==rwx==



chmod +x/+r/+w filename

chmod u=r,g=w,o=x filename

u=---,g=---,o=--- 



chmod -R u=r,g=w,o=x filename--------------->文件都变成这个权限



rwx--->111 100 000 ---------->三位二进制

751 rwx  r-x  --x







## chown命令

修改文件、文件夹==所属==的 用户、组

想把自己的文件丢给别人 , 先要争得别人的同意 

所以能随便丢给别人的只有root用户

语法：`chown [-R] [用户][:][用户组] 文件或文件夹`

![image-20221027222326192](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222326.png)







## 用户组管理

![image-20221027222354498](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222354.png)











## 用户管理

![image-20221027222407618](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222407.png)

​	









## genenv命令

- `getenv group`，查看系统全部的用户组

  ![image-20221027222446514](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222446.png)

- `getenv passwd`，查看系统全部的用户

  ![image-20221027222512274](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027222512.png)



## env命令

查看系统全部的环境变量

语法：`env`

​		



## export命令







```vim
export name = sth
echo $name
sth
```



但是export只是暂时保存

如果想要永久保存 

那就用vim 将想要保存到变量 写进 ==.bashrc==文件 , 然后就保存

==写完之后一定要刷新== .bashrc 

```vim
source .bashrc
或者
. .bashrc
```











## rz命令

上传文件--->打开图形化文件界面--->慢



直接拖拽快一点





## sz命令

下载文件 













## tar命令

打包

`c`：创建压缩包（create）

`x`：解压压缩包（extract）

`t`：查看压缩包内容（list）

`v`：显示过程（verbose）

`f`：指定文件名（file） ---->必须在指令的结尾

`z`：使用 gzip 压缩（.gz）

`j`：使用 bzip2 压缩（.bz2）

`J`：使用 xz 压缩（.xz）

`-C` : 指定路径 单独使用

```bash
tar [选项] [压缩包名称] [要打包的文件或目录]4

tar -cvf newone.tar filepath  打包
tar -zxvf test.tar.gz -C towhich 以gz模式解压至当前目录
tar -xvf newone.tar -C towhich 

```

######  小记口诀：

> **"c 打包，x 解包，v 啰嗦，f 文件名，z 压缩"**
>  搭配顺序记：`tar -czvf` 是压缩，`tar -xzvf` 是解压。



```
# 打包文件夹为 .tar（仅打包不压缩）
tar -cvf archive.tar myfolder/

# 解压 .tar 包
tar -xvf archive.tar

# 打包为 .tar.gz（gzip压缩）
tar -czvf archive.tar.gz myfolder/

# 解压 .tar.gz
tar -xzvf archive.tar.gz




# 打包为 .tar.bz2（bzip2压缩）
tar -cjvf archive.tar.bz2 myfolder/

# 解压 .tar.bz2
tar -xjvf archive.tar.bz2



# 打包为 .tar.xz（xz压缩）
tar -cJvf archive.tar.xz myfolder/

# 解压 .tar.xz
tar -xJvf archive.tar.xz



# 查看压缩包内容（不解压）
tar -tvf archive.tar.gz

# 解压到指定目录
tar -xvf archive.tar.gz -C /path/to/target/



# 打包多个文件与文件夹
tar -czvf archive.tar.gz file1.txt file2.txt folder/

# 打包时排除某些文件（如排除 .log 文件）
tar --exclude="*.log" -czvf archive.tar.gz folder/

```





## zip命令

```bash
zip [-r] newone.zip 被压缩的参数1~n
unzip 参数 [-d towhich]
```











## 认识权限信息

权限细节10个槽位    文件 - or文件夹 d /  ==用户==权限  / ==用户组==权限 / 其他用户权限


![image-20250527190818489](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250527190818489.png)



rwx  读,查看  /  写,修改  /  执行









## 安装APP

使用命令行装app

yum程序  自动化安装配置linux软件

RPM包--->centOS的并发版linux系统的安装包





语法 

```vim
yum [-y] [install] || remove || search
-y默认允许
```



yum -y search appname



ubuntu 的安装包 deb , apt

```vim
apt -y install wget
```





## 软连接

将文件,文件夹连接到其他位置---->相当于==桌面快捷方式==



ln   -s(表示软连接)  被链接的文件 目的地















## 日期和时区





| 格式符 | 含义                        | 示例         |
| ------ | --------------------------- | ------------ |
| `%Y`   | **四位年份**                | `2025`       |
| `%y`   | **两位年份**                | `25`         |
| `%m`   | **两位数字月份（01-12）**   | `05`         |
| `%B`   | **完整月份英文**            | `May`        |
| `%b`   | **缩写月份英文**            | `May`        |
| `%d`   | **两位日期**                | `27`         |
| `%e`   | **不补零日期**              | ` 7` or `27` |
| `%H`   | **24小时制的小时（00-23）** | `22`         |
| `%I`   | **12小时制的小时（01-12）** | `10`         |
| `%p`   | **AM/PM**                   | `PM`         |
| `%M`   | **分钟（00-59）**           | `04`         |
| `%S`   | **秒（00-59）**             | `15`         |
| `%A`   | **星期几（英文全称）**      | `Tuesday`    |
| `%a`   | **星期几（英文缩写）**      | `Tue`        |
| `%Z`   | **时区缩写**                | `CST`        |



```bash
date -d "now + 1 day"
date -d "now - 3 hours"
date -d "2 days ago"
date -d "next Monday"
date -d "tomorrow 13:00"
```





## IP地址 主机名

127.0.0.1----------->此IP是本机

0.0.0.0--------->可以代表本机

hostnamectl set-hostname newname

dns域名解析

过程 : 1. 先查看本机的记录 私人地址本---->所以我们可以通过添加本地的映射
 ip + 主机名  直接找本机

2. 再联网去DNS服务器查询

   linux看  /etc/hosts





## 固定IP



1. 频繁变化会要求我们频繁修改适配很麻烦
2. 进行了ip和主机名的映射 , 如果ip频繁修改 , 要重新更新映射关系







## 端口

物理端口 : 接口

虚拟端口 : 不可见的 , 电脑对应的app程序号65535
1~1023知名程序

1024~49151注册端口 , 通常允许随意使用

49152~65535动态端口 , 通常不会固定绑定程序 , 程序对外进行网络连接时 , 用于临时使用







## 





















| 名称     | 含义                                           | 举例                     |
| -------- | ---------------------------------------------- | ------------------------ |
| `mysql`  | 是客户端程序，用来连接数据库                   | `mysql -u root -p`       |
| `mysqld` | 是守护进程（daemon），真正跑在后台的数据库服务 | `systemctl start mysqld` |







## alias 别名命令

自定义命令别名

首先用vim进入.bashrc文件

```vim
vim .bashrc
```



然后用alias命令 添加别名

```vim
alias cls = 'clear'
```



然后重新加载.bashrc

```vim
. .bashrc
// source .bashrc
```



然后就能用了







## shuf

生成随机数

```vim
shuf [-i] l-r -n number         --> -i 表示范围  -n表示生成个数
```



当我们想要让命令输出的结果赋值给变量的时候有2种

```vim
number = ` shuf -i 1-10 -n 1 `        --->反引号
或者
number = $ (shuf -i 1-10 -n 1)        -->dollar()
```





# linux文件系统

### 分类

| 符号 | 类型              | 含义说明                   | 示例                               |
| ---- | ----------------- | -------------------------- | ---------------------------------- |
| `-`  | 普通文件          | 文本、二进制、脚本等       | `/etc/passwd`, `a.out`, `hello.sh` |
| `d`  | 目录（directory） | 文件夹                     | `/home/`, `/etc/`                  |
| `l`  | 符号链接（link）  | 类似快捷方式               | `myfile -> /etc/passwd`            |
| `c`  | 字符设备文件      | 一次传输一个字符的设备接口 | `/dev/tty`, `/dev/random`          |
| `b`  | 块设备文件        | 块方式读写，如磁盘、U盘    | `/dev/sda`, `/dev/sr0`             |
| `s`  | 套接字文件        | 用于进程间通信（IPC）      | `/run/docker.sock`                 |
| `p`  | 命名管道（FIFO）  | 用于进程间单向通信         | 用 `mkfifo mypipe` 创建的管道      |



