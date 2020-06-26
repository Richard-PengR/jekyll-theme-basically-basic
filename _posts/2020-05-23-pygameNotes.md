---
title: "pygame 学习笔记"
categories:
  - coding
excerpt: "争取用这个做大作业"
tags:
  - python
  - coding
last_modified_at: 2020-05-23T30:21:32-22:02
---

这是 <i>Making Games with Python & Pygame</i> 一书的学习笔记与示例代码。

### 一个简单的 Hello World 窗口

```python
import pygame, sys
from pygame.locals import *

pygame.init() # 初始化。在导入 pygame 模块之后总是需要初始化。
DISPLAYSURF = pygame.display.set_mode((400, 300))
pygame.display.set_caption('Hello World')
while True: # main game loop
  for event in pygame.event.get():
    if event.type == QUIT:
      pygame.quit()
      sys.exit()
    pygame.display.update()
```

`DISPLAYSURF` 是一个 <b> Surface 对象</b>，`pygame.display.set_mode()` 函数创建了一个 400 * 300 的窗口（单位为像素），`pygame.set_caption('Hello World')` 设置窗口标题。

一个 8 * 8 的矩形，以左上角为远点，往右为 X 正向，往下为 X 负向。

Surface 对象表示一个矩形的 2D 图像，可以通过调用 pygame 中的绘制函数来改变 Surface 对象的像素。`pygame.display.set_mode()` 返回的对象叫做“显示 Surface 对象”（display surface），当调用 `pygame.display.update()` 函数时，“显示 Surface 对象”就会显示到窗口中。在这个程序中 `DISPLAYSURF` 这个 Surface 对象并没有改变，因此每调用一次 `pygame.display.update()` 程序就会重新绘制一遍相同的黑色图像。

`while` 循环是<b>游戏循环（主循环）</b>。主循环中主要做三件事情：处理时间、更新游戏状态、在屏幕上绘制游戏状态。游戏状态是游戏程序中所有变量的一组值。

事件即 <b>Event 对象</b>，由 `pygame.event.get()` 得到。事件包括但不限于鼠标点击、键盘按键等。事件分为很多类型，有 Event 对象的成员变量那个 `type` 得到，即 `event.type`。`QUIT` 是 `pygame.locals` 中的一个常量，代表一种事件类型。`pygame.locals` 中还有很多其他的事件类型常量。由于在程序第一行写了 `from pygame.locals import *`，因此在使用 `pygame.locals` 中的变量或方法时不需要在写模块名。

### **颜色**

pygame 中的颜色用含 3 个 0 - 255 的整数的 tuple 来表示，这个 tuple 叫做 RGB 值，这三个整数分别代表红、绿、蓝这三种基本色的量。

如果需要颜色的透明效果，则需要给颜色值增加第四个 0 - 255 的整数来表示透明度，称为 alpha 值。需要注意的是，“显示 Surface”是不接受透明颜色绘制的，要使用透明颜色，需要用“显示 Surface”中的方法 `convert_alpha()` 来创建一个新的 Surface 对象：`anotherSurface = DISPLAYSURF.convert_alpha()`，完成绘制之后再将新的 Surface 对象复制（blit）到原来的“显示 Surface”对象中。

pygame 的颜色也可以用 `pygame.Color` 对象表示，用 `pygame.Color()` 创建：`myColor = pygame.Color(255, 0, 0, 128)`，若使用不透明颜色，也可只传入 3 个参数。

### **矩形**

矩形可用含有 4 个整数的 tuple 表示，四个整数分别代表左上角的 X 坐标、左上角的 Y 坐标、矩形的宽度、矩形的高度，单位是像素。

矩形也可以用 `pygame.Rect` 对象表示，创建时使用：`spamRect = pygame.Rect(10, 20, 200, 300)`。Rect 对象有很多属性（attributes），如下表：

