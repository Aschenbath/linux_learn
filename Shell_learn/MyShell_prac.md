# MyShell_prac





## 1.利用cmd直接pushgogo

##  

### 1.`.bat` 文件？

`.bat`（batch）文件是一种**Windows 批处理脚本文件**，作用就像是：

> “你本来要一条条打在 CMD（命令行）里的指令，我帮你全写进去，双击一下就全执行了。”



### 2. 功能

你可以用 `.bat` 文件来：

- 自动执行 Shell 脚本（如 autopush.sh）
- 打开指定文件或软件
- 自动拷贝/移动文件
- 编译代码、运行程序
- 启动服务器或本地服务
- 一键配置开发环境
- 自动提交 Git 项目（比如你现在做的）



### 3.编写

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

#### 保存方法

1. 打开 **记事本**
2. 写完内容
3. 点击【文件 → 另存为】
4. 文件名写 `xxx.bat`（注意：**别加 `.txt` 后缀！**）
5. 编码格式选 ANSI 或 UTF-8，无 BOM
6. 选择保存位置（比如放到 `C:\Users\你的用户名\`）





### 设为环境变量

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





### 检查

> where pushgogo ---->linux里是
>
> 如果返回路径则表示配置成功





### 总结流程

1. **脚本路径**：`C:\Users\aschenbath\autopush.sh`
2. **bat 文件**：`C:\Users\aschenbath\pushgogo.bat`
3. **环境变量里加入了**：`C:\Users\aschenbath`
4. **然后你就能在任意 CMD 输入**：

```bash
pushgogo
```

xixixixi66666

