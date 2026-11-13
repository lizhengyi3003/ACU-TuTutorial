<span style="color: orange; font-weight: bold;">⚠️ 这份教程是我自己踩过坑之后整理的, 不敢说讲得多好, 只能保证是我验证过能跑通的流程. 配置过程中如果遇到我没写到的问题,或者你看不懂的地方——别慌, 这很正常. 善用AI提问、去B站搜相关视频、翻官方文档, 这些才是解决问题的核心能力. 教程只是起点,学会自己找答案才是目的.</span>

## 一. 部署AI Agent[^1]

### 1. 前述:

不少同学或许使用过像是 ChatGPT、DeepSeek 或是豆包这样的**LLM**[^2]聊天机器人来完成编程工作. 大家只需要在网页或客户端的聊天框中输入文字或上传图片来描述自己的需求, 把这些内容作为**提示词**[^3]发送给机器人, 稍等片刻就能看到AI给我们生成的代码.

虽然通常这已经比大家手写快得多了, 不过似乎还是存在一些问题: 
1. 需要手动从聊天窗口里把代码复制粘贴到自己的**IDE**[^4]中, 这有点麻烦. 对于更大的包含多个文件和复杂结构的项目, 这样手动复制几乎不太可能. 
2. 这些AI只会指导你怎么去做, 只会给你提建议, 而不是它帮你去执行某一个特定的任务

### 2. 下载和配置Harness[^5]

国内的主流Harness有深度求索的**DeepSeek Harness**[^6], 阿里的**Qoder**, 腾讯的**WorkBuddy**等

国外的Harness有OenAI的**Codex**, Anthropic的**Claude Code**,  **Hermes**, **Pi**等

#### (1) 下载和配置GUI[^9] Agent: 

图形化Agent的特点是互动性对新手用户友好, 界面可视化

这里教大家如何下载和配置国内的dsh:

