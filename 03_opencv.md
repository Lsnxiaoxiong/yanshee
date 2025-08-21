# 第三单元：OpenCV 图像处理（2 课时 / 90 分钟）

本讲义为 `yanshee` 课程中“OpenCV 图像处理”模块的详细示例与练习，面向已完成 Python 基础单元的学员。目标是掌握图像读写/显示、摄像头视频流处理、常用图像处理操作（灰度、模糊、边缘检测）、以及人脸检测的两种实现（Haar 与 DNN）。

时间分配（建议）
- 环境检查与安装：5 分钟
- 图像读写与绘制：20 分钟
- 视频流与帧处理：25 分钟
- 边缘检测与轮廓：20 分钟
- 人脸检测（Haar / DNN）：15 分钟
- 练习与答疑：5 分钟

先决条件
- 已安装 Python 3.9+
- 已安装本单元前的示例文件（`02_python.md` 的练习基础）
- 推荐在 VSCode 中运行示例，Windows 下使用 PowerShell

安装（PowerShell）

```powershell
# 推荐安装 opencv-python（纯 Python 绑定）
python -m pip install --upgrade pip
python -m pip install opencv-python
# 若需额外 contrib 模块（如增强的特征、xfeatures2d 等），安装：
python -m pip install opencv-contrib-python
```

如何运行示例
- 在 VSCode 中另建 `example.py` 并粘贴代码，按 F5 运行；或在 PowerShell 运行：

```powershell
python example.py
```

请确保摄像头可用并未被其他程序占用（如浏览器、Teams）。

------

## 1. 图像读写与显示（示例）
目标：能读取、显示、保存图像，理解 BGR 与 RGB 区别并能做基本像素操作。

示例：读取并保存图像

```python
# img_read_write.py
import cv2

# 读取图像（注意：OpenCV 按 BGR 顺序读取）
img = cv2.imread('input.jpg')  # 相对路径或绝对路径
if img is None:
    raise SystemExit('无法打开 input.jpg，请检查路径')

# 显示图像
cv2.imshow('原图', img)
cv2.waitKey(1000)  # 显示 1000ms（1s）

# 将 BGR 转为灰度并保存
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
cv2.imwrite('output_gray.jpg', gray)

# 关闭窗口
cv2.destroyAllWindows()
```

关键点
- cv2.imread 返回 None 时表明文件未找到或无法解码
- OpenCV 使用 BGR，若要用 matplotlib 显示需转换为 RGB

示例：在图像上绘制形状与文字

