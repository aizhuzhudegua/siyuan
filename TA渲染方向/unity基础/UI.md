# UI

# Unity2D和UI的区别

![image](assets/image-20250601220835-kcz2nad.png)

# EventSystem

事件系统，实现了UI的各种事件

# 设置UI层级

```csharp
head.transform.SetAsLastSibling();
```

# UI的类型

![image](assets/image-20250319095601-gdl6sdm.png)

## UGUI

### 六大基础组件

![image](assets/image-20250319102301-x4gzrtp.png)

![image](assets/image-20250319102439-mfb7lh4.png)

#### Canvas

![image](assets/image-20250603112032-t4wp46q.png)

##### 三种模式

覆盖模式

![image](assets/image-20250319103754-ewqqg1h.png)

相机模式，不推荐把主相机作为渲染相机

关闭主摄像机对UI层的渲染，UI摄像机只渲染UI

![image](assets/image-20250319105220-wrp9gxs.png)

UI摄像机改成Depth only 不覆盖3d物体的渲染

![image](assets/image-20250319105438-d8mcbw1.png)

![image](assets/image-20250319103650-r16awvp.png)

World Space

![image](assets/image-20250319111332-g13tbv7.png)

#### 想要渲染在UI前的物体

![image](assets/image-20250319105855-8a9338d.png)

![image](assets/image-20250319105934-yrohzl9.png)

# 布局

## 锚点

![image](assets/image-20250603103313-nejxc8b.png)

适应父级宽度

![image](assets/image-20250603105936-a3v3j29.png)

## 网格布局

![image](assets/image-20250603102937-drlcqgj.png)

![image](assets/image-20250319202238-riv7xeh.png)

### <span id="20250321195159-njxha0m" style="display: none;"></span>实现自动排布并且父物体适应子物体尺寸

![image](assets/image-20250321195228-nbiw8dz.png)

## 水平/垂直布局

![image](assets/image-20250603103142-vkbind9.png)

# 点击行为

## 方法一、实现 IPointerClickHandler

## 方法二、Event Trigger

![image](assets/image-20250320145753-sy7sg6k.png)

# RaycastTarget决定UI是否可以点触

![image](assets/image-20250320212213-ylxdtpu.png)

# 设置分辨率缩放

![image](assets/image-20250321091735-mr62r8y.png)

# Scroll View

content里面才是内容，scrollbar是根据content内容大小缩放的

![image](assets/image-20250321192033-ekwpul7.png)

## 隐藏滚动条

![image](assets/image-20250321192247-9exjqo6.png)

现在才可以隐藏

![image](assets/image-20250321193615-conuz5t.png)

## 开关两种滚动条

![image](assets/image-20250321201636-mb7aib9.png)

## 事件

事件的参数是Vector2，代表在x和y方向上滚动了多少，值在0-1之间

![image](assets/image-20250603094854-7xgfxkw.png)

# Button

![image](assets/image-20250601225736-fh1nj1i.png)

Target Graphic必须设置

![image](assets/image-20250326201356-tymvl33.png)

## Navigation（重要）

方向输入来控制选中

![image](assets/image-20250601230347-c4kxwv4.png)

![image](assets/image-20250601230444-epabmtj.png)

## 点击事件

- 把text组件的值修改
- 修改Main Camera的name
- 修改Main Camera的父节点

![image](assets/image-20250601230825-qcjswo6.png)

# Image

![image](assets/image-20250601222145-6fk7hrr.png)

## Set Native Size

设置图片组件大小为sprite原始尺寸

![image](assets/image-20250601222558-ryz7t2y.png)

## Image Type

![image](assets/image-20250601222903-iul1p0e.png)

### Filled 可以用来做进度条之类的效果

### Sliced

需要图片九宫格

![image](assets/image-20250601223836-7kl1g4m.png)

![image](assets/image-20250601224018-6991rs2.png)

- 好处在于拉伸之后可以控制sprite的哪些部分缩放，哪些部分不变
- 如下图水平拉伸只有中间缩放了

![image](assets/image-20250601224111-ba4mtfq.png)

![image](assets/image-20250601224117-v34hdd3.png)

# Text

![image](assets/image-20250601225058-b7zy4vj.png)

## Best Fit

字体自适应文本框大小

# InputField

可以约束输入的内容类型

![image](assets/image-20250602153617-4ukori0.png)

## 事件

![image](assets/image-20250602153931-zkntrzi.png)

# Toggle

## Toggle Group   实现单选

![image](assets/image-20250602154615-bxzkb0d.png)

![image](assets/image-20250602154623-uoopasv.png)

在子级添加Group的引用

![image](assets/image-20250602154713-1hl4t8v.png)

# Dropdown

Dropdown的template是下拉后的样式

![image](assets/image-20250603092140-zt26aix.png)

如果要显示sprite，需要手动指定一个载体

![image](assets/image-20250603093534-tdz3pk8.png)

![image](assets/image-20250603093554-x5wnwi6.png)

事件的回调参数是int

![image](assets/image-20250603093720-qzb8er2.png)

# Mask

## 效果

![image](assets/image-20250603094132-lnqfkju.png)

## 层级结构

![image](assets/image-20250603094159-d158vtk.png)

父节点添加一个Mask组件

![image](assets/image-20250603094227-70lo8p7.png)

# 事件系统

![image](assets/image-20250603165705-k8hcwde.png)
