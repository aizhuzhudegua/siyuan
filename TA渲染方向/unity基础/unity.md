# unity

[TOC]

# unity的架构

![image-20231201145508727](C:\Users\王周凯\AppData\Roaming\Typora\typora-user-images\image-20231201145508727.png)

# C#的反射机制

编译器会为每个类生成**Type**的描述

![image-20241007094420234](assets/image-20241007094420234-20250209173613-aztq79v.png)

例如：

![image-20241007094559968](assets/image-20241007094559968-20250209173613-2i86zwm.png)

‍

![image-20241007100136517](assets/image-20241007100136517-20250209173613-hke4v9f.png)

代码实现：

![image-20241007100156637](assets/image-20241007100156637-20250209173613-37kvb9i.png)

![image-20241007100136517](assets/image-20241007100136517-20250209173613-19icpps.png)

![image-20241007100245538](assets/image-20241007100245538-20250209173613-6obiuoj.png)

‍

**在unity中脚本的名字必须和类名相同，这是由于创建脚本实例的时候需要读取文件名/类名来创建类**

# 常用操作

- Alt+RMB 缩放
- Alt+RML 旋转
- 中键 平移
- F 置于视图中心
- backspace 回退
- gameobject中选中camera然后 algin with view，可使scene和game视角一致
- edit中 lockViewToSelected
- ctrl+移动 增量移动
- v 顶点对齐
- ![image-20241017203052864](assets/image-20241017203052864-20250209173613-gdlpb7l.png)

# 常用设置

- 在increment snapping 设置旋转角度

![image-20241017151406130](assets/image-20241017151406130-20250209173613-0o6c56b.png)

# 约定

- 一格约定为1m

# 坐标

左手系，与opengl的z轴相反

## 局部坐标（local）（Space.Self）

每个物体包括相机都有：x = right，y = up，z = forword

![image-20241017160822955](assets/image-20241017160822955-20250209173613-3b6drcg.png)

![image-20241007152922933](assets/image-20241007152922933-20250209173613-0djdl1u.png)

## global 全局/世界坐标

## 屏幕坐标

![image-20241005222439263](assets/image-20241005222439263-20250209173613-yc30any.png)

#### 获取屏幕尺寸

![image-20241005222554780](assets/image-20241005222554780-20250209173613-8jppgpj.png)

#### 获取一个物体在屏幕上的位置

Z值是离摄像机的距离

![image-20241005222811702](assets/image-20241005222811702-20250209173613-zjhq3oi.png)

![image-20241005222936667](assets/image-20241005222936667-20250209173613-yqa3bq6.png)

#### 判断一个物体是否出了屏幕

![image-20241005223143062](assets/image-20241005223143062-20250209173613-w2yyomn.png)

# 颜色空间

gamma和linear具有不同的表现

![image-20241025221849904](assets/image-20241025221849904-20250209173613-dd58b5j.png)

# 空物体

组织和管理其他节点

# 层级关系

Unity的父子节点关系是由**Transform**组件来维持的

gameObject可以忽略

## 获取子节点数量

```c#
int childCount = this.transform.childCount;
```

## 获取子节点

![image-20241006161908386](assets/image-20241006161908386-20250209173613-ubqiv5l.png)

![image-20241006162315551](assets/image-20241006162315551-20250209173613-q1ixbmc.png)

![image-20241006162623281](assets/image-20241006162623281-20250209173613-tvztg1b.png)

## 获取父节点

![image-20241006162016350](assets/image-20241006162016350-20250209173613-m5y0cmm.png)

## 设置父级

![image-20241006162830080](assets/image-20241006162830080-20250209173613-o5rwxf2.png)​

## 从根开始查找

![image-20241006163023017](assets/image-20241006163023017-20250209173613-z9ftocl.png)

# 外部模型

## FBX：unity标准格式

修改材质的方式

1、材质重映射

![image-20241005151542815](assets/image-20241005151542815-20250209173613-2i22gg4.png)

2、使用外部材质

![image-20241005151623906](assets/image-20241005151623906-20250209173613-zshpb3j.png)

3、分解重组

# 组件

## 1、Audio souce

属性

- Audio clip 音频源
- 自动播放

![image-20241005220450442](assets/image-20241005220450442-20250209173613-jg1xdbn.png)

## 2、transform（基础组件，无法删除）

Inspector显示的transform是**相对坐标**

## 3、脚本组件

