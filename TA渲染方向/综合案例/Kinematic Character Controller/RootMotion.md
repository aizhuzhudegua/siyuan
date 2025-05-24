# RootMotion

- RootMotion会根据动画上一帧的相对位置和相对转角，获得一个变换矩阵，之后游戏对象的运动由矩阵获得
- 启用Animator的RootMotion，物体变换的控制权交给动画
- ![image](assets/image-20250212112656-zue73h7.png)
- 在开启RootMotion的对象上使用OnAnimatorMove，物体的移动会交由脚本控制
- ![image](assets/image-20250212164009-fjjfptn.png)
- RootMotion在Generic动画中就是将根骨骼的运动应用到游戏对象上
- ![image](assets/image-20250212165659-2x32j7j.png)
- Bake into pose是指将rootmotion当作骨骼动画处理，这部分的root motion就无法影响角色运动，绿色表示可以勾选
- ![image](assets/image-20250212175726-c0o2n88.png)
- humanoid动画中会计算一个RootPosition表示根骨骼，rootMotion根据这个根骨骼影响到对象
- ![image](assets/image-20250212190846-fgmehvp.png)

‍

## On AnimationMove的刷新时机

要注意在此时赋予角色速度会不会与物理引擎冲突

![image](assets/image-20250212195800-smjcbeh.png)

‍
