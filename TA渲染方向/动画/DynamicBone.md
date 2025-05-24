# DynamicBone

# DynamicBone介绍

基于模拟模拟弹簧振子算法

- Damping：弹簧的摩擦力
- Elasticity：弹簧的弹力
- Stiffness：刚性，限制形变程度
- Inert：惯性

![image-20241226144656039](assets/image-20241226144656039-20250209154022-pvdkb40.png)

虚拟点

![image-20241226151604748](assets/image-20241226151604748-20250209154022-96fkkhu.png)

# 抖动效果

![image-20241226140640025](assets/image-20241226140640025-20250209154022-wgo92m8.png)

# 自定义角色

## 解开prefab

![image-20241226143127257](assets/image-20241226143127257-20250209154022-3z0k7to.png)

## 头发效果

![image-20241226144510317](assets/image-20241226144510317-20250209154022-ewhsie8.png)

## 排除项

排除不需要运动的骨骼节点

![image-20241226151916891](assets/image-20241226151916891-20250209154022-pl46kwp.png)

## 统一管理，添加碰撞

![image-20241226153355973](assets/image-20241226153355973-20250209154022-y57npsy.png)

![image-20241226153415502](assets/image-20241226153415502-20250209154022-ixji4z5.png)

## 飘动效果（风）

### Perlin Noise (柏林函数)设置DynamicBone的重力

```c#
public class DynamicRandomWind : MonoBehaviour
{
    private DynamicBone[] bones;
    public bool isWindActive = true;
    public float windForceValue;

    // Start is called before the first frame update
    void Start()
    {
        bones = GetComponents<DynamicBone>();
    }

    // Update is called once per frame
    void Update()
    {
        Vector3 force = Vector3.zero;
        if (isWindActive)
        {
            force = new Vector3(Mathf.PerlinNoise(Time.time, 0.0f) * 0.005f * windForceValue, 0, 0);
        }
        for (int i = 0; i < bones.Length; i++)
        {
            bones[i].m_Gravity = force;
        }
    }
}
```