- 文件名就是类名
- 反射机制实现的

# 运行时的参数如何保留

![image-20241005215635808](assets/image-20241005215635808-20250209173613-1ud0pkc.png)

![image-20241005215712336](assets/image-20241005215712336-20250209173613-rxwaoum.png)

# 脚本

## 属性

![image-20241025091008498](assets/image-20241025091008498-20250209173613-k1b61x0.png)

## 注解编程

```c#
[Tooltip("y轴向的角速度")]
public float rotateSpeed = 5.0f; // 30°/s
```

![image-20241005204733703](assets/image-20241005204733703-20250209173613-o4rhowq.png)

### 常用注解

https://blog.csdn.net/mr_five55/article/details/134721810

## 消息函数

Awake/Start只执行一次

![image-20241005202819514](assets/image-20241005202819514-20250209173613-s0zwecn.png)

## 脚本执行顺序

每一阶段的执行顺序是不确定的，但是阶段是有顺序的

![image-20241005203107032](assets/image-20241005203107032-20250209173613-qk5id2p.png)

优先级的设定——值越小优先级越高，默认全都是0

![image-20241005203454081](assets/image-20241005203454081-20250209173613-p43sa8u.png)

## 脚本参数

public修饰

## 参数的赋值顺序

1、public float rotateSpeed = 5.0f;

2、inspector

![image-20241005205258733](assets/image-20241005205258733-20250209173613-rpfychi.png)

3、Awake

4、Start

## 值类型

![image-20241005205433876](assets/image-20241005205433876-20250209173613-aoxskoo.png)

![image-20241005205725324](assets/image-20241005205725324-20250209173613-b9y0agn.png)

## 引用类型

![image-20241005205942781](assets/image-20241005205942781-20250209173613-8deg2xr.png)

## 常用函数和属性

- ### forward（z）朝向函数

  this.transform.LookAt(targetPos);

  this.transform.LookAt(obj.transform);
- ### 获取scene 中的gameobject

  GameObject.Find("TagName");

  GameObject.Find("a/b/c");
- ### 向量模

  distance.magnitude
- ### 单位向量

  distance.normalized
- ### 旋转

  transform.eulerAngles = new Vector3(x,y,z) // 输入度

  transform.localEulerAngles  = new Vector3(x,y,z) // 输入度
- ### 限制帧率

  Application.targetFrameRate = 60; // 16.7ms

## 获取transform的坐标

```c#
void Start()
{
    GameObject obj = this.gameObject;
    Transform trans = obj.transform;
    // 全局
    Vector3 postion = trans.position;
    // 局部
    Vector3 localPostion = trans.localPosition;
    Debug.Log(postion.ToString("F3"));
    Debug.Log(localPostion.ToString("F3"));
    Debug.Log(obj.name); 
}
```

![image-20241005152819127](assets/image-20241005152819127-20250209173613-oqx48xl.png)

## 帧更新

帧更新时间是不固定的

```c#
void Update()
{
    // Debug.Log("现在的时间是: " + Time.time);
    Debug.Log("帧生成时间差: " + Time.deltaTime);
}
```

锁帧率

```c#
void Start()
{
    Application.targetFrameRate = 60; // 16.7ms
}
```

## 利用transform组件移动

并不是匀速的，因为帧生成不稳定

```c#
void Update()
{
    Vector3 pos = this.transform.localPosition;
    pos.x += 0.01f;
    this.transform.localPosition = pos;
}
```

匀速的运动

```c#
void Update()
{
    // 3m/s
    float speed = 3.0f;
    float distance = Time.deltaTime* speed;
    Vector3 pos = this.transform.localPosition;
    pos.x += distance;
    this.transform.localPosition = pos;
}
```

等价的 Translate(dx,dy,dz,space)

- Space.World
- Space.Self // 默认

```c#
void Update()
{
    // 3m/s
    float speed = 3.0f;
    float distance = Time.deltaTime* speed;
    // 向右移动
    this.transform.Translate(distance, 0, 0);
}
```

## 射线检测实现Moba移动