|属性名称|说明|
|----|----|
|`myRect.left`|矩形左边的 X 坐标 int 值|
|`myRect.right`|矩形右边的 X 坐标 int 值|
|`myRect.top`|矩形顶部 Y 坐标 int 值|
|`myRect.bottom`|矩形底部 Y 坐标 int 值|
|`myRect.centerx`|矩形中央 X 坐标 int 值|
|`myRect.centery`|矩形中央 Y 坐标 int 值|
|`myRect.width`|矩形宽度 int 值|
|`myRect.height`|矩形高度 int 值|
|`myRect.size`|含两个整数的一个 tuple：`(width, height)`|
|`myRect.topleft`|含两个整数的一个 tuple：`(left, top)`|
|`myRect.topright`|含两个整数的一个 tuple：`(right, top)`|
|`myRect.bottomleft`|含两个整数的一个 tuple：`(left, bottom)`|
|`myRect.midleft`|含两个整数的一个 tuple：`(left, centery)`|
|`myRect.midright`|含两个整数的一个 tuple：`(right, centery)`|
|`myRect.midtop`|含两个整数的一个 tuple：`(centerx, top)`|
|`myRect.midbottom`|含两个整数的一个 tuple：`(centerx, bottom)`|

### 基本的**绘制函数**

先看一段代码：

```python
import pygame, sys
from pygame.locals import *

pygame.init()

# set up the window
DISPLAYSURF = pygame.display.set_mode((400, 300), 0, 32)
pygame.display.set_caption('Drawing')

# set up the colors
BLACK = (  0,   0,   0)
WHITE = (255, 255, 255)
RED   = (255,   0,   0)
GREEN = (  0, 255,   0)
BLUE  = (  0,   0, 255)

# draw on the surface object
DISPLAYSURF.fill(WHITE)
pygame.draw.polygon(DISPLAYSURF, GREEN, ((146, 0), (291, 106), (236, 277), (56, 277), (0, 106)))
pygame.draw.line(DISPLAYSURF, BLUE, (60, 60), (120, 60), 4)
pygame.draw.line(DISPLAYSURF, BLUE, (120, 60), (60, 120))
pygame.draw.line(DISPLAYSURF, BLUE, (60, 120), (120, 120), 4)
pygame.draw.circle(DISPLAYSURF, BLUE, (300, 50), 20, 0)
pygame.draw.ellipse(DISPLAYSURF, RED, (300, 200, 40, 80), 1)
pygame.draw.rect(DISPLAYSURF, RED, (200, 150, 100, 50))

pixObj = pygame.PixelArray(DISPLAYSURF)
# print(DISPLAYSURF.get_locked())
pixObj[380][280] = BLACK
pixObj[382][282] = BLACK
pixObj[384][284] = BLACK
pixObj[386][286] = BLACK
pixObj[388][288] = BLACK
del pixObj
# print(DISPLAYSURF.get_locked())

# run the game loop
while True:
    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            sys.exit()
    pygame.display.update()
```

<b>填充整个 Surface 对象</b>，用 Surface 对象的方法 `fill()`。例：
```python
WHITE = (255, 255, 255)
DISPLAYSURF.fill(WHITE)
```

绘制<b>多边形</b>，使用 `pygame.draw.polygon(surface, color, pointlist, width)`，其中 `pointlist` 是点集，可以用一个元素为坐标二元组的 tuple 表示；`width` 是个可选参数，代表多边形边框的宽度，不传 `width` 参数时默认将颜色填充到整个多边形区域内。例：
```python
GREEN = (0, 255, 0)
pygame.draw.polygon(DISPLAYSURF, GREEN, ((146, 0), (291, 106), (236, 277), (56, 277), (0, 106)))
```

绘制**线段**，使用 `pygame.draw.line(surface, solor, start_point, end_point, width)`，它将从点 `start_point` 画一条线段到 `end_point`。除此之外，还可以使用 `pygame.draw.lines(surface, color, closed, pointlist, width)`，它将从 `pointlist` 中的第一个点开始，依次画一条直线指向下一个点，如果 `closed` 参数填 `True`，将会绘制最后一个点到第一个点的线段，反之则不画。这个功能类似绘制多边形。例：
```python
BLUE = (0, 0, 255)
pygame.draw.line(DISPLAYSURF, BLUE, (60, 60), (120, 60), 4)
```

