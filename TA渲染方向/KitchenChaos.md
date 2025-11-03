# KitchenChaos

- 动画切换与程序逻辑分离
- 玩家输入与游戏逻辑分离

# URP的管线设置

![image](assets/image-20250216222646-zkfru8u.png)

![image](assets/image-20250216222701-wjmenrj.png)

# 代码规范

![image](assets/image-20250217101948-cgl0hlc.png)

# Global Volume（后处理相关）

![image](assets/image-20250217102800-nilv6ft.png)

删除原有Profile

![image](assets/image-20250217102841-zue6xr9.png)

camera中启用后处理

![image](assets/image-20250217103904-ta87xcf.png)

在render pipline确保开启了后处理

![image](assets/image-20250217104323-jlm94pb.png)

# 添加AO

![image](assets/image-20250217120316-58hpfsx.png)

![image](assets/image-20250217120722-jzeoer7.png)

# 垂直同步开关

![image](assets/image-20250217133302-i49hqbz.png)

# [SerializeField]

可以使一个属性是私有的同时允许 inspector 修改

# Animator

关于animation的制作，move到idle的状态希望body不动，所以在idle的第一帧要设置body的位置

![image](assets/image-20250217142045-ut6ej9b.png)

![image](assets/image-20250217142053-ce4j69h.png)

只有对象身上的animator有该animation的状态时才可以切换

![image](assets/image-20250217142402-xgjuwxb.png)

# Cinemachine

添加Virtual Camera

添加柏林噪声，模拟手持相机效果

![image](assets/image-20250217151815-h58ixvs.png)

## 控制cinemachine的相机跟随

cinemachine允许存在多个虚拟相机，通过设置优先级决定谁是主导

![image](assets/image-20250217152603-zb8wyoq.png)

# new Input System

启用

![image](assets/image-20250217160401-tij0eiv.png)

新建player action asset

![image](assets/image-20250217160737-sgp3qxx.png)

内容

![image](assets/image-20250217161243-mlqk365.png)

在player对象上添加player input

![image](assets/image-20250217161356-wcj6ine.png)

或者从asset生成脚本

![image](assets/image-20250217161558-ivod0a5.png)

![image](assets/image-20250217161617-6kvr0l9.png)

GameInput中激活

![image](assets/image-20250217161850-g1fj1he.png)

注意PlayerInputActions对象需要手动释放

虽然理论上对象销毁后事件监听器应该被清理，但由于 Unity 的 Input System 的特殊性（涉及非托管资源和全局状态），显式调用 `Dispose()` 是必要的。这是一种良好的编程习惯，可以避免资源泄漏和潜在的运行时错误。

如果不调用 `Dispose()`，可能会导致：

- 资源泄漏。
- 旧的事件监听器被触发。
- 输入系统状态不一致。

因此，**始终在** **​`OnDestroy`​**​ **中调用** **​`Dispose()`​**  是推荐的做法。

```csharp
private void OnDestroy()
{
        playerInputActions.Player.Interact.performed -= Interact_performed; // Add listener
        playerInputActions.Player.InteractAlternate.performed -= InteractAlternate_performed;
        playerInputActions.Player.Pause.performed -= Pause_performed;

        playerInputActions.Dispose();
}
```

即使添加新的操作模式后脚本内容也会自动更新

![image](assets/image-20250217162747-j9rflzg.png)

连接手柄时可以看到

![image](assets/image-20250217162940-3j6ju3f.png)

添加手柄

![image](assets/image-20250217163215-cqlbhqc.png)

![image](assets/image-20250217163243-q2ivnz4.png)![image](assets/image-20250217163411-zc6q3kg.png)

# 碰撞检测

[射线检测](常用脚本/射线检测实现碰撞检测.md)

# 添加LayerMask

![image](assets/image-20250217202859-m4wstvd.png)

![image](assets/image-20250217203020-ns7ppk2.png)

![image](assets/image-20250217203125-v9dqxrk.png)

# [事件](c#.md#20250217210605-lyq2o0z)

## 自定义事件

![image](assets/image-20250217205536-eq32yt0.png)

## 触发自定义事件的两种写法

判断事件的订阅者是否为空

![image](assets/image-20250217205335-du1gpjf.png)

## 订阅输入系统的事件

![image](assets/image-20250217205637-xljwoc3.png)

## 自定义的EventArgs

```csharp
public event EventHandler<OnSelectedCounterChangedEventArgs> OnSelectedCounterChanged;
public class OnSelectedCounterChangedEventArgs:EventArgs
    {
        public ClearCounter selectedCounter;
    }

// 触发
 OnSelectedCounterChanged?.Invoke(this, new OnSelectedCounterChangedEventArgs
        {
            selectedCounter = selectedCounter
        });
```

# ScriptableObject（享元模式的一种体现）

![image](assets/image-20250219084253-730iqq8.png)

![image](assets/image-20250219084332-6h9ncs6.png)

![image](assets/image-20250219084351-02mo17q.png)

![image](assets/image-20250219084511-skcsj6k.png)

![image](assets/image-20250219084546-xwo447y.png)

# 预制体变体

![image](assets/image-20250219154504-0ra1a9h.png)

# 物体上的UI

![image](assets/image-20250220205102-hb3k8ti.png)

## 用image制作进度条

![image](assets/image-20250220210433-vcwn6fs.png)

![image](assets/image-20250220210447-davi8qb.png)

![image](assets/image-20250220210500-3qsk324.png)

# [协程](KitchenChaos/协程.md)

```csharp
private void Start()
{
	StartCoroutine(HandleFryTimer());
}

private IEnumerator HandleFryTimer()
{
	yield return new WaitForSeconds(1f);
}
```