目前存在射线击中自己时的bug

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Demo : MonoBehaviour
{
    // Start is called before the first frame update
    private Camera mainCamera;
    void Start()
    {
        // TODO 获取相机
        mainCamera = Camera.main.GetComponent<Camera>();
        Application.targetFrameRate = 60; // 16.7ms
    }

    // Update is called once per frame
    private Vector3 targetPos;
    void Update()
    {
        if(Input.GetMouseButton(0))
        {
            Ray ray = mainCamera.ScreenPointToRay(Input.mousePosition);
            RaycastHit hit;
            if (Physics.Raycast(ray, out hit))
            {
                targetPos = hit.point;
                // 看向目标
                this.transform.LookAt(targetPos);
            }
        }
        // 停止条件
        float distance = (targetPos - this.transform.position).magnitude;
        if (distance > 0.5)
        {
            // 移动
            // 3m/s
            float speed = 3.0f;
            float deltaDistance = Time.deltaTime * speed;
            this.transform.Translate(0, 0, deltaDistance, Space.Self);
        }
        
    }
}

```

## 旋转

读取 .eulerAngles 属性时，Unity 会将四元数的旋转内部表示形式转换为 Euler 角。因为使用欧拉角表示任何给定旋转的方法不止一种，所以读回的值可能与分配的值完全不同，**在实现递增时尽量避免使用Rotate或者读取eulerAngles**，Rotate内部实现读取了 .eulerAngles

unity inspector上的rotation是一个**四元数**，不方便代码使用，常用的是**欧拉角**

![image-20241007170628254](assets/image-20241007170628254-20250209173613-n3t3n1c.png)

```c#
void Update()
{
    float speed = 30.0f; // 30°/s
    float deltaAngle = speed * Time.deltaTime;
    Vector3 angle = this.transform.localEulerAngles;
    angle.y += deltaAngle;
    this.transform.localEulerAngles = angle;
}
```

使用Rotate函数

```c#
void Update()
{
    float speed = 30.0f; // 30°/s
    float deltaAngle = speed * Time.deltaTime;
    this.transform.Rotate(0, deltaAngle, 0, Space.Self);
}
```

火控

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class FireLogic : MonoBehaviour
{
    public float bulletSpeed;
    public float bulletLifetime;
    public float shotSpeed; // 射速
    public float rotateSpeed = 1.0f;

    public GameObject bulletPrefab;
    public Transform bulletFolder;
    public Transform firePoint;
    public Transform cannon;

    private bool isFire = false;

    public Vector3 currentEurlerAngles;
    // Start is called before the first frame update
    void Start()
    {
        InvokeRepeating("TestFire", 0.0f, shotSpeed);
    }
    
    // Update is called once per frame
    void Update()
    {
        isFire = Input.GetMouseButton(0);
        if(Input.GetKey(KeyCode.W))
        {
            currentEurlerAngles.x -= rotateSpeed * Time.deltaTime;
        }
        else if (Input.GetKey(KeyCode.S))
        {
            currentEurlerAngles.x += rotateSpeed * Time.deltaTime;
        }
        else if (Input.GetKey(KeyCode.A))
        {
            currentEurlerAngles.y -= rotateSpeed * Time.deltaTime;
        }
        else if (Input.GetKey(KeyCode.D))
        {
            currentEurlerAngles.y += rotateSpeed * Time.deltaTime;
        }
        currentEurlerAngles.x = Mathf.Clamp(currentEurlerAngles.x, -60.0f, 60.0f);
        currentEurlerAngles.y = Mathf.Clamp(currentEurlerAngles.y, -60.0f, 60.0f);
        cannon.localEulerAngles = currentEurlerAngles;
    }

    void TestFire()
    {
        if(isFire)
        {
            GameObject node = Object.Instantiate(bulletPrefab, bulletFolder);
            node.transform.position = firePoint.position;
            node.transform.eulerAngles = cannon.eulerAngles;
            BulletLogic script = node.GetComponent<BulletLogic>();
            script.speed = bulletSpeed;
            script.maxDistance = script.speed * bulletLifetime; // 5m，10s后消失
        }
    }
}
```

## 自转和公转

![image-20241005201015989](assets/image-20241005201015989-20250209173613-qkryai1.png)

a1和地球都位于原点

1、地球自转

```c#
void Update()
{
    float speed = 30.0f; // 30°/s
    float deltaAngle = speed * Time.deltaTime;
    this.transform.Rotate(0, deltaAngle, 0, Space.Self);
}
```

2、卫星公转

```c#
void Update()
{
    float speed = 60.0f; // 30°/s
    float deltaAngle = speed * Time.deltaTime;
    Transform parent = this.transform.parent;
    parent.Rotate(0, deltaAngle, 0, Space.Self);
}
```

