
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
