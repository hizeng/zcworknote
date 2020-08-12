###### 1.实现飘金币

- egret api:坐标，层级对应关系，
- eui 类型



###### 2.还需补充的知识概念（项目）

1.网络通讯接口

2.核心工具类的写法，理解

3.egret项目文件说明 get

4.静态变量，等是ts语法的概念。

 

#### 上午

1.回顾了昨天的10说，当中的入口文件，跟服务器通讯概念模糊等，便浏览了index.html入口文件。其作用是： 结合egret引擎框架，进行相关的配置，并且通过XMLHttpRequest对象，执行加载egret的相关库文件。

[XMLHttpRequest]: https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest

**2.入口文件：index.html**

body标签内含,默认配置，

```html
data-entry-class：文件类名称。
data-orientation：旋转模式。
data-scale-mode：适配模式。
data-frame-rate：帧频数。
data-content-width：游戏内舞台的宽。
data-content-height：游戏内舞台的高。
data-multi-fingered：多指最大数量。
data-show-fps：是否显示 fps 帧频信息。
data-show-log：是否显示 egret.log 的输出信息。
data-show-fps-style：fps面板的样式。支持5种属性，x:0, y:0, size:30, textColor:0xffffff, bgAlpha:0.9
```

关键点：egret.runEgret({}),参数对象

- “renderMode”: 引擎渲染模式，”canvas” 或者 “webgl”，两者有何区别？
- “audioType”: 使用的音频类型，0:默认，2:web audio，3:audio [两者的区别，可以参考文档](https://www.cnblogs.com/martinl/p/6005424.html)
- “calculateCanvasScaleFactor”：屏幕的物理像素适配方法，使用默认的即可

**项目配置文件说明：egretProperties.json.引擎所涉及的配置**。

当中modules字段是指 定义项目中引用的所有库文件。库文件就是封装好的逻辑代码。方便开发者调用，提高开发效率，也就是游戏引擎的核心作用。

第三方库，项目中有使用的场景么？有的话，是有哪些？

**tsconfig配置文件：**编译成js

格式:

{

"index1":{},

"index2":[]

}

 是 Typescript 项目的配置文件，TypeScript 编译器编译代码之前，会首先读取这个配置文件，并根据其中的属性来设置 TypeScript 项目的编译参数。

核心字段：compilerOptions

个人见解：这里的编译并非是底层编译成机器代码，是ts转成js的编码转换过程。

#### 下午：

> 上午的工作，发现，对于前一天的10讲解的某种知识概念，第二天是较为之模糊而且导致的结果是，容易忘记。所以，加深理解是非常有必要的事。

回顾，早上定下来的计划。关于某个需求的实现。下午，应该要围绕这个计划进行，毕竟，日常开发就是做这些事情。

休息时候，看到有关评论程序员职业发展的文章，说明要改变打法，在日后的工作中，要多加注意，避免重复上一年的错误。

##### egret框架的显示对象的坐标。

坐标：**XY轴**。

这里的原点并非是固定的，用新的概念描叙：是**锚点**。

而且，显示对象的数量增多，那么在<u>**舞台**</u>上的位置关系，就会出现重叠的现象。如何区分？

利用**层级关系**，那么结合坐标。就产生了，**相对坐标系**的概念。

> 我们都对面向对象编程。而对象是与原型，实例，等相关。要从理论知识，带到实际对应的开发当中，这才是真正要做的事。也才会加深这样编程思想的认识。

舞台，就是数据最终渲染的地方。那么，对于egret框架，我们如何利用它？那就是通过实例化对象，来调用它封装好的对象的属性，方法。而底层如何讲代码渲染成图像，这里，就不做延伸。

那么，egret有哪些常用的对象，而项目中又有些比频繁使用，结合这次需求，我们尝试总结分析一下：

**常用的对象（类）**

DisplayObject:显示对象基类，所有显示对象均继承自此类

Bitmap:位图，用来显示图片

Shape:用来显示矢量图，可以使用其中的方法绘制矢量图形

TextField: 文本类

BitmapText:位图文本类 (项目中没有使用)

DisplayObjectContainer:显示对象容器接口，所有显示对象容器均实现此接口

Sprite:带有矢量绘制功能的显示容器

Stage:舞台类

小结：比较容易混淆的DisplayObject,DisplayObjectContainer.Shape,Sprite。还有一个Stage.

继承关系：

DisplayObjectContainer => DisplayObject

Bitmap.Shape,TextField,BitmapText=>DisplayObject

Sprite,Stage => DisplayObjectContainer



**由于网站的文档简单，便通过源码的注释 ，方便后续复习**。补充说明：DOContainer,是基本显示列表构造块：一个可包含子项的显示列表节点。

```js
 * DisplayObject 类是可放在显示列表中的所有对象的基类。该显示列表管理运行时中显示的所有对象。使用 DisplayObjectContainer 类排列
 * 显示列表中的显示对象。DisplayObjectContainer 对象可以有子显示对象，而其他显示对象（如 Shape 和 TextField 对象）是“叶”节点，没有子项，只有父级和
 * 同级。DisplayObject 类有一些基本的属性（如确定坐标位置的 x 和 y 属性），也有一些高级的对象属性（如 Matrix 矩阵变换）。<br/>
 * DisplayObject 类包含若干广播事件。通常，任何特定事件的目标均为一个特定的 DisplayObject 实例。例如，added 事件的目标是已添加到显示列表
 * 的目标 DisplayObject 实例。若只有一个目标，则会将事件侦听器限制为只能监听在该目标上（在某些情况下，可监听在显示列表中该目标的祖代上）。
 * 但是对于广播事件，目标不是特定的 DisplayObject 实例，而是所有 DisplayObject 实例（包括那些不在显示列表中的实例）。这意味着您可以向任何
 * DisplayObject 实例添加侦听器来侦听广播事件。
```
##### 对于项目的使用场景：

Bitmap:获的奖励时的特效，此时需要添加图片资源，就需要用到 new egret.Bitmap()来创建新的对象。

Shape:进度条的遮罩。通常会结合数学基本的三角函数，圆周率等等。用到的时候，在查阅相关用法，自带的一些绘制方法：

Sprite:动态生成二维码，通过结合qr.QRCode.create()使用。

TextField:使用其子类 eui.Lable

###### 延伸问题：

eui.UIComponent的实现。

> 当未知的问题过多，总是想不断拓展，这样有个危险的弊端。会容易忘记侧重解决的问题。

小结：基本实现动画效果，但是远不符合实际项目需求。同时，对于未知的知识点，或者不熟练会出现这样的结果：花大量时间去查阅相关文档，理解。而最终却是花10分钟的时间，敲代码，就把问题处理掉。虽然问题目前来看，也是非常简单。

##### 主要问题整理

1.编程语言：类之间的属性，方法，相互调用理解不深，导致实现想法时，总会出错。

2.egret框架：常用的对象，有结合项目场景，初步加深印象。但是，具体的实现，拓展，还需要大量工作应用才可。















