# Navigation

# 2022版本需要现在WIndos=》Package导入

![image](assets/image-20250605161359-q5m8c85.png)

# Bake完成

![image](assets/image-20250605162006-huhop8j.png)

![image](assets/image-20250605161949-qr5k9sr.png)

# 代码控制

![image](assets/image-20250605162442-hskjv2n.png)

```c#
    void Update()
    {
        agent.SetDestination(target.position);
        if (Input.GetKeyDown(KeyCode.Space))
        {
            agent.isStopped = !agent.isStopped;
        }
    }
```

# 面板属性

## Agent面板

这里代表一种类型，无论如何修改，对最终结果都不影响

![image](assets/image-20250605221219-8eo0b4r.png)

## 区域和代价

![image](assets/image-20250605202247-mtz4d36.png)

![image](assets/image-20250605202551-g6kfgbh.png)

## Object 设置

![image](assets/image-20250605202636-v2m0wir.png)

### 把两个桥分别设置为Walkable和Water

![image](assets/image-20250605203447-suawzu8.png)

![image](assets/image-20250605203814-516pc9r.png)

根据角色的宽度设置合适的Radius，否则容易出现角色越出边缘

![image](assets/image-20250605220756-llqj6xj.png)

![005cccc04cf2f39041685ba3ca8ef00](assets/005cccc04cf2f39041685ba3ca8ef00-20250605220540-zbcpec8.png)

Bake![image](assets/image-20250605220559-uemw26r.png)

Agent显示是0.5

![image](assets/image-20250605220921-500zlgq.png)

按照0.5烘焙

![image](assets/image-20250605220956-p2b9dk9.png)

物体贴边

![image](assets/image-20250605221031-qlho84z.png)

## Bake

![image](assets/image-20250605221436-2f9zpa7.png)

![image](assets/image-20250605221447-g5f79em.png)

这脸图上显示的坡度、半径以及高度，是真实影响烘焙的参数

# NavMeshObstacle

![image](assets/image-20250605221644-mqg8uhf.png)

![image](assets/image-20250605221950-3h5526k.png)

## Carve的勾选

勾上，当然如果足够高的话也可以通过，这跟Bake中设置的Agent Height有关

![image](assets/image-20250605222228-bxpuno4.png)

![image](assets/image-20250605222446-c3dzzaz.png)

不勾

![image](assets/image-20250605222250-ice8v8c.png)

# 角色移动案例

![image](assets/image-20250606161415-jbjzzyy.png)

```c#
private void Update()
    {
        if (Input.GetMouseButtonDown(1))
        {
            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);

            if (Physics.Raycast(ray,out RaycastHit hitInfo, 1000))
            {

                Debug.DrawLine(ray.origin, hitInfo.point , Color.red);
                agent.SetDestination(hitInfo.point);
                animator.SetBool("Run", true);
                agent.isStopped = false;

            }
        }

        if (Vector3.Distance(transform.position , agent.destination) <= agent.stoppingDistance)
        {
            animator.SetBool("Run", false);
            agent.isStopped = true;
        }
    }
```