下载链接: [DeepSeek Harness｜共探智能上限](https://www.deepseek.com/harness/)
![1-1.png](images_class1/1-1.png)
根据自己电脑系统下载即可, 安装位置可以保持默认

第一次进去的时候是用不了的 (因为还没有接入特定模型), 需要在DeepSeek API开放平台[DeepSeek 开放平台](https://platform.deepseek.com/usage)申请个**API key**[^7]

流程: 
1. 先往账户里充值特定金额 (充1元即可试试水)![1-2.png](images_class1/1-2.png)
2. 申请API key, 名称按你的需求取一个 (你用这个API key是拿来干嘛的)![1-3.png](images_class1/1-3.png)![1-4.png](images_class1/1-4.png)

3. <font color = 'red'>注意:</font>
	1. 创建API key好后到这个页面, 需要把这串key复制好后再关掉页面!!!否则后续将无法再保存这个key了
	2. 复制好的key不要给其他人使用, 否则别人使用你的key将从你的账号中扣除金钱 ![1-5.png](images_class1/1-5.png)

接下来就点进dsh里, 点击添加API key, 把你的key复制进去![1-6.png](images_class1/1-6.png)

DeepSeek官方目前内置两个模型: flash和pro, 提示词相同的情况下, 选择不同的模型和不同的推理等级, 消耗的**token**[^8]会有所不同 (如下的选择的模型为flash, 推理等级为high)
![1-7.png](images_class1/1-7.png)

你可以修改下面的权限来控制agent的操作范围, 一般选择在工作区内修改, 如果你想让AI操控你的电脑帮你完成某个配置任务什么的可以选择完全权限, 但是风险很高, 一不小心agent可能会使删除重要文件什么的, 所以需要谨慎使用!![1-8.png](images_class1/1-8.png)

示范: 叫它在某一个目录下生成网页
![1-9.png](images_class1/1-9.png)

生成的网页预览: 
![1-10.png](images_class1/1-10.png)其它更高级的功能自己慢慢去探索吧\~~
(<font color = 'red'>实际上, dsh可以帮你完成75%以上的活, 比如说帮你完成许多环境的配置, 把权限都给它, 下面的教程都可以由它接活, 有什么不懂的可以试着跟它诉说一下</font>)



#### (2) 下载和配置CLI[^10] Agent: 

如果你更倾向于使用终端CLI来完成某一特定的任务, 这里教大家怎么下载和配置在CLI运行的Agent

以国外的Claude code为例 (如果你配置好dsh的话你可以把权限都打开, 直接叫它帮你配置)

1. 配置Claude Code运行环境: 下载**node.js**, 下载链接: https://nodejs.org/zh-cn 
![1-11.png](images_class1/1-11.png)

![1-12.png](images_class1/1-12.png)
下载完后一路点击下一步即可

2. 安装**git**: 链接(以WIndows系统x64为例) https://mirrors.tuna.tsinghua.edu.cn/github-release/git-for-windows/git/
![1-13.png](images_class1/1-13.png)

![1-14.png](images_class1/1-14.png)
下载完后一路点击下一步即可

3. 以管理员身份打开cmd (ctrl shift enter进入管理员模式), 输入下面这三条命令, 如果显示对应版本则说明安装成功![1-15.png](images_class1/1-15.png)


4. 安装Claude Code: 继续在管理员模式下的cmd执行这条命令下载国内镜像源, 方便Claude Code安装
	```cmd
	npm config set registry https://registry.npmmirror.com/
	```
	接着执行这条命令下载Claude Code
	```cmd
	npm install -g @anthropic-ai/claude-code
	```
	当出现下面红色框框内容时即表示安装完成, 输入claude -v来查看版本号![1-16.png](images_class1/1-16.png)


5. 接入DeepSeek模型(下面介绍三种接入方式, <font color = 'cyan'>后面两种可能存在网络问题</font>)
	1. **第一种方式----使用终端**: cmd输入以下命令创建目录
		```cmd
		mkdir "%USERPROFILE%\.claude" 2>nul
		```
		再输入以下命令打开配置文件
		```cmd
		notepad "%USERPROFILE%\.claude\settings.json"
		```
		这会打开记事本, 选择新建新文件夹, 在文件夹复制以下内容后保存(记得把 "*你的key*" 换成你申请的key): 
		```json
		{
		  "env": {
		    "ANTHROPIC_BASE_URL": "https://api.deepseek.com/anthropic",
		    "ANTHROPIC_AUTH_TOKEN": "你的key",
		    "ANTHROPIC_MODEL": "deepseek-flash[1m]",
		    "ANTHROPIC_DEFAULT_OPUS_MODEL": "deepseek-flash[1m]",
		    "ANTHROPIC_DEFAULT_SONNET_MODEL": "deepseek-flash[1m]",
		    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "deepseek-flash",
		    "CLAUDE_CODE_SUBAGENT_MODEL": "deepseek-flash",
		    "CLAUDE_CODE_EFFORT_LEVEL": "max",
		    "CLAUDE_CODE_AUTO_COMPACT_WINDOW": "786432"
		  }
		}
		```
	2. **第二种方式----使用CC Switch**: 去GitHub上面下载CC Switch : [farion1231/cc-switch: A cross-platform desktop All-in-One assistant for Claude Code, Codex, OpenCode,DeepSeek Harness and more. Only official website: ccswitch.io](https://github.com/farion1231/cc-switch)![1-17.png](images_class1/1-17.png)根据自己电脑的系统下载, 下载完后双击即可打开![1-18.png](images_class1/1-18.png)安装成功后点击右上角的 "添加供应商"![1-19.png](images_class1/1-19.png)点击DeepSeek![1-20.png](images_class1/1-20.png)把你的API Key粘贴进去![1-21.png](images_class1/1-21.png)点击获取模型, 然后在下来菜单中改成以下模型即可, 点击右下角的添加![1-22.png](images_class1/1-22.png)
	3. **第三种方式----使用magpie**: 去GitHub上面下载magpie : [yetone/magpie: Every agent's model. One place. Codex on DeepSeek, Claude Code on Kimi, from the menu bar.](https://github.com/yetone/magpie)![1-23.png](images_class1/1-23.png)根据自己电脑的系统下载![1-24.png](images_class1/1-24.png)后面的配置步骤和CC Switch的差不多, 有什么不懂的多借助AI

6. 使用Claude Code: 打开cmd(不一定要用管理员身份), 输入`claude`, 回车, 开始界面应该是叫你选一个主题(忘记了)![1-25.png](images_class1/1-25.png)然后它叫你是否信任该目录(选择信任即可)![1-26.png](images_class1/1-26.png)然后就可以跟它对话了, 它和dsh一样会帮你执行特定的任务(其它更高级的功能自己去问AI探索吧\~~)![1-27.png](images_class1/1-27.png)



## 二. Python环境配置

下载Python的解释器[^11]: [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)![1-28.png](images_class1/1-28.png)

安装步骤:
下面两个选项务必勾上, 然后点击 Install Now![1-29.png](images_class1/1-29.png)

检测安装是否成功: 打开cmd输入:
```cmd
python --version
```
如果显示版本号就说明安装成功了, 如果提示找不到命令, 可能是安装时没勾选 "Add Python to PATH", 重新运行安装程序勾选即可, 或手动配置环境变量
![1-30.png](images_class1/1-30.png)



## 三. Java环境配置

下载Java的编译器[^12](用镜像源下载多快一些): 
https://mirrors.tuna.tsinghua.edu.cn/Adoptium/

强烈建议下载21版本的: ![1-31.png](images_class1/1-31.png)

点击jdk(注意不是jre)
![1-32.png](images_class1/1-32.png)

往后的就点击x64, 选择Windows系统, 选msi后缀的那个安装包即可开始下载

双击msi, 除了一下页面需要更改外, 其他一路点击下一步![1-33.png](images_class1/1-33.png)
![1-34.png](images_class1/1-34.png)

安装完成后, 请务必打开新的cmd, 分别输入以下指令后回车
```cmd
java -version
```

```cmd
javac -version
```

显示版本号则说明安装成功![1-35.png](images_class1/1-35.png)



## 四. 数据库环境配置

这里以**mySQL**为例(当然数据库还有PostgreSQL, SQLite等), 并且学校就是教MySQL的

下载mySQL是网址: https://dev.mysql.com/downloads/installer/
![1-36.png](images_class1/1-36.png)![1-37.png](images_class1/1-37.png)

下面是安装向导的流程:

**除了以下页面**需要注意外, 其他步骤一路next (或Execute)

这里是建立你的mysql数据库的密码, <font color = 'red'>密码千万不能忘记!!!</font>
![1-38.png](images_class1/1-38.png)

最后点finish完成即可

接下来是验证有没有安装成功, 但是此时你的电脑还不知道`mysql`这个指令是什么意思

所以我们首先要配置**Path环境变量**[^13], 让终端熟悉`mysql`这个指令
打开cmd, 输入下列一串指令: 
```cmd
setx Path "%Path%;C:\Program Files\MySQL\MySQL Server 8.0\bin"
```
![1-39.png](images_class1/1-39.png)

这样环境变量就配置好了

**重新打开终端**, 接着输入这串指令看看是否安装成功:
```cmd
mysql -u root -p
```
![1-40.png](images_class1/1-40.png)
显示 Enter password(输入密码) 时就说明安装成功了, 输入你刚才设置的密码后就会显示这个页面![1-41.png](images_class1/1-41.png)

这时候就可以用sql语句写代码了, 但是在终端写代码并不直观, 后续会讲一款可以写mysql的编辑器



## 五. 基本IDE的下载和配置

### 1. VS Code

写前端代码推荐使用的IDE是VS Code, 下载链接: [https://code.visualstudio.com/](https://code.visualstudio.com/)
![1-42.png](images_class1/1-42.png)

在安装界面中, 下面这个界面全部勾选, 其余的一路点击下一步即可![1-43.png](images_class1/1-43.png)

进入VS Code后, 界面是英文状态的, 按照下面流程可以下载中文插件![1-44.png](images_class1/1-44.png)

下载插件完后右下角会有弹窗, 点击按钮它就会重启软件, 之后页面就是中文状态了![1-45.png](images_class1/1-45.png)

接下来是VS Code一些必要以及推荐的插件 (各插件具体的用法这里不在赘述, 可以问问AI):

#### (1) 前端相关

1. open in browser![1-46.png](images_class1/1-46.png)此插件是写前端必备的插件, 它能让你写的代码在浏览器解析渲染出来并展示

2. Live Server![1-47.png](images_class1/1-47.png)此插件主要功能是浏览器解析渲染与代码变化实时监控, 当你改动某一行代码后, 浏览器无需手动刷新就会同步你写的代码

3. px to rem & rpx & vw (cssrem)![1-48.png](images_class1/1-48.png)此插件适配了可以让单位px和rem或vw之间相互转换的快捷键, 响应式布局可以考虑使用

4. Auto Rename Tag![1-49.png](images_class1/1-49.png)此插件的功能是: 当你修改双标签某一端时, 另一端标签也会进行相应地修改

5. CSS Peek![1-50.png](images_class1/1-50.png)Ctrl+点击class 名直接跳到 CSS 定义, 写前端实验时减少来回切换文件

6. Path Autocomplete![1-51.png](images_class1/1-51.png)写import, src, href路径时自动补全文件名和目录, 在HTML, JS中引用本地文件时很省事


#### (2) 效率相关

1. Prettier-Code formatter![1-52.png](images_class1/1-52.png)此插件适配非常多种不同的编程语言进行格式化, 使代码排版更加美观

2. ESLint![1-53.png](images_class1/1-53.png)此插件负责检查代码是否规范, 还有一个相似的插件是Error Lens![1-54.png](images_class1/1-54.png)此插件负责把代码检查工具发现的问题直接显示在代码旁边

3. indent-rainbow![1-55.png](images_class1/1-55.png)不同层级代码缩进用颜色标出, 更具有可视化

4. Code Runner![1-56.png](images_class1/1-56.png)点右上角三角可以直接运行当前文件, 使运行更加方便些

5. Bracket Pair Color DLW![1-57.png](images_class1/1-57.png)让多层级括号用不同颜色进行匹对, 使读代码更加直观

6. Punctuation Auto Switch![1-58.png](images_class1/1-58.png)把中文标点 ，。； 自动转成英文 ,.;, 防止写代码时误输入中文标点, 国内写的典型问题, 很实用

7. Better Comments![1-59.png](images_class1/1-59.png)主要作用是美化并分类代码注释, 让原本单调的注释变得醒目且富有语义, 从而提升代码的可读性

8. Numbered Bookmarks 或 Bookmarks![1-60.png](images_class1/1-60.png)![1-61.png](images_class1/1-61.png)给特定行代码前面标上书签, 可以快速跳转到指定的行

9. Region Highlighter![1-62.png](images_class1/1-62.png)标记代码区块并高亮


#### (3) 个性化相关

1. background-cover![1-63.png](images_class1/1-63.png)此插件可以上传图片或动图自定义你的VS Code背景

2. One Dark Pro![1-64.png](images_class1/1-64.png)此插件可以更改你的代码高亮, 相应的还有Dracula Theme Official等![1-65.png](images_class1/1-65.png)

3. vscode-icons-mac![1-66.png](images_class1/1-66.png)此插件可以更改不同扩展名文件的图标, 让文件类型更加直观, 可视化


#### (4) Python相关

1. Pylance, Python, Python Debugger, Python Environments![1-67.png](images_class1/1-67.png)Python环境必备四件套

写Python代码推荐使用的IDE是Pycharm


#### (5) Java相关

1. 安装java的扩展包(这些插件都封装在一个扩展包里面) :![1-68.png](images_class1/1-68.png)

<font color = 'red'>关于VS Code的Java环境的其他配置可以叫dsh帮你弄好 (底层原理有点复杂), 如果要写Java代码的话我还是推荐使用的IDE是IDEA</font>


#### (6)数据库相关

我的建议是和Java一样用其他编辑器写, 因为VS Code需要安装插件配置数据库环境什么的, 过程比较繁琐hhh(或者叫dsh帮你弄)



### 2. Pycharm

Pycharm是专门用于写py代码的IDE, 下载链接是
https://www.jetbrains.com/pycharm/download/?section=windows
![1-69.png](images_class1/1-69.png)

安装向导中除了以下页面需要勾选, 其他的可以一路点击下一步, 安装完成即可![1-70.png](images_class1/1-70.png)

这里新建项目窗口选好自己已经下载好的解释器![1-71.png](images_class1/1-71.png)

新建项目后等右下角的进度完成即可![1-72.png](images_class1/1-72.png)

Pycharm也可以根据自己的需求安装插件, 但插件市场远没有VS Code的插件生态丰富



### 3. IDEA

IDEA是专门用于写java代码的IDE, 下载链接是
https://www.jetbrains.com/idea/download/?section=windows

因为IDEA和Pycharm都是同一家公司出品, 下载和安装流程可以触类旁通Pycharm的流程, 这里不再一一赘述

新建项目中选择自己下载好的编译器即可
![1-73.png](images_class1/1-73.png)



### 4. DataGrip

DataGrip和Pycharm, IDEA一样, 都是同一家公司出品, 可以写许多种数据库代码的编辑器

下载链接: https://www.jetbrains.com/zh-cn/datagrip/

和Pycharm的流程一样
![1-74.png](images_class1/1-74.png)

简单演示一下如何创建你的数据库: 
选择的数据库为MySQL
![1-75.png](images_class1/1-75.png)

弹出一个窗口, 这里输入你的用户名(root)和密码(自己设置的)
![1-76.png](images_class1/1-76.png)

点击左下角测试连接, 显示Succeeded后就说明连接成功了, 点击OK
![1-77.png](images_class1/1-77.png)

后面就可以写mysql指令了



## 六. 部分词语扫盲


[^1]: Agent: 英文翻译为代理和行动者, 在AI领域指能够感知环境并自主采取行动的系统, 说人话就是你的助手, 它会自己去帮你按要求完成某一个任务

[^2]: **L**arge **L**anguage **M**odel: 大语言模型

[^3]: 提示词 (Prompt): 指用户输入给AI模型的指令或问题描述, 就是你对AI发送的对话

[^4]: 集成开发环境 (**I**ntegrated **D**evelopment **E**nvironment): 用于提供程序开发环境的应用程序, 说人话就是你写代码的地方(不可能写在记事本上吧)

[^5]: harness, 英文翻译为马鞍, 意为束缚马的工具从而驾驭它, 不让其变野性乱跑. 在AI领域下harness被赋予上了新的活力: 指围绕模型构建的一整套工程化控制与评测框架, 用来约束、引导和评估模型的行为, 使其输出稳定、可控、可复现, 但是只有harness是不够的, AI圈子有一个非常出名的公式是 **Agent = Model + Harness**, harness接上特定的模型 (model) 才能帮你干活, 就像骑马务必要有马鞍一样, 接入的模型会影响执行效率和输出结果, 就像骑不同品种的马一样, 当然harness也有许多产品 (后面会教如何配置) , 类比马鞍也有不同类型一样

[^6]: DeepSeek Harness我们简称dsh

[^7]: 这里的API key相当于是电话卡, 打电话需要插入电话卡, 申请API key就是一个办卡的过程, 当然,  只有电话卡是不够的, 还需要往里面充钱才能有通话功能, 所以要充钱才能使用API 

[^8]: 中文常译为“词元”. 在LLM中, 指文本被切分后得到的最小处理单元, 可以是一个字、一个词或一个子词片段. 模型按token计数来处理输入和输出, 计费通常也以 token 为单位.

[^9]: GUI: Graphical User Interface, 图形用户界面

[^10]: CLI: Command-Line Interface, 命令行界面

[^11]: 解释器: 能够把高级编程语言逐行翻译成机器语言并立即执行, 而不需要像编译器那样先整体生成可执行文件. 它相当于是翻译官, 把py代码翻译成计算机可以读得懂的二进制代码

[^12]: 编译器: 和解释器的底层原理有所区别, 但同样是"翻译官"

[^13]: Path环境变量: 这么理解: 一个存储路径的变量, 比如这个路径"C:\Program Files\MySQL\bin"长长一段我就可以用一个变量Path来表示

