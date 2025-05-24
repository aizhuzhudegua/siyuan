# re4

# Blender导出设置

![image-20250201164108870](assets/image-20250201164108870-20250209175128-460bsto.png)

# Avatar替身系统

## spine transform has bone length of zero 问题

检查模型骨骼是否有遮挡

## 创建avatar

![image-20250131210004120](assets/image-20250131210004120-20250209175128-nx3mqu6.png)

## 使用动画

![image-20250131212952434](assets/image-20250131212952434-20250209175128-ml2m7bu.png)

# Animation Rigging

## 骨骼绘制

![image-20250201111619892](assets/image-20250201111619892-20250209175128-9d24ci1.png)

# ShaderGraph

# <span id="20250209175129-3y3n4wn" style="display: none;"></span>Magica Cloth

依赖：

com.unity.jobs

burst

## 目录结构

![image-20250202211256781](assets/image-20250202211256781-20250209175128-ewvg0ru.png)

![image](assets/image-20250313143632-uydbr98.png)

## 画笔修正

![image-20250202211232746](assets/image-20250202211232746-20250209175128-8dmddcs.png)

## 参数

### 主要参数

#### Root Rotation

根骨是否旋转，一般0.5

#### Animation Pose Ratio

自动蒙皮解算，一般0，消耗大

#### Rotation Interpolation

0.5

### 布料效果

![image-20250202211852548](assets/image-20250202211852548-20250209175128-xd8j1wu.png)

#### Force

![image-20250202214009071](assets/image-20250202214009071-20250209175128-iz4hxjo.png)

damping（阻力）较小时显得布料比较重

StablizationTime 形变恢复时间

#### Angle Restoration

![image-20250202220354183](assets/image-20250202220354183-20250209175128-kcnprxg.png)

stiffness（刚性）越大布料越硬

Velocity Attenuation（速度衰减）越小越Q弹

Gravity Falloff能够使倒立的状态下维持布料形态，头发应该为1

#### Angle Limit

![image-20250202221859899](assets/image-20250202221859899-20250209175128-y9lifa2.png)

Limit Angle 限制晃动的角度

Stiffness 相当于限制的权重

#### Inertia 惯性

![image-20250202222119995](assets/image-20250202222119995-20250209175128-zrbsyvl.png)

![image-20250202222223542](assets/image-20250202222223542-20250209175128-omhns6h.png)

##### 惯性限制

防止速度太快导致布料异常

![image-20250202222425222](assets/image-20250202222425222-20250209175128-nq4qf3s.png)

![image-20250202222552980](assets/image-20250202222552980-20250209175128-tliaani.png)

动画自身产生的惯性

![image-20250202222733522](assets/image-20250202222733522-20250209175128-buceqcf.png)

惯性随着深度发送变化，深度是指骨骼离根部的距离

![image-20250202222946729](assets/image-20250202222946729-20250209175128-lq0rels.png)

离心力，旋转时布料能否甩起

![image-20250202223301552](assets/image-20250202223301552-20250209175128-57qy3jd.png)

限制每根骨骼的最大速度

![image-20250202223550458](assets/image-20250202223550458-20250209175128-ffj4dah.png)

##### 传送判断

一帧之内的判断条件，下面时传送后重置布料解算

![image-20250202223752697](assets/image-20250202223752697-20250209175128-1ej9jeb.png)

### 布料穿插

Collider Collision设置

点模式和边模式

![image-20250203112624370](assets/image-20250203112624370-20250209175128-u27b3gj.png)

![image-20250203113125394](assets/image-20250203113125394-20250209175128-dou9xgy.png)

### 形状保持

添加碰撞体之后还需要设置形状保持

![image-20250203135313140](assets/image-20250203135313140-20250209175128-0o80rpz.png)

按顺序的一圈

![image-20250203141212419](assets/image-20250203141212419-20250209175128-jgz2rpo.png)

拖拽力，布料压缩程度，三角形变形程度

![image-20250203141720444](assets/image-20250203141720444-20250209175128-0m83x05.png)

### Movement Limit

![image-20250203144338903](assets/image-20250203144338903-20250209175128-o9z2hv9.png)

![image-20250203144852600](assets/image-20250203144852600-20250209175128-cpqb852.png)

### 风力系统

![image-20250204000521991](assets/image-20250204000521991-20250209175128-uayle2j.png)

![image-20250204000952998](assets/image-20250204000952998-20250209175128-4a0qbt7.png)

- 风力权重
- 风频
- 湍流权重
- 噪波混合正弦，0.7
- 一个magica cloth脚本骨骼之间的同步，越大越同步
- 深度权重，一般开一点

![image-20250204001312466](assets/image-20250204001312466-20250209175128-95mylci.png)

- 移动就有风 不需要风场 效果不再是直的

### 弹簧（breast）

![image-20250204110416252](assets/image-20250204110416252-20250209175128-bnpn1gk.png)

# <span id="20250209175129-vjvtpbw" style="display: none;"></span>雨水效果

![image-20250204171146870](assets/image-20250204171146870-20250209175128-vx3bomv.png)

新建一个camera 使他看不到除了粒子系统之外的东西

![image-20250204171233900](assets/image-20250204171233900-20250209175128-ekorvks.png)

![image-20250204171316793](assets/image-20250204171316793-20250209175128-znmujdi.png)

# 雨水效果2

## y轴偏移效果

![image-20250205205651209](assets/image-20250205205651209-20250209175128-dwmbjdi.png)

## 世界空间下的法线

![image-20250205210953496](assets/image-20250205210953496-20250209175129-u1qj2wa.png)

## Saturate节点

限制取值在0-1

# 新的输入系统

![image-20250209151608929](assets/image-20250209151608929-20250209175129-5orqkqk.png)

#
