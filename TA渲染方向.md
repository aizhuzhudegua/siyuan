# TA渲染方向

# 大纲

![image-20241230181508419](assets/image-20241230181508419-20250209152950-cd4b1il.png)

# 

# 数学软件

https://www.mathcha.io/wa

# [Unity基础](TA渲染方向/unity基础.md)

# [设计模式](TA渲染方向/设计模式.md)

基本方法：

1、封装复杂的方法，隐藏细节

2、对于经常修改的需求提取抽象接口

3、分层解耦

设计模式C++版  
观察者模式  
游戏设计中的设计模式

## 项目

### [红警](TA渲染方向/设计模式/红警.md)

- 状态模式
- 外观模式
- 单例模式
- 中介者模式
- 桥接模式
- 模板模式
- 策略模式
- 模板方法模式
- 工厂模式
- 建造者模式
- 享元模式
- 组合模式
- 命令模式
- 责任链模式
- 观察者模式
- 备忘录模式
- 访问者模式
- 适配器模式

[笔记]: notes\设计模式\学习笔记.md

# 光线追踪

[Whitted风格]: md\whitted风格光线追踪.md
[辐射度量学]: md\辐射度量学.md

# 光线步进

## 未完成

# 算法

## 未完成

[代码随想录]: md\代码随想录.md
[KMP]: md\KMP.md

# C#基础

