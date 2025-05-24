# UI

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

## 网格布局

![image](assets/image-20250319202238-riv7xeh.png)

### <span id="20250321195159-njxha0m" style="display: none;"></span>实现自动排布并且父物体适应子物体尺寸

![image](assets/image-20250321195228-nbiw8dz.png)

# 点击行为

## 方法一、实现 IPointerClickHandler

## 方法二、Event Trigger

![image](assets/image-20250320145753-sy7sg6k.png)

# RaycastTarget决定UI是否可以点触

![image](assets/image-20250320212213-ylxdtpu.png)

# 设置分辨率缩放

![image](assets/image-20250321091735-mr62r8y.png)

# Scroll View

![image](assets/image-20250321192033-ekwpul7.png)

## 隐藏滚动条

![image](assets/image-20250321192247-9exjqo6.png)

现在才可以隐藏

![image](assets/image-20250321193615-conuz5t.png)

## 开关两种滚动条

![image](assets/image-20250321201636-mb7aib9.png)

# Button

Target Graphic必须设置

![image](assets/image-20250326201356-tymvl33.png)
