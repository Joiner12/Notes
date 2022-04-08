# Processing

## 什么是Processing



## 为什么要学Processing





## 学习资料

[Processing 入门基础【秒懂小白篇】_升卿的博客-CSDN博客_processing](https://blog.csdn.net/hewes/article/details/76034154)

[一天一点Processing|12网易云音乐动效并不难2——迷幻水波 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/104271430)

经验之谈

[作为一名交互设计师应该如何学习 Processing？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/22017067)

[processing生成设计学习之路 - 知乎 (zhihu.com)](https://www.zhihu.com/column/c_1177899269960450048)

1. [Tutorials / Processing.org](https://processing.org/tutorials/)

2. [Processing编程学习指南（原书第2版） (豆瓣) (douban.com)](https://book.douban.com/subject/26992338/)
3. [The Nature of Code (豆瓣) (douban.com)](https://book.douban.com/subject/20452058/)

## 零碎想法

博客更新

学习节点 多久学习到什么程度

# Processing编程学习指南

## 像素:paintbrush:

**坐标系和像素:pick:**

概念：坐标纸和电脑窗口坐标系都是采用笛卡尔坐标系统(Cartesian coordinate system)，坐标纸和显示器的坐标系不同点：坐标纸，坐标值y轴正半轴朝上，x轴正半轴朝右，原点在中央；电脑窗口，原点在左上角，y轴正半轴朝下，x轴正半轴朝右。显示器显示的最小单位是像素，每个像素就是一个有效坐标点。

![image-20220407143045234](https://cdn.jsdelivr.net/gh/Joiner12/PicBed@main/image-20220407143045234.png)

**绘制基本图形:triangular_ruler:**

Processing基本图形包含：点(point)、线(line)、矩形(rect)、椭圆(ellinpse)、三角形(triangle)、弧线(arc)、正方形(quad)、曲线(curve)等。

**灰度模式:grey_exclamation:**

灰度(grayscale)是一种颜色表示的方法，用一个字节表示的数值表示颜色逐渐从黑色到白色的过渡色。0表示黑色，255表示白色。

![image-20220407144141362](https://cdn.jsdelivr.net/gh/Joiner12/PicBed@main/image-20220407144141362.png)

**RGB颜色模式:computer:**

RGB——数位色彩(digital color)是指混合红(R)蓝(G)绿(B)三种颜色来实现不同的颜色表示。三通道RGB中按照顺序通过颜色混合，表示为(R,G,B)，其中每个值的范围是0-255。除了红蓝绿之外，还有另外一种元素可选，那就是颜色的alpha值，alpha值的0-255。0：完全透明，255：完全不透明。

**HSB颜色模式:taco: **

颜色除了用RBG(alpha)表示外，还可以用HSB颜色模式来表示，H(hue,色调)，S(saturation，饱和度)，B(brightness，亮度)。

**自定义颜色取值范围:sagittarius:**

默认颜色取值范围是0-255，但是这不是processing中颜色的唯一处理方式。计算机内存中，该值有一个计算机存储方式，因此可以支持自定义修改取值范围。

```java
// processing中自定义颜色取值范围的函数
colorMode() 
```

## 交互:first_quarter_moon:

**setup和draw**

processing的代码结构很简单，其通常结构如下：

```java
// Explicitly import library functions
import lib1;
import lib2;

void setup()
{
    // a block of code
}
void draw()
{
    // a block of code
}
    
    
```

运行项目的时候，首先执行一次setup然后执行跳转到draw中，最后不停循环执行draw函数。



