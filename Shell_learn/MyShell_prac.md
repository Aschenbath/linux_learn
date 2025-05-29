# MyShell_prac







## pracone : pushgogo

###  方法一 : 

> 先写好shell脚本 , 然后通过bat批处理文件启动shell脚本

#### 1.`.bat` 文件？

`.bat`（batch）文件是一种**Windows 批处理脚本文件**，作用就像是：

> “你本来要一条条打在 CMD（命令行）里的指令，我帮你全写进去，双击一下就全执行了。”



#### 2. 功能

你可以用 `.bat` 文件来：

- 自动执行 Shell 脚本（如 autopush.sh）
- 打开指定文件或软件
- 自动拷贝/移动文件
- 编译代码、运行程序
- 启动服务器或本地服务
- 一键配置开发环境
- 自动提交 Git 项目（比如你现在做的）



#### 3.编写

```bash
@echo off
REM 注释：不执行这行，只是说明用的
命令1
命令2
命令3

例如:
@echo off
bash -c "~/autopush.sh"  --->bash -c "..."：调用 Git Bash 来执行你写的 Shell 脚本。
```

##### 保存方法

1. 打开 **记事本**
2. 写完内容
3. 点击【文件 → 另存为】
4. 文件名写 `xxx.bat`（注意：**别加 `.txt` 后缀！**）
5. 编码格式选 ANSI 或 UTF-8，无 BOM
6. 选择保存位置（比如放到 `C:\Users\你的用户名\`）





#### 4.设为环境变量

> 把 `.bat` 文件放在一个固定的目录，比如 `C:\Users\aschenbath\jioben`
>
> 添加这个目录到环境变量：
>
> - Win + S 搜“环境变量”
>
> - 找“系统变量”中的 `Path`
>
> - 点【编辑】→【新建】→ 添加你放脚本的路径
>
> - 确认 → 重新打开 CMD
>
> - 然后你就能随时在终端里输入脚本名，比如：
>
>   ```bash
>   pushgogo
>   ```





###### 检查

> where pushgogo ---->linux里是
>
> 如果返回路径则表示配置成功





#### 5.总结流程

1. **脚本路径**：`C:\Users\aschenbath\autopush.sh`
2. **bat 文件**：`C:\Users\aschenbath\pushgogo.bat`
3. **环境变量里加入了**：`C:\Users\aschenbath`
4. **然后你就能在任意 CMD 输入**：

```bash
pushgogo
```



```bash
pushgogo.bat
@echo off
echo start...

wsl bash -c "eval \$(ssh-agent -s) && ssh-add ~/.ssh/id_ed25519 && cd /mnt/f/linux_learn && git add . && git commit -m 'auto commit' || echo '无需提交' && git push"

echo.
echo "over, i love u three thousand times"
pause
```





```bash
withbat.sh （核心 Shell 脚本）
#!/bin/bash
# 启动 SSH 代理，开启身份验证守护进程，像一把守护你的密钥的利剑
eval "$(ssh-agent -s)"

# 向代理添加你的私钥，让后续的 git 操作拥有无声的通行证
ssh-add ~/.ssh/id_ed25519

# 切换到你代码的根目录，失败则立刻退出，绝不容忍迷失方向
cd /mnt/f/linux_learn || exit 1

# 把所有改动放入暂存区，准备好迎接历史的书写
git add .

# 自动提交，携带着当下时间的印记，像时光流逝的签名
git commit -m "auto commit $(date '+%Y-%m-%d %H:%M:%S')"

# 将你的代码推送到远方的仓库，连接你与世界的桥梁
git push




批处理文件 （Windows 端启动脚本）
@echo off
:: 关闭命令回显 , 即不显示echo等命令

echo.
echo start...
echo.
:: 打印空行

wsl /mnt/c/Users/aschenbath/withbat.sh
:: 在 WSL 环境中执行 Linux 下的提交脚本，跨越系统的边界如行云流水

echo.
echo.
echo "over, i love u three thousand times"
echo.
:: 结束语，诗意地告诉你任务已完成，感情满满

pause
:: 暂停，等待你的掌声或任意按键，告别静默
```





### 小keys

```bash
echo off 是关闭命令回显的意思，执行命令时不会再显示命令本身。
@echo off @命令 表示这条命令也不显示
```





### 方法二 : 

> 直接编写bat文件 然后加入全局变量执行
>
> 不推荐 , 代码如下

```bash
@echo off
echo start...

wsl bash -c "eval \$(ssh-agent -s) && ssh-add ~/.ssh/id_ed25519 && cd /mnt/f/linux_learn && git add . && git commit -m 'auto commit' || echo '无需提交' && git push"

echo.
echo "over, i love u three thousand times"
pause
```





## practwo : autopush

### 1.写好autopush.sh

```bash
#!/bin/bash

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

git add .
git commit -m "自动提交$(date '+%Y-%m-%d %H:%M:%S')"
git push
```



### 2.加入任务计划程序

![image-20250529154551754](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250529154551754.png)





![image-20250529154613461](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250529154613461.png)



![image-20250529154655940](C:\Users\aschenbath\AppData\Roaming\Typora\typora-user-images\image-20250529154655940.png)