# Unity不会在inspector中暴露接口

![image](assets/image-20250223215651-f8cfb3a.png)

![image](assets/image-20250223215705-0m7aawu.png)

# 如何显示结构体

![image](assets/image-20250225111649-t1p68ym.png)

![image](assets/image-20250225111705-hlx1f7u.png)

![image](assets/image-20250225111736-sqr5t7x.png)

# UI格子布局

![image](assets/image-20250225165042-uus0cys.png)

![image](assets/image-20250225165050-b34s4mg.png)

# 避免预制件过多的方法（Template）

用一个制作好的Template进行复制

![image](assets/image-20250225203607-hk8ubqv.png)

复制对象

```c#
[SerializeField] private Transform iconTemplate;
...
Transform iconTransform = Instantiate(iconTemplate,transform);
```

# 音乐的优先级

![image](assets/image-20250227171233-66e0pry.png)

# <span id="20250227171307-hgumo6y" style="display: none;"></span>初识TextMeshProUGUI（所在库TMPro）

![image](assets/image-20250302143103-ysx2kpc.png)

要带有LiberationSans SDF才能识别

![image](assets/image-20250302143132-hxxoigc.png)

现在就可以随意修改而不影响其他的文字

![image](assets/image-20250302143550-4xxad5y.png)

# <span id="20250302164606-vqhhwov" style="display: none;"></span>场景切换 SceneManagement

using UnityEngine.SceneManagement

![image](assets/image-20250302173638-bmfn5g2.png)

![image](assets/image-20250302173831-4zjycio.png)

# Canvas设置

![image](assets/image-20250302184316-nl418ne.png)

# <span id="20250302184643-1o4qims" style="display: none;"></span>场景间通信的方式

申明静态类

```public
public static class Loader{ ... }
```

在两个场景之间加入一个Loader场景，场景A调用Load进入Loader场景

![image](assets/image-20250302192713-s2pjf7u.png)

Loader场景的第一帧加载目标场景，由MonoBehaviour.Start调用

![image](assets/image-20250302192801-vqb0sqz.png)

![image](assets/image-20250302192744-ui1w2c0.png)

# 存储变量

```csharp
PlayerPrefs.SetFloat(PLAYER_PREFS_MUSIC_VOLUME , volume);
PlayerPrefs.Save();
```

# 获取绑定的按键

## 定义一个枚举作为抽象层

![image](assets/image-20250303205049-qt48obf.png)

## 从playerAction获取按键字符串

每个action是一个一维数组

![image](assets/image-20250303205130-n4coapw.png)

![image](assets/image-20250303205013-e7vbksp.png)

# 重新分配按键

```csharp
using UnityEngine.InputSystem;

public void RebindBinding(Binding binding, Action onActionRebound)
    {
        playerInputActions.Player.Disable();

        InputAction inputAction;
        int bindingIndex;

        switch (binding)
        {
            default:
            case Binding.Move_Up:
                inputAction = playerInputActions.Player.Move;
                bindingIndex = 1;
                break;
            case Binding.Move_Down:
                inputAction = playerInputActions.Player.Move;
                bindingIndex = 2;
                break;
            case Binding.Move_Left:
                inputAction = playerInputActions.Player.Move;
                bindingIndex = 3;
                break;
            case Binding.Move_Right:
                inputAction = playerInputActions.Player.Move;
                bindingIndex = 4;
                break;
            case Binding.Interact:
                inputAction = playerInputActions.Player.Interact;
                bindingIndex = 0;
                break;
            case Binding.Interact_Alternate:
                inputAction = playerInputActions.Player.InteractAlternate;
                bindingIndex = 0;
                break;
            case Binding.Pause:
                inputAction = playerInputActions.Player.Pause;
                bindingIndex = 0;
                break;
        }

        inputAction.PerformInteractiveRebinding(bindingIndex)
            .OnComplete(callback => {
                callback.Dispose();
                playerInputActions.Player.Enable();
                onActionRebound();

				PlayerPrefs.SetString(PLAYER_PREFS_BINDINGS, playerInputActions.SaveBindingOverridesAsJson());
				PlayerPrefs.Save();
            })
            .Start();
    }
```

## 保存按键

```csharp
PlayerPrefs.SetString(PLAYER_PREFS_BINDINGS, playerInputActions.SaveBindingOverridesAsJson());
PlayerPrefs.Save();
```

## 读取按键

```csharp
playerInputActions =  new PlayerInputActions();
if (PlayerPrefs.HasKey(PLAYER_PREFS_BINDINGS))
{
    playerInputActions.LoadBindingOverridesFromJson(PlayerPrefs.GetString(PLAYER_PREFS_BINDINGS));
}
playerInputActions.Player.Enable();
```

‍

# 手柄死区问题

避免角色漂移

![image](assets/image-20250304142029-gi4uqh7.png)

# UI的EventSystem设置，支持手柄输入

![image](assets/image-20250304152334-minu5j3.png)

## selectColor设置

resumButton.Select();

![image](assets/image-20250304160701-sfoyqps.png)

![image](assets/image-20250304152618-vusf3g2.png)

# 如何在打开其他UI后能够回到本UI

```csharp
// 打开ui调用
Hide();
OptionsUI.Instance.Show(Show);
// 目标ui的申明
public void Show(Action onCloseButtonAction)
{
        this.onCloseButtonAction = onCloseButtonAction;

        gameObject.SetActive(true);

        soundEffectsButton.Select();
}
// 关闭时回调
closeButton.onClick.AddListener(() =>
{
            Hide();
            onCloseButtonAction();
});
```

‍
