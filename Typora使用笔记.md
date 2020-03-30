# Typora使用笔记

## 1.基本语法

### 1.1 目录

```
[toc]
```

### 1.2 删除线

```
~~内容~~
```

~~删除线delete~~

### 1.3 下滑线

使用HTML标签代码实现

```html
<u> 下划线</u>
```

<u> 下划线</u>

### 1.4 上下标

~ 和 ^ 实现上下标

```html
H~2~O  2^3^
```

H~2~O | 2 ^[2]^

### 1.5 高亮

```
==HighLight==
```

==HightLight==

### 1.6 内部跳转

方式一：

```
[跳转](#标签)
```

[跳转](#目录)

方式二：

```html
<!--way1-->
<a href="#anchor">click to anchor</a> <!--点击跳转-->
<!--way2-->
[click to anchor](#anchor)

<a name="anchor"></a>anchorname <!--设置跳转点-->
```

e.g:

👉  <a name="第二种跳转">第二种跳转</a>

😀 [第二种跳转](#第二种跳转)

🍺 <a href="#😀">hre</a>





点击跳转

</a>

### Reference:

[1] MarkDown中文使用指南 https://zhuanlan.zhihu.com/p/39872673

[2] Office Document http://support.typora.io/HTML/

[3] <a name="😀"> </a>实现内部跳转 https://blog.csdn.net/u013502146/article/details/103171825

[4] typora-数学符号 https://blog.csdn.net/wait_for_eva/article/details/84307306