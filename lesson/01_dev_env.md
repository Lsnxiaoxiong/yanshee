
# Yanshee机器人介绍
[官网](https://yandev.ubtrobot.com/#/zh)

## 硬件信息
详见[Yanshee教育标准版](../res/Yanshee教育标准版.pdf)
与[Yanshee机器人开发指南](../res/Yanshee传感器模组.pdf)以及官网[指南](https://yandev.ubtrobot.com/#/zh/guide)。

## 软件下载
在官网[下载页面](https://yandev.ubtrobot.com/#/zh/download)可下载机器人固件以及app。

![image-20250821154919934](./01_dev_env_assets/image-20250821154919934.png)



## 使用app连接机器人

长按机器人胸前按钮，等待蓝光亮起，启动机器人。打开下载安装完成的app，手机连接到wifi，注意wifi频率是2.4G。

![image-20250821160604635](01_dev_env_assets/image-20250821160604635.png)

点击app右上角按钮，进入设备搜索页面，选择对应的机器人连接即可。

![image-20250821160715360](01_dev_env_assets/image-20250821160715360.png)





#  开发环境

## python安装



### python下载

进入[python官网](https://www.python.org/)

![image-20250822101938032](01_dev_env_assets/image-20250822101938032.png)



选择合适的系统版本，这里以windows系统为例。

![image-20250822102053525](01_dev_env_assets/image-20250822102053525.png)



选择python版本，3.9<=版本<最新版。

![image-20250822102340317](01_dev_env_assets/image-20250822102340317.png) 



### python安装

下载installer之后，点击安装。

![image-20250822102519729](01_dev_env_assets/image-20250822102519729.png)

**如果没装过python**，可以点击勾选下方的Add python.exe tp PATH。

![image-20250822102654356](01_dev_env_assets/image-20250822102654356.png)

然后点击自定义安装。

![image-20250822102732819](01_dev_env_assets/image-20250822102732819.png)

点击Next。

![image-20250822102809841](01_dev_env_assets/image-20250822102809841.png)



这里选项保持默认即可，可更换下方python的安装位置。点击Install安装。

![image-20250822103018766](01_dev_env_assets/image-20250822103018766.png)



安装完成之后，关闭窗口。

![image-20250822103126746](01_dev_env_assets/image-20250822103126746.png)



### python验证

安装完成之后，打开命令行终端（以window为例），按下键盘WIN+R，屏幕左下方会显示一个输入框，输入cmd确定后，会打开命令行终端。

![image-20250822103354944](01_dev_env_assets/image-20250822103354944.png)

![image-20250822103436623](01_dev_env_assets/image-20250822103436623.png)

或者在搜索中输入cmd打开。

![image-20250822103533404](01_dev_env_assets/image-20250822103533404.png)



在终端输入python，回车，终端会显示当前使用的python版本。

![image-20250822103702323](01_dev_env_assets/image-20250822103702323.png)



### 配置环境变量

若在终端输入python之后提示“不是内部或外部命令，也不是可运行的程序”，需要将python.exe配置到PATH环境变量中。



搜索“环境变量”，点击打开“**编辑系统环境变量**”

![image-20250822103920767](01_dev_env_assets/image-20250822103920767.png)



点击“环境变量”

![image-20250822104039075](01_dev_env_assets/image-20250822104039075.png)



在“系统变量”中找到“Path”一行，点击编辑。

![image-20250822104119967](01_dev_env_assets/image-20250822104119967.png)



点击“新建”，找到python的安装路径，以及该路径下的Scripts文件夹，把这两个文件夹的完整路径分别填到新建的变量中。

可添加多个python，点击右侧的“上移”“下移”移动变量的位置，优先使用在上面的变量。

![image-20250822104205404](01_dev_env_assets/image-20250822104205404.png)

![image-20250822104628010](01_dev_env_assets/image-20250822104628010.png)

![image-20250822104823462](01_dev_env_assets/image-20250822104823462.png)





点击确定。打开终端再次输入python，即可显示版本信息。

![image-20250822105150436](01_dev_env_assets/image-20250822105150436.png)



## Nodejs安装

nodejs是javaScript的运行环境，后续课程使用的mcp需要nodejs环境。



### 下载

进入[nodejs官网](https://nodejs.org)，点击download。

![image-20250822151136899](01_dev_env_assets/image-20250822151136899.png)



选择合适的系统以及长期支持的版本（LTS），点击下载Window Installer。

![image-20250822151327875](01_dev_env_assets/image-20250822151327875.png)



### 安装

点击下载完成的安装包，保持默认选项，点击下一步，选择安装位置完成安装。

![image-20250822151554406](01_dev_env_assets/image-20250822151554406.png)

### 验证

安装完成后打开终端输入node，显示版本信息即安装成功。

![image-20250822151741245](01_dev_env_assets/image-20250822151741245.png)



### 配置运行权限

 **PowerShell 的执行策略 (Execution Policy)** 限制了脚本运行。默认情况下，Windows 可能会禁止运行 `.ps1` 脚本。

在powershell输入

```powershell
Get-ExecutionPolicy
```

默认情况下的输出为：**Restricted**

![image-20250822160720325](01_dev_env_assets/image-20250822160720325.png)



**修改运行策略**

在powershell输入：

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
Get-ExecutionPolicy
```

显示RemoteSigned代表修改成功。

![image-20250822160946406](01_dev_env_assets/image-20250822160946406.png)



## GIT安装

git是一个代码管理工具。[官网](https://git-scm.com/downloads)

![image-20250822110601008](01_dev_env_assets/image-20250822110601008.png)



### 下载

选择合适的版本。

![image-20250822110826556](01_dev_env_assets/image-20250822110826556.png)

![image-20250822110858749](01_dev_env_assets/image-20250822110858749.png)



### 安装

下载完成后，点击安装包开始安装。

![image-20250822111702271](01_dev_env_assets/image-20250822111702271.png)

选择安装位置，点击下一步。

![image-20250822111745415](01_dev_env_assets/image-20250822111745415.png)

保持默认选项，点击下一步。

![image-20250822111829419](01_dev_env_assets/image-20250822111829419.png)

![image-20250822111858003](01_dev_env_assets/image-20250822111858003.png)

![image-20250822111917038](01_dev_env_assets/image-20250822111917038.png)

![image-20250822111931940](01_dev_env_assets/image-20250822111931940.png)

![image-20250822111949783](01_dev_env_assets/image-20250822111949783.png)

![image-20250822112006586](01_dev_env_assets/image-20250822112006586.png)

![image-20250822112021951](01_dev_env_assets/image-20250822112021951.png)

![image-20250822112040628](01_dev_env_assets/image-20250822112040628.png)

![image-20250822112053275](01_dev_env_assets/image-20250822112053275.png)

![image-20250822112105209](01_dev_env_assets/image-20250822112105209.png)

![image-20250822112115571](01_dev_env_assets/image-20250822112115571.png)

![image-20250822112131835](01_dev_env_assets/image-20250822112131835.png)

安装完成后关闭窗口即可。

![image-20250822112300353](01_dev_env_assets/image-20250822112300353.png)



### 验证

打开终端，输入git，会显示一下内容，说明安装成功。

![image-20250822112429505](01_dev_env_assets/image-20250822112429505.png)







## VSCode安装

Visual Studio code 是微软开发的一款IDE集成开发环境软件，后续课程的代码演示使用该软件。也可以使用其它软件如pycharm、cursor、trae等。



### 下载

进入[vscode官网](https://code.visualstudio.com/)，直接点击下载即可，其它系统点击右上方的下载，选择合适的版本。

![image-20250822113059091](01_dev_env_assets/image-20250822113059091.png)

![image-20250822113132724](01_dev_env_assets/image-20250822113132724.png)



### 安装

下载完成之后，点击安装。点击同意，下一步。

![image-20250822113253883](01_dev_env_assets/image-20250822113253883.png)



选择安装位置，点击下一步。后续选项保持默认即可，点击下一步。

![image-20250822113319904](01_dev_env_assets/image-20250822113319904.png)



点击安装。

![image-20250822113425937](01_dev_env_assets/image-20250822113425937.png)



点击完成。

![image-20250822113509685](01_dev_env_assets/image-20250822113509685.png)

![image-20250822113549703](01_dev_env_assets/image-20250822113549703.png)





### 语言设置

打开vscode，点击左侧的插件按钮，输入chinese，可安装汉化插件，安装完成后重启即可。

![image-20250822113846408](01_dev_env_assets/image-20250822113846408.png)



### 创建文件夹

在电脑上创建一个文件夹，打开vscode，点击左上方的文件按钮，点击打开文件夹，选择刚才创建的文件夹打开。

![image-20250822114747972](01_dev_env_assets/image-20250822114747972.png)

![image-20250822114808771](01_dev_env_assets/image-20250822114808771.png)

![image-20250822114838632](01_dev_env_assets/image-20250822114838632.png)



点击信任作者。

![image-20250822114913611](01_dev_env_assets/image-20250822114913611.png)



打开文件夹后，左上方会显示文件夹名称。

![image-20250822114948709](01_dev_env_assets/image-20250822114948709.png)

点击文件夹名称，右侧会显示操作图标，可以创建文件、文件夹等。

![image-20250822115117635](01_dev_env_assets/image-20250822115117635.png)

### 安装python插件

创建一个hello.py文件，打开，右下角会出现下载python插件的提示，直接安装即可。

![image-20250822115157862](01_dev_env_assets/image-20250822115157862.png)

![image-20250822115425910](01_dev_env_assets/image-20250822115425910.png)

![image-20250822115450599](01_dev_env_assets/image-20250822115450599.png)



如果没有出现提示，直接在插件中搜索python，手动安装 Python Debugger、Python Environments、Python即可。

![image-20250822115603786](01_dev_env_assets/image-20250822115603786.png)



点击允许访问。

![image-20250822115707602](01_dev_env_assets/image-20250822115707602.png)



安装完成后，打开hello.py文件，右上角会显示一个三角形。

![image-20250822115916915](01_dev_env_assets/image-20250822115916915.png)



### 运行python程序

在hello.py文件中编写示例代码。

```python
if __name__ == "__main__":
    print("hello vscode")
```

点击右上角面板显示按钮，可以显示/隐藏终端。

![image-20250822122313332](01_dev_env_assets/image-20250822122313332.png)



点击右上角允许该程序，下方的终端会输出"hello vscode"。

![image-20250822120206453](01_dev_env_assets/image-20250822120206453.png)



观察终端输出的上一行：

```shell
 C:/Users/lsn/AppData/Programs/Python/Python312/python.exe c:/Users/lsn/Desktop/teste1/hello.py
```

+ ...python.exe ：这个就是之前安装的python
+ ...hello.py ：这个是我们编写的程序

这个命令就是终端执行python程序的命令

```shell
python xxx.py
```

因为我们添加了python的环境变量，所以可以不输入完整的python路径。

在终端输入：

```shell
python hello.py
```

![image-20250822120850834](01_dev_env_assets/image-20250822120850834.png)

可以看到程序正常运行了。不过python后面的hello.py文件也不是完整路径，因为当前终端所在的路径是...\test01，也就是hello.py文件所在的路径，那么执行命令的时候，python会在当前文件寻找hello.py文件进行执行，所以不需要完整路径。

我们在终端输入：

```shell
cd ..
```

![image-20250822121332309](01_dev_env_assets/image-20250822121332309.png)

可以看到当前路径变成了test01的上一级目录。

我们再次执行hello.py文件。

![image-20250822121446286](01_dev_env_assets/image-20250822121446286.png)

可以看到执行出现错误：没有这个文件或者目录。

我们在终端输入ls来查看当前目录下的文件和文件夹：

```shell
ls
```

![image-20250822121702454](01_dev_env_assets/image-20250822121702454.png)

可以看到，当前目录下确实没有hello.py这个文件，所以执行错误。

那么，我们在终端输入：

```python
python ./test01/hello.py
```

![image-20250822121928881](01_dev_env_assets/image-20250822121928881.png)

可以看到程序再次成功运行。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                

综上，在终端运行python程序时，你可以cd到程序所在的目录下后，执行程序；或者输入完整/相对路径来执行。



### Copilot

copilot是vscode自带的一个AI插件，打开vscode点击右上方的机器人图标，即可打开对话框。

![image-20250822114436532](01_dev_env_assets/image-20250822114436532.png)



使用github登录copilot。

![image-20250822141144098](01_dev_env_assets/image-20250822141144098.png)



登录后可在输入框输入文本进行对话，对话框下方可以选择模型。

![image-20250822143404039](01_dev_env_assets/image-20250822143404039.png)



输入#hello，copilot会匹配对应的文件，选择需要的文件可以将其添加为上下文。

![image-20250822143615298](01_dev_env_assets/image-20250822143615298.png)

![image-20250822143637662](01_dev_env_assets/image-20250822143637662.png)



输入文本让它添加功能。

![image-20250822143738029](01_dev_env_assets/image-20250822143738029.png)

![image-20250822143756710](01_dev_env_assets/image-20250822143756710.png)

模型输出了结果，但是没有添加到文件中，因为当前的模式是“Ask”（对话框左下角），将模式改为Edit/Agent后，让它把新内容添加到文件中。

![image-20250822143925247](01_dev_env_assets/image-20250822143925247.png)

模型执行完成后，hello.py文件中出现了新的内容。可以检测内容是否是需要的，然后选择Keep/Undo。

![image-20250822144215992](01_dev_env_assets/image-20250822144215992.png)



每段对话上方都有一个checkpoint，点击后可以将操作撤销，回到执行这个操作之前。

![image-20250822144935083](01_dev_env_assets/image-20250822144935083.png)

![image-20250822145054911](01_dev_env_assets/image-20250822145054911.png)



### Lingma

通义灵码是阿里开发的一个AI插件。在插件中搜索lingma安装。

![image-20250822145506794](01_dev_env_assets/image-20250822145506794.png)



注册登录阿里云账号后使用。

![image-20250822145716218](01_dev_env_assets/image-20250822145716218.png)



与copilot类似，可在对话框左下角调整模式、模型

![image-20250822145952861](01_dev_env_assets/image-20250822145952861.png)

![image-20250822150213700](01_dev_env_assets/image-20250822150213700.png)



#### 语言设置

点击右上角的设置按钮，将settings中最底下的三个语言设置为中文即可。

![image-20250822150422204](01_dev_env_assets/image-20250822150422204.png)



## CUDA+cuDNN安装

> 这部分的进行，需要电脑安装了英伟达Nvidia的显卡

### Nvidia显卡驱动安装

查看任务栏中是否有英伟达显卡驱动的图标，如果有说明已经安装了驱动，跳过显卡驱动安装这一步。

![image-20250822165226039](01_dev_env_assets/image-20250822165226039.png)

进入[Nvidia官网](https://www.nvidia.cn/geforce/campaigns/back-to-school/?ncid=pa-srch-baid-450176)，点击驱动程序。

![image-20250822165400645](01_dev_env_assets/image-20250822165400645.png)



#### 确认显卡型号

按下Ctrl+Alt+Delete，或者右键点击任务栏，打开任务管理器。

![image-20250822165527822](01_dev_env_assets/image-20250822165527822.png)

在“性能”栏下找到对应的显卡，查看显卡型号。

![image-20250822165603521](01_dev_env_assets/image-20250822165603521.png)



或者在搜索中搜索“设备管理器”，打开

![image-20250822165745215](01_dev_env_assets/image-20250822165745215.png)



在“显示适配器”下找到显卡，确认型号。

![image-20250822165815625](01_dev_env_assets/image-20250822165815625.png)



#### 下载显卡驱动

填入相关信息，搜索驱动程序。

![image-20250822170026457](01_dev_env_assets/image-20250822170026457.png)



选择最新版本的驱动下载，GeForce Game Ready和NVIDIA Studio都可以。

![image-20250822170345928](01_dev_env_assets/image-20250822170345928.png)



点击立即下载，下载完成后点击安装，选择默认选项，点击下一步完成安装即可。

![image-20250822170503761](01_dev_env_assets/image-20250822170503761.png)

![image-20250822170546349](01_dev_env_assets/image-20250822170546349.png)



#### 验证

安装完成后，在终端输入：

```shell
nvidia-smi
```

控制台会输出显卡信息：CUDA Version：12.9 --》就是当前最高支持的CUDA版本。

![image-20250822170807436](01_dev_env_assets/image-20250822170807436.png)



### CUD安装

进入[Nvidia开发者平台](https://developer.nvidia.com/)





## Pytorch安装

pytorch是一个深度学习框架，在后续的yolo模型训练推理中会使用到。



### 下载

进入[pytorch官网](https://pytorch.org/)，点击get started

![image-20250822164545249](01_dev_env_assets/image-20250822164545249.png)