## 游戏输入

### 鼠标输入

![image-20241005220914485](assets/image-20241005220914485-20250209173613-udrf44l.png)

![image-20241005221327768](assets/image-20241005221327768-20250209173613-52xeee2.png)

#### 事件探测和状态探测

![image-20241005221708290](assets/image-20241005221708290-20250209173613-claqro7.png)

#### 获取鼠标按下位置

```c#
if ( Input.GetMouseButtonDown( 0 ))
{
    Debug.Log(Input.mousePosition);
}
```

### 键盘输入

![image-20241006112600654](assets/image-20241006112600654-20250209173613-hei5hcg.png)

![image-20241006112730574](assets/image-20241006112730574-20250209173613-pewhuvf.png)

对于每帧都需要判断的逻辑使用**状态**

![image-20241006113320523](assets/image-20241006113320523-20250209173613-a5464ss.png)

## 组件的调用

### 音频组件

```c#
void PlayMusic()
{
    AudioSource audio = this.GetComponent<AudioSource>();
    if(audio.isPlaying)
    {
        audio.Stop();
    }
    else
    {
        audio.Play();
    }
}
```

### 调用其他GameObject的音频组件

```c#
private void Awake()
    {
        Application.targetFrameRate = 60;
        GameObject bgMusic = GameObject.Find("背景音乐");
        bgMusic.GetComponent<AudioSource>().Play(); 
    }
```

unity对音频组件的调用做了优化

1、定义AudioSouce成员而不是GameObject

```c#
public AudioSource bgm;
private void Awake()
{
    Application.targetFrameRate = 60;
    bgm.Play(); 
}
```

2、把带有AudioSource的GameObject拖入能够自动识别

![image-20241006115948393](assets/image-20241006115948393-20250209173613-khxjnt8.png)

### 脚本组件的引用

```c#
Planet planet = earth.GetComponent<Planet>();
planet.rotateSpeed = 30;
```

常用

```c#
public Planet bgm;
```

## 组件通信

![image-20241006153645170](assets/image-20241006153645170-20250209173613-rpjm0sk.png)

## 物体的显示和隐藏

![image-20241006163212707](assets/image-20241006163212707-20250209173613-790o9vh.png)

## 音乐资源的引用——音效

调用**AudioSource**组件播放不同音频资源

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class AudioTest : MonoBehaviour
{
    public AudioClip audioSuccess;
    public AudioClip audioFail;
    // Start is called before the first frame update
    void Start()
    {
        
    }
    // Update is called once per frame
    void Update()
    {
        if(Input.GetKeyDown(KeyCode.A))
        {
            AudioSource audioSource = this.GetComponent<AudioSource>();
            audioSource.PlayOneShot(audioSuccess);
        }
        if (Input.GetKeyDown(KeyCode.D))
        {
            AudioSource audioSource = this.GetComponent<AudioSource>();
            audioSource.PlayOneShot(audioFail);
        }

    }
}
```

## 音乐资源的引用——音乐盒

```c#
void NextSong()
{
    int index = Random.Range(0, songs.Length);
    AudioSource audioSource = this.GetComponent<AudioSource>();
    audioSource.clip = this.songs[index];
    audioSource.Play();
}
```

## 材质资源的引用——三色球

```c#
void ChangeColor()
{
    cur++;
    if(cur >= this.colors.Length)
    {
        cur = 0;
    }
    Material selected = this.colors[cur];
    this.GetComponent<MeshRenderer>().material = selected;
}
```

## 定时器

- 反射机制实现的
- **事件函数的执行是一个大循环，任何的事件调度都塞进 **​***脚本生命周期大循环***​ ** ，在合适的时间发生调度**
- 每次InvokeRepeating都会增加新的调度

![image-20241007090730929](assets/image-20241007090730929-20250209173613-9pbjilj.png)

![image-20241007103044904](assets/image-20241007103044904-20250209173613-87zxr7r.png)

### 弹跳的小球

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class InvokeTest : MonoBehaviour
{
    public float speed = 1.5f;
    // Start is called before the first frame update
    void Start()
    {
        Debug.Log(Time.time);
        this.InvokeRepeating("doSomething", 2 , 2);
    }

    // Update is called once per frame
    void Update()
    {
        this.transform.Translate(0, speed * Time.deltaTime, 0, Space.Self);
    }
    private void doSomething()
    {
        Debug.Log("do something " + Time.time);
        speed = -speed;
    }
}
```

