# FZOJPaintBoard-master
# Developed For FZOJPaintBoard

## 鸣谢

[@ouuan](https://github.com/ouuan) 大佬。本项目所有的源代码均来自于[@ouuan](https://github.com/ouuan) 大佬的项目 [LuoguPaintBoard](https://github.com/ouuan/LuoguPaintBoard)。本人仅作了适配 FZOJ 的修改。

cjh [@ChineseCJH](https://github.com/ChineseCJH) 、lq [@LQ636721](https://github.com/LQ636721) 、yyx [@juruoyyx](https://github.com/juruoyyx) 等人。提供了的帮助。

**特别的**，感谢 YYX 大佬提供了此次 FZOJ 冬日绘板机会。

## 前置准备

本项目需要如下环境：

- [Python3.7](https://www.python.org/downloads/) 及以上版本
- [GIMP](https://www.gimp.org/downloads/)
- Python Pillow 库和 Requests 库

对于 Python 和 pip ：需要添加到环境变量（path）。

安装 Python 和使用 pip 安装 Python 扩展库自行百度学习。



##  处理图像

1. 将文件夹下的 `FZOJPaintBoard.gpl` 复制到 `GIMP安装路径\share\gimp\2.0\palettes` 下。
2. 使用 GIMP 打开原始图像。
3. 图像 → 缩放图像，调整你想要的图像大小。
4. 图像 → 模式 → 索引，使用自定义色板 → FZOJPaintBoard 。**不要勾选“从颜色表中移除无用和重复的颜色”。** “递色”选项自定。
5. 文件 → 导出为 → 选一个路径 → 选择文件类型：**bmp** → 导出。

## 生成图像数据

请在 `data` 文件夹下操作。

1. `python ImageToData.py 图片路径  左上角 x 坐标  左上角 y 坐标`，依次对每张图片运行（此脚本为增量更新）。

## 获取 cookie

1. 打开 FZOJ冬日绘板 页面。（[UOJ](https://www.fzoi.top/paintBoard)  或  [QOJ](https://qoj.fzoi.top/paintBoard)）。
2. 按 `F12` 打开浏览器的 `开发者工具` 或 `DevTools`。
3. 顶栏选择 `网络` 或 `Networks`。刷新页面（`F5` 或 `Crtl + R`）。
4. 单击 `Board` 栏。在弹出的侧栏中选择顶栏的 `cookie` 选项。
5. 全部复制到 `cookies.json`。格式详见下栏。

## 填写 cookie

请在在 源文件夹 下操作。

在 `cookies.json` 文件里按如下格式填写

```json
[
	"UOJSESSID=XXXXXX;connect.sid=XXXXXX; …………",
	"UOJSESSID=XXXXXX;connect.sid=XXXXXX; …………"
]	
```



## 运行脚本

请在 源文件夹 下操作。

使用 `python paint.py mode` 使用脚本。

其中，mode 有如下三种模式：

* order ：每次画需要画的点中在 `board.json` 里最靠前的一个。
* rand ： 每次在需要画的点中随机选择。建议在 cookies 大于等于 5 个时使用。
* battle ：优先画最近被修改过的格子。建议在画完后维护使用。

为防止出现未被捕获的异常，建议循环运行脚本。



## 常量设置

请在 源文件夹 下操作。

在 `paint.py` 开头，有如下常量：

- `WIDTH`：绘板宽度。
- `HEIGHT`：绘板高度。
- `COLORS`：颜色数量。
- `GETTIMEOUT`：单次读取绘板（GET 请求）用时上限。
- `POSTTIMEOUT`：单次画绘板（POST 请求）用时上限。
- `GETBOARDFREQ`：读取绘板间隔时间。
- `COOKIETIMEOUT`：一轮 Cookies 画完之后的等待时间。
- `PAINTBOARDURL`：绘板地址。
- `UA`：header 中使用的 User Agent。

在本项目中已对 FZOJPaintBoard 进行适配，除 `UA` 外不建议也没必要更改。



## 注意事项

- 本项目所有代码均默认适配于 FZQOJ。在 `paint.py` 中，可以根据注释改为适配于 FZUOJ 。
- 多个账号，需要使用多个浏览器获取 cookies。
- 不要过于频繁请求 FZOJ。