```python
# draw_example.py
import cv2

img = cv2.imread('input.jpg')
h, w = img.shape[:2]

# 绘制矩形（左上、右下坐标）
cv2.rectangle(img, (10, 10), (w-10, h-10), (0, 255, 0), 2)
# 绘制圆
cv2.circle(img, (w//2, h//2), 40, (255, 0, 0), 3)
# 绘制文本
cv2.putText(img, 'Yanshee', (30, 30), cv2.FONT_HERSHEY_SIMPLEX, 1.0, (0,0,255), 2)

cv2.imshow('draw', img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

练习 1
- 读取一张图片，按 50% 缩放并保存为 `small.jpg`。

参考答案

```python
import cv2
img = cv2.imread('input.jpg')
h, w = img.shape[:2]
small = cv2.resize(img, (w//2, h//2))
cv2.imwrite('small.jpg', small)
```

------

## 2. 视频流处理（示例）
目标：搭建摄像头读取流水线，处理并保存帧到文件。

示例：打开摄像头并显示（按 q 退出），并把每第 N 帧保存为图片

```python
# webcam_capture.py
import cv2

cap = cv2.VideoCapture(0)  # 0 通常是默认摄像头
if not cap.isOpened():
    raise SystemExit('无法打开摄像头')

frame_id = 0
save_every = 30  # 每 30 帧保存一张
while True:
    ret, frame = cap.read()
    if not ret:
        break
    cv2.imshow('cam', frame)
    if frame_id % save_every == 0:
        cv2.imwrite(f'frame_{frame_id}.jpg', frame)
    frame_id += 1

    key = cv2.waitKey(1) & 0xFF
    if key == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```

示例：读取视频文件并另存为不同编码（将 avi 转为 mp4）

```python
# transcode.py
import cv2
cap = cv2.VideoCapture('input.avi')
fourcc = cv2.VideoWriter_fourcc(*'mp4v')
out = None

while True:
    ret, frame = cap.read()
    if not ret:
        break
    if out is None:
        h, w = frame.shape[:2]
        out = cv2.VideoWriter('out.mp4', fourcc, 25.0, (w, h))
    out.write(frame)

cap.release()
if out is not None:
    out.release()
```

注意：编码器可用性依赖系统及 OpenCV 构建方式；如遇问题可保存为 AVI 或使用 ffmpeg。

练习 2
- 修改 `webcam_capture.py`，在显示画面上叠加当前帧号（左上角）。

参考答案要点：使用 `cv2.putText(frame, str(frame_id), (10,30), ...)`。

------

## 3. 边缘检测与轮廓（示例）
目标：理解 Canny 边缘检测与轮廓查找，能提取物体轮廓并绘制边界框。

示例：Canny + findContours

```python
# edges_contours.py
import cv2

img = cv2.imread('input.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
blur = cv2.GaussianBlur(gray, (5,5), 0)
edges = cv2.Canny(blur, 50, 150)

# 找轮廓（注意 OpenCV 版本兼容）
contours, _ = cv2.findContours(edges.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

out = img.copy()
for cnt in contours:
    x,y,w,h = cv2.boundingRect(cnt)
    cv2.rectangle(out, (x,y), (x+w, y+h), (0,255,0), 2)

cv2.imshow('edges', edges)
cv2.imshow('contours', out)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

练习 3
- 使用阈值化（`cv2.threshold`）替代 Canny，观察轮廓差异。

参考答案要点
- 应用 `ret, th = cv2.threshold(gray, 128, 255, cv2.THRESH_BINARY)`，然后 `findContours`。

------

## 4. 人脸检测：Haar 与 DNN（示例）
目标：掌握两种人脸检测方法的基本用法与区别，并能在摄像头实时检测人脸。

注意：Haar 是经典轻量方法，适合 CPU；DNN（基于 SSD / ResNet 等）通常更稳健，但需要预训练模型文件。

### 4.1 Haar Cascade（快速上手）
OpenCV 自带部分 Haar cascade xml 文件（若无，可从 OpenCV GitHub 下载）。常用文件：`haarcascade_frontalface_default.xml`。

示例：Haar 人脸检测

```python
# face_haar.py
import cv2

cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')
cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    if not ret:
        break
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    faces = cascade.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5, minSize=(30,30))
    for (x,y,w,h) in faces:
        cv2.rectangle(frame, (x,y), (x+w, y+h), (255,0,0), 2)
    cv2.imshow('haar', frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
```

优点：不需额外模型文件（通常随 opencv 安装），速度快；缺点：对复杂角度、光照不稳健。

### 4.2 DNN 人脸检测（更稳健）
需要两个文件（以 OpenCV 提供的 ResNet-SSD 为例）：
- deploy.prototxt（模型结构）
- res10_300x300_ssd_iter_140000.caffemodel（权重）

可从 OpenCV 的 GitHub 仓库下载这两个文件（在课堂上提供一份或事先放在教学服务器）。

示例：DNN 人脸检测

```python
# face_dnn.py
import cv2
import numpy as np

modelFile = 'res10_300x300_ssd_iter_140000.caffemodel'
configFile = 'deploy.prototxt'
net = cv2.dnn.readNetFromCaffe(configFile, modelFile)

cap = cv2.VideoCapture(0)
while True:
    ret, frame = cap.read()
    if not ret:
        break
    h, w = frame.shape[:2]
    blob = cv2.dnn.blobFromImage(cv2.resize(frame, (300, 300)), 1.0,
                                 (300, 300), (104.0, 177.0, 123.0))
    net.setInput(blob)
    detections = net.forward()
    for i in range(detections.shape[2]):
        confidence = detections[0, 0, i, 2]
        if confidence > 0.6:
            box = detections[0, 0, i, 3:7] * np.array([w, h, w, h])
            (x1, y1, x2, y2) = box.astype('int')
            cv2.rectangle(frame, (x1, y1), (x2, y2), (0, 255, 0), 2)
            cv2.putText(frame, f"{confidence:.2f}", (x1, y1 - 10),
                        cv2.FONT_HERSHEY_SIMPLEX, 0.45, (0,255,0), 1)
    cv2.imshow('dnn', frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
cap.release()
cv2.destroyAllWindows()
```

注意事项
- DNN 模型文件体积较大，请提前下载并放置到示例目录
- 若在没有显卡的设备上运行，降低输入的分辨率或减少帧率以保持实时性

练习 4
- 使用 `face_haar.py` 捕获一张人脸并保存到 `face_<timestamp>.jpg`

参考答案要点
- 当检测到 faces 时用 `cv2.imwrite` 保存对应区域或整帧

------

## 5. 实验小项目（整合练习）
目标：将前述知识点整合成一个小 demo：摄像头检测运动并在画面上标注位置，当检测到人脸时保存并发出提示。

项目要点
- 打开摄像头，连续处理帧
- 使用帧差法或背景建模检测运动（简单方法：两帧差值阈值化）
- 使用 Haar 检测人脸；当检测到人脸且有运动时保存截图并在控制台打印信息

项目参考实现（伪代码要点）

1. 初始化摄像头与人脸 cascade
2. 读取第一帧并做灰度与模糊处理作为基线
3. 循环读取下一帧，计算绝对差并阈值化得到运动掩码
4. 如果运动区域面积超过阈值，则运行人脸检测
5. 若检测到人脸，则保存帧并在窗口/终端提示

该项目可扩展：记录时间戳、保存到指定文件夹、加入声音提示（TTS）或机器人动作触发。

------

## 6. 常见问题与故障排查
- 摄像头打不开：检查设备管理器、排查占用程序（浏览器/会议软件）
- cv2.imshow 无窗口或窗口黑屏：在某些远程环境或无 GUI 的 Linux 上不可用，使用 matplotlib 或保存为文件代替
- 编码/保存失败：检查输出路径权限和可用磁盘空间
- DNN 模型无法加载：确认 `deploy.prototxt` 与 `caffemodel` 路径正确且文件未损坏

------

## 课后作业（建议）
1. 编写脚本从摄像头实时读取并显示灰度图；将按键 `s` 绑定为保存当前帧。
2. 基于 `edges_contours.py`，统计图片中轮廓数目并保存带标注的图片。
3. 改进人脸检测 demo：在检测到人脸时输出信心度并把人脸裁剪保存为单独文件。

参考资料
- OpenCV 官方文档：https://docs.opencv.org/
- Haar cascades：OpenCV 仓库 `data/haarcascades`
- DNN face detection model：OpenCV 示例模型（ResNet-SSD）

---

文件准备者：课程材料自动生成器（可根据硬件环境调整采样率与分辨率）
