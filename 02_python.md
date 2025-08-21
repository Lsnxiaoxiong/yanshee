# 第二单元：Python 编程基础（2 课时 / 90 分钟）

本讲义面向零基础到初学者，目标是在 90 分钟内让学员掌握 Python 基本语法、流程控制、函数与模块、简单的类与面向对象，并能写出能控制机器人或处理传感器数据的基础脚本。

时间分配（建议）
- 课程语境与环境检查：5 分钟
- Python 基础语法（0.5 课时 ≈ 22 分钟）
- 流程控制（0.5 课时 ≈ 22 分钟）
- 函数与模块（0.5 课时 ≈ 22 分钟）
- 类与面向对象（0.5 课时 ≈ 19 分钟）
- 练习与答疑：约 10 分钟（穿插进行）

先决条件
- 已安装 Python 3.8+（推荐 3.9+）
- 能打开终端（Windows: PowerShell）并运行 python / pip
- 推荐在 VSCode 中打开本项目并安装 Python 扩展

如何运行示例
- 在 VSCode 中新建文件，例如 `example.py`，粘贴示例并运行（F5 或右上角运行）
- 在 PowerShell 中运行：

```powershell
python example.py
```

------

## 1. Python 基础语法（0.5 课时）
目标：掌握 Python 基本语法，能编写简单脚本打印与处理变量。

要点
- 注释：单行 `#`，多行可用三引号（主要用于 docstring）
- 基本类型：int, float, bool, str
- 容器类型：list, dict, tuple
- 变量命名与赋值
- 字符串格式化（f-string）

示例 1 — Hello 与变量：

```python
# example_hello.py
name = "Yanshee学生"
age = 20
pi = 3.14159
is_robot = True
print(f"你好，{name}，年龄：{age}，PI≈{pi}")
```

预期输出：

你好，Yanshee学生，年龄：20，PI≈3.14159

示例 2 — 容器与遍历：

```python
# example_containers.py
nums = [1, 2, 3, 5]
info = {"name": "Yanshee", "id": 1001}
coords = (10.0, 20.0)

print(nums[0])      # 访问列表
print(info["name"]) # 访问字典
print(coords)       # 元组
```

练习 1（2-3 分钟）
- 写一个脚本：定义列表 [10, 20, 30]，把每个元素乘以 2 并打印结果。

参考答案：

```python
lst = [10, 20, 30]
for x in lst:
    print(x * 2)
```

小贴士
- Python 是动态类型，赋值时不需要声明类型
- 推荐使用有意义的变量名，遵循 snake_case 风格

------

## 2. 流程控制（0.5 课时）
目标：能用条件与循环解决基本逻辑问题（计数、筛选、循环任务）。

要点
- if / elif / else
- for 循环（可遍历列表、字典、range）
- while 循环
- break / continue

示例 1 — 条件判断：

```python
# example_if.py
x = 15
if x < 10:
    print("小于 10")
elif x < 20:
    print("10-19")
else:
    print(">=20")
```

示例 2 — 循环与过滤：

```python
# example_loop.py
nums = [1, 2, 3, 4, 5, 6]
# 打印偶数
for n in nums:
    if n % 2 != 0:
        continue
    print(n)

# range 用法
for i in range(0, 5):
    print(i)
```

练习 2（3-4 分钟）
- 给定列表 [3, 7, 2, 9, 4]，打印所有大于 4 的元素并统计个数。

参考答案：

```python
lst = [3, 7, 2, 9, 4]
count = 0
for v in lst:
    if v > 4:
        print(v)
        count += 1
print("总数：", count)
```

课堂应用示例（机器人场景）
- 根据传感器读数（如距离），实现简单阈值决策：若距离 < 0.3m 则停止并后退。

```python
# pseudo sensor handling
distance = 0.25  # 单位：米
if distance < 0.3:
    robot.stop()
    robot.move_backward(0.2)
```

------

## 3. 函数与模块（0.5 课时）
目标：编写可重用函数并能使用 pip 安装第三方包。

要点
- def 定义函数，参数与返回值
- 默认参数、可变参数（*args, **kwargs）
- 模块与包的导入（import / from ... import）
- 使用 pip 安装第三方库并在脚本中引用

示例 1 — 简单函数：

```python
# example_func.py
def add(a, b):
    """返回 a + b"""
    return a + b

print(add(2, 3))  # 输出 5
```

示例 2 — 模块拆分（project structure）
- 文件结构：
  - robot_project/
    - main.py
    - utils.py

utils.py:
```python
# utils.py
def clamp(x, lo, hi):
    return max(lo, min(hi, x))
```

main.py:
```python
# main.py
from utils import clamp
v = clamp(10, 0, 5)
print(v)  # 输出 5
```

如何用 pip 安装库（在 PowerShell）

```powershell
python -m pip install opencv-python
```

练习 3（5 分钟）
- 写一个函数 safe_div(a, b) 返回 a / b；当 b 为 0 时返回 None 而不是抛错。

参考答案：

```python
def safe_div(a, b):
    try:
        return a / b
    except ZeroDivisionError:
        return None
```

课堂应用示例（机器人场景）
- 将相机读取封装成函数：get_frame(camera_id=0) 返回图像数组

------

## 4. 类与面向对象基础（0.5 课时）
目标：用类封装简单对象（如机器人关节或传感器接口）。

要点
- class 定义，__init__ 构造方法
- 属性与方法，实例化对象
- 简单继承与方法重写（可选）

示例 1 — 关节封装：

```python
# example_class.py
class Joint:
    def __init__(self, name, angle=0.0):
        self.name = name
        self.angle = angle

    def set_angle(self, a):
        self.angle = a
        print(f"{self.name} 角度设置为 {self.angle}")

# 使用
j = Joint('shoulder', 0.0)
j.set_angle(30)
```

示例 2 — 继承（传感器示例）：

```python
class Sensor:
    def read(self):
        raise NotImplementedError()

class UltrasonicSensor(Sensor):
    def read(self):
        # 伪实现
        return 0.35

s = UltrasonicSensor()
print(s.read())
```

练习 4（5 分钟）
- 实现一个 RobotController 类，包含方法 move_forward(distance) 与 stop()，并在 move_forward 中打印移动距离。

参考答案：

```python
class RobotController:
    def move_forward(self, distance):
        print(f"向前移动 {distance} 米")

    def stop(self):
        print("停止")

rc = RobotController()
rc.move_forward(0.5)
rc.stop()
```

------

## 课堂小结与延伸任务

本节重点回顾：变量/容器、条件与循环、函数/模块、类的基本用法。掌握这些内容后，学员应能编写小脚本来读取传感器、对数据做简单处理并控制机器人动作。

课后作业（建议）
1. 使用 OpenCV 读取摄像头（或视频文件）并显示窗口（提示：cv2.VideoCapture）。
2. 编写一个监测距离并在低于阈值时触发报警的脚本（伪传感器数据也可）。
3. 在 GitHub 上创建仓库并提交本次课的所有示例代码与 README（说明如何运行）。

参考资料
- 官方文档：https://docs.python.org/3/
- 在线教程（中文）：廖雪峰 Python 教程
- OpenCV Python：https://opencv.org/

---

文件准备者：课程模板自动生成器（可根据需要调整示例或加入更多课堂练习）