[C#]: md\C#.md
[unity中的c#]: md\unity中的c#.md

# 骨骼动画

[DynamicBone]: 骨骼动画\DynamicBone.md

# Shader

# 课程笔记

## 未完成

[Kerry]: md\技术美术.md

# 项目

[re4]: re4\re4.md

‍

### Blender导出设置

![image-20250201164108870](assets/image-20250201164108870-20250209153111-j7jn7yo.png)

### Avatar替身系统

#### spine transform has bone length of zero 问题

检查模型骨骼是否有遮挡

#### 创建avatar

![image-20250131210004120](assets/image-20250131210004120-20250209153111-65sffm8.png)

#### 使用动画

![image-20250131212952434](assets/image-20250131212952434-20250209153111-eonekh1.png)

### Animation Rigging

#### 骨骼绘制

![image-20250201111619892](assets/image-20250201111619892-20250209153111-kvxmyt5.png)

### ShaderGraph

### Magica Cloth

依赖：

com.unity.jobs

burst

#### 目录结构

![image-20250202211256781](assets/image-20250202211256781-20250209153111-hg3k9gt.png)

#### 画笔修正

![image-20250202211232746](assets/image-20250202211232746-20250209153111-kbw22lm.png)

#### 参数

##### 主要参数

###### Root Rotation

根骨是否旋转，一般0.5

###### Animation Pose Ratio

自动蒙皮解算，一般0，消耗大

###### Rotation Interpolation

0.5

##### 布料效果

![image-20250202211852548](assets/image-20250202211852548-20250209153111-hyz9z9q.png)

###### Force

![image-20250202214009071](assets/image-20250202214009071-20250209153111-y91v428.png)

damping（阻力）较小时显得布料比较重

StablizationTime 形变恢复时间

###### Angle Restoration

![image-20250202220354183](assets/image-20250202220354183-20250209153111-gg7rmkn.png)

stiffness（刚性）越大布料越硬

Velocity Attenuation（速度衰减）越小越Q弹

Gravity Falloff能够使倒立的状态下维持布料形态，头发应该为1

###### Angle Limit

![image-20250202221859899](assets/image-20250202221859899-20250209153111-x2bdx53.png)

Limit Angle 限制晃动的角度

Stiffness 相当于限制的权重

###### Inertia 惯性

![image-20250202222119995](assets/image-20250202222119995-20250209153111-dsjdtj6.png)

![image-20250202222223542](assets/image-20250202222223542-20250209153111-iyrw8wo.png)

###### 惯性限制

防止速度太快导致布料异常

![image-20250202222425222](assets/image-20250202222425222-20250209153111-p523yho.png)

![image-20250202222552980](assets/image-20250202222552980-20250209153111-gl21mn1.png)

动画自身产生的惯性

![image-20250202222733522](assets/image-20250202222733522-20250209153111-dt52fup.png)

惯性随着深度发送变化，深度是指骨骼离根部的距离

![image-20250202222946729](assets/image-20250202222946729-20250209153111-uh5m7e8.png)

离心力，旋转时布料能否甩起

![image-20250202223301552](assets/image-20250202223301552-20250209153111-jpwhphx.png)

限制每根骨骼的最大速度

![image-20250202223550458](assets/image-20250202223550458-20250209153111-532ne2h.png)

###### 传送判断

一帧之内的判断条件，下面时传送后重置布料解算

![image-20250202223752697](assets/image-20250202223752697-20250209153111-mk0zbtk.png)

##### 布料穿插

Collider Collision设置

点模式和边模式

![image-20250203112624370](assets/image-20250203112624370-20250209153111-b7br6s2.png)

![image-20250203113125394](assets/image-20250203113125394-20250209153111-j77sj6c.png)

##### 形状保持

添加碰撞体之后还需要设置形状保持

![image-20250203135313140](assets/image-20250203135313140-20250209153111-p4vsdxq.png)

按顺序的一圈

![image-20250203141212419](assets/image-20250203141212419-20250209153111-v83fs7s.png)

拖拽力，布料压缩程度，三角形变形程度

![image-20250203141720444](assets/image-20250203141720444-20250209153111-4o0r4xm.png)

##### Movement Limit

![image-20250203144338903](assets/image-20250203144338903-20250209153111-1gb7bui.png)

![image-20250203144852600](assets/image-20250203144852600-20250209153111-qumekma.png)

##### 风力系统

![image-20250204000521991](assets/image-20250204000521991-20250209153111-nww5gf5.png)

![image-20250204000952998](assets/image-20250204000952998-20250209153111-3m2tocp.png)

- 风力权重
- 风频
- 湍流权重
- 噪波混合正弦，0.7
- 一个magica cloth脚本骨骼之间的同步，越大越同步
- 深度权重，一般开一点

![image-20250204001312466](assets/image-20250204001312466-20250209153111-pzxcw6y.png)

- 移动就有风 不需要风场 效果不再是直的

##### 弹簧（breast）

![image-20250204110416252](assets/image-20250204110416252-20250209153111-5qi0ect.png)

### 雨水效果

![image-20250204171146870](assets/image-20250204171146870-20250209153111-zoinmnl.png)

新建一个camera 使他看不到除了粒子系统之外的东西

![image-20250204171233900](assets/image-20250204171233900-20250209153111-zlnxrrw.png)

![image-20250204171316793](assets/image-20250204171316793-20250209153111-ezzadln.png)

### 雨水效果2

#### y轴偏移效果

![image-20250205205651209](assets/image-20250205205651209-20250209153111-5rc9ywa.png)

#### 世界空间下的法线

![image-20250205210953496](assets/image-20250205210953496-20250209153111-fj4rw1n.png)

#### Saturate节点

限制取值在0-1

### 新的输入系统

![image-20250209151608929](assets/image-20250209151608929-20250209153111-hbfjnvi.png)

# 面试资料

https://www.yuque.com/chengxuyuanchangfeng/wg2e4q/ybq3h4cegwcwk8yz#D0VyE

**百人计划：**​[https://www.bilibili.com/video/BV1pJ411z7JD/?spm_id_from=333.337.search-card.all.click](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/BV1pJ411z7JD/%3Fspm_id_from%3D333.337.search-card.all.click)  
**庄懂的TA教程：**​[https://www.bilibili.com/video/BV1sE411g7N9/?spm_id_from=333.337.search-card.all.click](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/BV1sE411g7N9/%3Fspm_id_from%3D333.337.search-card.all.click)  
**Games101：**​[https://www.bilibili.com/video/BV1X7411F744/?spm_id_from=333.337.search-card.all.click](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/BV1X7411F744/%3Fspm_id_from%3D333.337.search-card.all.click)  
**Games104：**​[https://www.bilibili.com/video/BV1oU4y1R7Km/?spm_id_from=333.337.search-card.all.click](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/BV1oU4y1R7Km/%3Fspm_id_from%3D333.337.search-card.all.click)  
**Games202：**​[https://www.bilibili.com/video/BV1YK4y1T7yY/?spm_id_from=333.337.search-card.all.click](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/BV1YK4y1T7yY/%3Fspm_id_from%3D333.337.search-card.all.click)

‍