### 红绿灯

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class hongludeng : MonoBehaviour
{
    public Material[] colors;
    private int cur;
    // Start is called before the first frame update
    void Start()
    {
        ChangeColor();
    }

    // Update is called once per frame
    void Update()
    {
        
    }

    void ChangeColor()
    {
        Material color = colors[cur];
        MeshRenderer meshRenderer = GetComponent<MeshRenderer>();
        meshRenderer.material = color;
        if(cur == 0)
        {
            Invoke("ChangeColor", 4);
        }
        else if(cur == 1)
        {
            Invoke("ChangeColor", 4);
        }
        else if (cur == 2)
        {
            Invoke("ChangeColor", 1);
        }
        cur++;
        if (cur >= colors.Length)
        {
            cur = 0;
        }
    }
}
```

## 加速减速

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class jiasujiansu : MonoBehaviour
{
    float a = 100; // 加速度
    float speed = 0;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        // 鼠标按下时加速
        if(Input.GetMouseButton(0))
        {
            // 计算速度的增加
            speed += Time.deltaTime * a;
        }
        // 鼠标松开时减速
        else
        {
            speed += Time.deltaTime * -50;
        }
        if (speed < 0) speed = 0;
        transform.Rotate(0, Time.deltaTime*speed, 0, Space.Self);
    }

}

```

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class jiasujiansu : MonoBehaviour
{
    public float maxSpeed = 720;
    float speed = 0;
    bool isAcc = false;
    // Start is called before the first frame update
    void Start()
    {
        InvokeRepeating("AdjustSpeed", 0.1f, 0.1f);
    }

    // Update is called once per frame
    void Update()
    {
        // 切换开关
        if(Input.GetMouseButton(0))
        {
            isAcc = !isAcc;
        }
        
        if(speed > 0)
        {
            transform.Rotate(0, Time.deltaTime * speed, 0, Space.Self);
        }
    }

    void AdjustSpeed()
    {
        if(isAcc)
        {
            if (speed < maxSpeed)
                speed += 10;
        }
        else
        {
            if (speed > 0)
                speed -= 10;
        }
    }
}