画**圆**，使用 `pygame.draw.circle(surface, color, center_point, radius, width)`。`center_point` 是圆心，`radius` 是半径。例：
```python
pygame.draw.circle(DISPLAYSURF, BLUE, (300, 50), 20, 0)
```

画**椭圆**，使用 `pygame.draw.ellipse(surface, color, bounding_rectangle, width)`，其中 `bounding_rectangle` 顾名思义“边界矩形”，指能完全装下所画椭圆的最小矩形，它的长为椭圆的长轴，宽为椭圆的短轴，与椭圆同中心。`bounding_rectangle` 可以用 Rect 对象表示，也可以用含四个整数的一个 tuple 表示（这四个整数分别是左上角的 X 与 Y 坐标、宽度、高度）。例：
```python
RED = (255, 0, 0)
pygame.ellipse(DISPLAYSURF, RED, (300, 250, 40, 80), 1)
```

绘制**矩形**，使用 `pygame.draw.rect(surface, color, rectangle_tuple, width)` 表示。同理，`rectangle_tuple` 传一个含四个整数的 tuple 或 Rect 对象。例：

```python
pygame.rect(DISPLAYSURF, RED, (200, 150, 100, 50))
```

创建一个 Surface 对象的**像素集** `pygame.PixelArray` 对象会锁定该 Surface 对象，这个时候可以往上面使用绘制函数画图，但不能使用 `blit()`。可以用 Surface 对象的 `get_locked()` 方法查看其是否被锁定。PixelArray 对象可以用索引来访问。例：
```python
pixObj = pygame.PixelArray(DISPLAYSURF)
pixObj[480][380] # 把坐标为 (480, 380) 的点设置为黑色
```

### 简单的动画

来看一个简单的猫猫移动的动画：

```python
import pygame, sys
from pygame.locals import *

pygame.init()

FPS = 30 # frames per second setting
fpsClock = pygame.time.Clock()

# set up the window
DISPLAYSURF = pygame.display.set_mode((400, 300), 0, 32)
pygame.display.set_caption('Animation')

WHITE = (255, 255, 255)
catImg = pygame.image.load('cat.png')
catx = 10
caty = 10
direction = 'right'

while True: # the main game loop
    DISPLAYSURF.fill(WHITE)

    if direction == 'right':
        catx += 5
        if catx == 280:
            direction = 'down'
    elif direction == 'down':
        caty += 5
        if caty == 220:
            direction = 'left'
    elif direction == 'left':
        catx -= 5
        if catx == 10:
            direction = 'up'
    elif direction == 'up':
        caty -= 5
        if caty == 10:
            direction = 'right'

    DISPLAYSURF.blit(catImg, (catx, caty))

    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            sys.exit()

    pygame.display.update()
    fpsClock.tick(FPS)
```

动画其实是多张不同的图片连续显示。pygame 中制作游戏动画的时候要需要设置**帧速率** FPS（单位 Hz），一般情况下 FPS = 30 或 60 动画就非常流畅。此外，给 FPS 赋值后，需要定义一个 `pygame.time.Clock` 对象，在每次游戏循环的末尾调用这个对象中的 `tick()` 方法来保证最大帧速率就是我们所定义的 FPS。

如果我们需要**加载外部图像**（PNG，JPG等），我们需要调用`pygame.image.load()`函数，函数的参数为图像的文件名字符串。这个函数返回另外一个 Surface 对象，这个 Surface 对象上存储有我们所需要的图片，但我们需要在“显示 Surface 对象”上加载这张图片，这时就需要将存储图像的 Surface 对象复制（blit）到“显示 Surface 对象”上，调用“显示 Surface 对象”的方法 `blit()` 。例：

```python
catImg = pygame.image.load("cat.png") # 创建外部图像的 Surface 对象
DISPLAYSURF.blit(catImg, (catx, caty)) # 将外部图像的 Surface 对象复制到“显示 Surface”，图像复制到的位置的左上角坐标为 (catx, caty)
```

此外，pygame 还有设置字体、播放声音的功能，此处暂不提。

---