```

## 向量

![image-20241007153636023](assets/image-20241007153636023-20250209173613-jhdcvxr.png)

# 预制体

prefab发生修改，实例也会同步的发生修改

## 创建

![image-20241007155255207](assets/image-20241007155255207-20250209173613-ap1y6ls.png)

## 导出

![image-20241007155822683](assets/image-20241007155822683-20250209173613-3ky7pgh.png)

## 转为普通物体

![image-20241007160133844](assets/image-20241007160133844-20250209173613-cdip18p.png)

## 编辑

![image-20241007160405005](assets/image-20241007160405005-20250209173613-1hvudpl.png)

![image-20241007160418227](assets/image-20241007160418227-20250209173613-9uths3p.png)

![image-20241007160801816](assets/image-20241007160801816-20250209173613-xxqpbx8.png)

![image-20241007160711943](assets/image-20241007160711943-20250209173613-dcxqkil.png)

# 动态创建实例

![image-20241007161449629](assets/image-20241007161449629-20250209173613-3yeggo8.png)

子弹

```c#
void TestFire()
{
    GameObject node = Object.Instantiate(bulletPrefab, bulletFolder);
    node.transform.position = firePoint.position;
    node.transform.eulerAngles = cannon.eulerAngles;
    node.GetComponent<BulletLogic>().speed = 1;
}
```

# 销毁实例

![image-20241007172442571](assets/image-20241007172442571-20250209173613-s07zbxz.png)

# 物理系统

## 刚体

## 碰撞体

![image-20241008161734893](assets/image-20241008161734893-20250209173613-nfatrg3.png)

![image-20241008162408960](assets/image-20241008162408960-20250209173613-wl03fnd.png)

# 天空盒

## 天空盒材质

![image-20241017201657372](assets/image-20241017201657372-20250209173613-h561lss.png)

![image-20241017201735116](assets/image-20241017201735116-20250209173613-332etks.png)

![image-20241008164628831](assets/image-20241008164628831-20250209173613-235mm7k.png)

## 天空盒贴图

天空盒贴图设置为clamp确保无缝

![image-20241017202627993](assets/image-20241017202627993-20250209173613-m55h023.png)

# 光照

## 环境光设置

![image-20241017145815156](assets/image-20241017145815156-20250209173613-rfy0hz9.png)

# 粒子系统

## 基础参数

![image-20241010123343591](assets/image-20241010123343591-20250209173613-jhzvb49.png)

![image-20241009203847458](assets/image-20241009203847458-20250209173613-nerb410.png)

![image-20241009205015980](assets/image-20241009205015980-20250209173613-ol5anbm.png)

![image-20241009205147897](assets/image-20241009205147897-20250209173613-n8lyrj2.png)

## 粒子发生器

![image-20241009205735254](assets/image-20241009205735254-20250209173613-w439r9v.png)

## 广告牌

![image-20241009210045110](assets/image-20241009210045110-20250209173613-zwjudcm.png)

## 粒子贴图

![image-20241009210155518](assets/image-20241009210155518-20250209173613-9wjuo56.png)

![image-20241009210625572](assets/image-20241009210625572-20250209173613-iu1k8oa.png)

### Additve

![image-20241009212815108](assets/image-20241009212815108-20250209173613-xg9ov3p.png)

黑色叠加

![image-20241009213112066](assets/image-20241009213112066-20250209173613-p1mib2t.png)

### Multiply

Start Color和贴图相乘

### 两个效果叠加

![image-20241009213802142](assets/image-20241009213802142-20250209173613-pecrype.png)

![image-20241009214218073](assets/image-20241009214218073-20250209173613-j7py01h.png)

## 黑底白图

![image-20241010121739237](assets/image-20241010121739237-20250209173613-d9dsinm.png)

![image-20241010121833183](assets/image-20241010121833183-20250209173613-5wz4svf.png)

## 透明底图

![image-20241010122125554](assets/image-20241010122125554-20250209173613-n7lm1o6.png)

![image-20241010122303499](assets/image-20241010122303499-20250209173613-9plt8fa.png)

![image-20241010122431823](assets/image-20241010122431823-20250209173613-my37kvj.png)

![image-20241010122620095](assets/image-20241010122620095-20250209173613-keigjgo.png)

## 区间随机值

![image-20241010123130194](assets/image-20241010123130194-20250209173613-h959it9.png)

## 周期与时长

![image-20241010123440130](assets/image-20241010123440130-20250209173613-6py4voq.png)

## 模拟空间

![image-20241010123903810](assets/image-20241010123903810-20250209173613-72glund.png)

world模式下已经发射的粒子不会随着粒子发射系统移动

![image-20241010124012491](assets/image-20241010124012491-20250209173613-pe5f4u1.png)

## 匀速发射

![image-20241010124149200](assets/image-20241010124149200-20250209173613-ncybh7o.png)

![image-20241010124243430](assets/image-20241010124243430-20250209173613-0r3desr.png)

## 最大粒子数量

![image-20241010124557626](assets/image-20241010124557626-20250209173613-cmd2ntb.png)

## 爆发发射

![image-20241010124729795](assets/image-20241010124729795-20250209173613-el3kqft.png)

一般去掉looping

![image-20241010125121214](assets/image-20241010125121214-20250209173613-cwcspgz.png)

## 爆炸参数

![image-20241010125333286](assets/image-20241010125333286-20250209173613-ld5tuwq.png)

## 发射器形状

![image-20241010125505003](assets/image-20241010125505003-20250209173613-ag88ios.png)

## Cone

![image-20241010130125534](assets/image-20241010130125534-20250209173613-3voy4mo.png)

angle是单边的

## Color Over LifeTime

![image-20241011135515831](assets/image-20241011135515831-20250209173613-w5fu5nx.png)

![image-20241011135827855](assets/image-20241011135827855-20250209173613-8gte03o.png)

### 淡入淡出

![image-20241011135752283](assets/image-20241011135752283-20250209173613-vwk8flz.png)

## 渐变和start color的混合规则

![image-20241011140040163](assets/image-20241011140040163-20250209173613-xeh0b9l.png)

![image-20241011140130648](assets/image-20241011140130648-20250209173613-mu1tfcb.png)

## 大小渐变

![image-20241011150244940](assets/image-20241011150244940-20250209173613-f13pi5a.png)

## 速度控制

![image-20241011151807238](assets/image-20241011151807238-20250209173613-jsqhx4c.png)

![image-20241011154245048](assets/image-20241011154245048-20250209173613-bs7aj1o.png)

## 环绕

![image-20241011154745573](assets/image-20241011154745573-20250209173613-hflrzrk.png)

## 速度叠加

![image-20241011155635381](assets/image-20241011155635381-20250209173613-8817oj4.png)

## 速度调节因子

![image-20241011160326699](assets/image-20241011160326699-20250209173613-41exw7z.png)

![image-20241011160410739](assets/image-20241011160410739-20250209173613-a5kty3v.png)

## 粒子受力

![image-20241011162519805](assets/image-20241011162519805-20250209173613-g074mo0.png)

![image-20241011163106439](assets/image-20241011163106439-20250209173613-jk4ihz2.png)

### 模拟重力

![image-20241011163132594](assets/image-20241011163132594-20250209173613-6k2vq36.png)

### 介质阻力

![image-20241011164601550](assets/image-20241011164601550-20250209173613-d3f4qma.png)

![image-20241011164458837](assets/image-20241011164458837-20250209173613-kag5ly1.png)

### 噪声

![image-20241011164803789](assets/image-20241011164803789-20250209173613-fs1c1xj.png)

## 粒子的旋转

![image-20241011165025285](assets/image-20241011165025285-20250209173613-780ksl0.png)

![image-20241011192258608](assets/image-20241011192258608-20250209173613-ehxtc54.png)

![image-20241011192700555](assets/image-20241011192700555-20250209173613-vwt6wgr.png)

### 花瓣飞舞效果

![image-20241011194522393](assets/image-20241011194522393-20250209173613-mre7j4h.png)

## 拉伸广告牌模式

粒子贴图左边为头部方向，粒子转向头部方向

![image-20241011195853967](assets/image-20241011195853967-20250209173613-q1hs0cu.png)

![image-20241011200004483](assets/image-20241011200004483-20250209173613-q5bhfq6.png)

![image-20241011200819406](assets/image-20241011200819406-20250209173613-egmglde.png)

![image-20241011201101188](assets/image-20241011201101188-20250209173613-q4bvhqf.png)

### 火星飞溅

![image-20241011201641265](assets/image-20241011201641265-20250209173613-n9gkati.png)

## 水平广告牌模式

![image-20241011205835450](assets/image-20241011205835450-20250209173613-hjz1lpk.png)

![image-20241011205752897](assets/image-20241011205752897-20250209173613-oued2ot.png)

### 旋转法门

8s发射一个粒子，一个粒子每秒转45度需要8秒转完一周

![image-20241014202939478](assets/image-20241014202939478-20250209173613-5nafmz5.png)

## 拖尾

![image-20241014204412821](assets/image-20241014204412821-20250209173613-tjqjcdd.png)

![image-20241014204136007](assets/image-20241014204136007-20250209173613-otgpef9.png)

![image-20241014204903816](assets/image-20241014204903816-20250209173613-9mrgloc.png)

### 拖尾的长度

![image-20241014205016308](assets/image-20241014205016308-20250209173613-eaynstm.png)

### 拖尾的宽度

![image-20241014205207161](assets/image-20241014205207161-20250209173613-oxe3p5g.png)

### 拖尾的颜色

![image-20241014210741195](assets/image-20241014210741195-20250209173613-0mqr3dv.png)

![image-20241014210902159](assets/image-20241014210902159-20250209173613-upbc49q.png)

### 拖尾的形状

![image-20241014205549348](assets/image-20241014205549348-20250209173613-0v8tp3o.png)

![image-20241014205801654](assets/image-20241014205801654-20250209173613-kkx9tll.png)

### 烟花爆炸

![image-20241014212748013](assets/image-20241014212748013-20250209173613-1tc7mw5.png)

## Texture Sheet Animation

![image-20241015132752153](assets/image-20241015132752153-20250209173613-bifiijj.png)

![image-20241015132608883](assets/image-20241015132608883-20250209173613-31gjyv9.png)

![image-20241015133439973](assets/image-20241015133439973-20250209173613-1sx7jsp.png)

![image-20241015133946508](assets/image-20241015133946508-20250209173613-vqs8u4i.png)

### 材质的HDR可以调整亮度

![image-20241015133718083](assets/image-20241015133718083-20250209173613-gl75tkb.png)

### 火焰的轴心

![image-20241015133825427](assets/image-20241015133825427-20250209173613-if8rt7f.png)

### 烛火效果

![image-20241015134616387](assets/image-20241015134616387-20250209173613-sooxi47.png)

![image-20241015134821039](assets/image-20241015134821039-20250209173613-kvvgbk9.png)

## 粒子发光

### 携带点光源

![image-20241015135739358](assets/image-20241015135739358-20250209173613-ce8m21v.png)

### Lights模块

![image-20241015141817329](assets/image-20241015141817329-20250209173613-h6g12kl.png)

![image-20241015152402111](assets/image-20241015152402111-20250209173613-rphfrqm.png)

## 空粒子系统

禁用emission的粒子系统

![image-20241016111142585](assets/image-20241016111142585-20250209173613-maci5bw.png)

## 二级粒子

![image-20241016115120352](assets/image-20241016115120352-20250209173613-grwhz9v.png)

![image-20241016114734027](assets/image-20241016114734027-20250209173613-y42mpwg.png)

![image-20241016115031505](assets/image-20241016115031505-20250209173613-8wri1e6.png)

![image-20241016115207566](assets/image-20241016115207566-20250209173613-gyndfgm.png)

### 注意

![image-20241016121216840](assets/image-20241016121216840-20250209173613-kjp207q.png)

![image-20241016193929892](assets/image-20241016193929892-20250209173613-da2e7y4.png)

## 粒子的碰撞

![image-20241016202216441](assets/image-20241016202216441-20250209173613-wzr1i0g.png)

![image-20241016203210402](assets/image-20241016203210402-20250209173613-qx678ap.png)

![image-20241016203336014](assets/image-20241016203336014-20250209173613-xwbgrrb.png)

![image-20241016203609109](assets/image-20241016203609109-20250209173613-k0z82hg.png)

### 粒子碰撞事件

脚本挂在粒子上

![image-20241016211746285](assets/image-20241016211746285-20250209173613-f5ejsp8.png)

## 播放完毕后自毁

![image-20241016214539572](assets/image-20241016214539572-20250209173613-n0gby2e.png)

## 均匀分布

![image-20241016221404906](assets/image-20241016221404906-20250209173613-ifapiu1.png)

![image-20241016221437840](assets/image-20241016221437840-20250209173613-noit6p9.png)

# 动画

![image-20241018142545596](assets/image-20241018142545596-20250209173613-tr0uk54.png)

## 动画曲线

![image-20241018160624961](assets/image-20241018160624961-20250209173613-6cisnd7.png)

![image-20241018161232477](assets/image-20241018161232477-20250209173613-0shnt2l.png)

## 曲线的编辑

![image-20241018162008344](assets/image-20241018162008344-20250209173613-d2ywoog.png)

## 动画事件

![image-20241020203325529](assets/image-20241020203325529-20250209173613-t4er086.png)

## 播放模式

![image-20241020204111364](assets/image-20241020204111364-20250209173613-keibynr.png)

# 动画状态机

![image-20241020204419700](assets/image-20241020204419700-20250209173613-qax8tma.png)

## 绑定动画

![image-20241020210203472](assets/image-20241020210203472-20250209173613-xu45ywl.png)

## 状态转移

![image-20241020211512201](assets/image-20241020211512201-20250209173613-o9zyh1v.png)

## ExitTime

![image-20241020211806838](assets/image-20241020211806838-20250209173613-q5kv35m.png)

## 状态机API

![image-20241020212029028](assets/image-20241020212029028-20250209173613-45aolhw.png)

### 按住不动

![image-20241020212326361](assets/image-20241020212326361-20250209173613-qwy3xgq.png)

## 状态机行为

![image-20241020212753599](assets/image-20241020212753599-20250209173613-dy67da8.png)

![image-20241020212826369](assets/image-20241020212826369-20250209173613-fk2gca0.png)

![image-20241020212928643](assets/image-20241020212928643-20250209173613-w5lhwxm.png)

### 结合ExitTIme 可以在dance退出到idle的时候，用该脚本重置参数

![image-20241020213348913](assets/image-20241020213348913-20250209173613-lkaq0wg.png)

## 精细控制

![image-20241022144006872](assets/image-20241022144006872-20250209173613-4hpuu6l.png)

# 视角跟随

## 方法一：

```c#
ublic class CameraController : MonoBehaviour
{
    public Transform obj;
    private Vector3 distance = new Vector3(0,8,-8);
    // Start is called before the first frame update
    void Start()
    {
    }

    // Update is called once per frame
    void Update()
    {
        transform.position = obj.position + distance;
    }
}
```

## 方法二：

将相机作为玩家的子节点
