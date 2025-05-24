# PlantVsZombie

# 创建序列帧动画

将所有sprite拖到场景中的GameObject

![image](assets/image-20250305202457-ggcvx35.png)

# 层级设置

![image](assets/image-20250305205224-i4tjo91.png)

![image](assets/image-20250305205319-r32n907.png)

# 动画事件

![image](assets/image-20250305211423-b5qbd3c.png)

![image](assets/image-20250305211504-17b9zmj.png)

# 设置image比例

![image](assets/image-20250306094932-h4a8w8g.png)

# 图片进度条

![image](assets/image-20250306100115-9veb6ex.png)

# Grid Layout

![image](assets/image-20250306145827-ph2eo05.png)

lines使用 horizontal

![image](assets/image-20250306145957-apemcqn.png)

linex使用vertical，设置好cell size和box的碰撞体一致

![image](assets/image-20250306150010-43m99i0.png)

![image](assets/image-20250306150150-cqgsj2y.png)

# 标签

给格子打上标签

![image](assets/image-20250306150342-qa24kxs.png)

# Event System

![image](assets/image-20250306154250-3pfq8ki.png)

## 屏幕坐标、UI坐标、世界坐标转换

![image](assets/image-20250306160431-uk33cvz.png)

### 屏幕坐标

![image](assets/image-20250306160555-j9mlf1s.png)

### UI坐标系

![image](assets/image-20250306160646-b70e302.png)

# 刚体和碰撞体

is trigger决定了物体碰撞后时穿过

kinematic 表示不需要物理行为

![image](assets/image-20250306201642-48gdcn7.png)

![image](assets/image-20250306222612-zkjau0d.png)

# 子弹销毁的方式

## 延迟销毁

```csharp
GameObject.Destroy(gameObject, 10);
```

## 碰撞销毁

# 鼠标事件

```csharp
public void OnDrag(BaseEventData data)
    {
        if (curGameObject == null)
        {
            return;
        }
        PointerEventData pointerEventData = data as PointerEventData;
        curGameObject.transform.position = TranslateScreenToWorld(pointerEventData.position);
    }
public static Vector3 TranslateScreenToWorld(Vector3 position)
    {
        Vector3 cameraTranslatePos = Camera.main.ScreenToWorldPoint(position);
        return new Vector3(cameraTranslatePos.x, cameraTranslatePos.y,0);
    }
```

# 判断某一个点击中的Collider

```csharp
Collider2D[] col = Physics2D.OverlapPointAll(TranslateScreenToWorld(pointerEventData.position));
        foreach (Collider2D c in col)
        {
            if (c.tag == TARGET && c.transform.childCount == 0)
            {
                curGameObject.transform.parent = c.transform;
                curGameObject.transform.localPosition = Vector3.zero;
                curGameObject = null;
            }
        }
```

# 判断是否active

```csharp
dark.activeSelf
```

# 很难点击到阳光的问题

## 原因分析

点击击中了格子，射线被格子挡住

## 解决方法

设置阳光的位置，使阳光更接近摄像机

![image](assets/image-20250307215845-2ogkc13.png)

# 使用excel设计关卡

![image](assets/image-20250308095016-bg564xb.png)

## 启动时运行Editor脚本代码

![image](assets/image-20250308103821-oyi3unj.png)

## 读取xlsl并保存为SO

```csharp
using UnityEngine;
using System.IO;
using OfficeOpenXml;
using UnityEditor;
using System.Reflection;
using System;

[InitializeOnLoad]
public class ReadTable
{
    public static bool needRead = false;
    private const string ZOMBIE_SHEET = "僵尸";
    static ReadTable()
    {
        if (! needRead)
        {
            return;
        }

        string path = Application.dataPath + "/Editor/关卡管理.xlsx";
        string assetName = "Level";

        FileInfo fileInfo = new FileInfo(path);

        // 创建序列化类
        LevelData levelData = (LevelData)ScriptableObject.CreateInstance(typeof(LevelData));

        using (ExcelPackage excelPackage = new ExcelPackage(fileInfo))
        {
            ExcelWorksheet workSheet = excelPackage.Workbook.Worksheets[ZOMBIE_SHEET];
            for (int i = workSheet.Dimension.Start.Row + 2; i < workSheet.Dimension.End.Row; i++)
            {
                LevelItem levelItem = new LevelItem();
                Type type = typeof(LevelItem);
                for (int j = workSheet.Dimension.Start.Column; j < workSheet.Dimension.End.Column; j++)
                {
                    FieldInfo variable = type.GetField(workSheet.GetValue(2, j).ToString());
                    string tableValue = workSheet.GetValue(i,j).ToString();
                    variable.SetValue(levelItem, Convert.ChangeType(tableValue, variable.FieldType));
                }
                levelData.levelDataList.Add(levelItem);
            }
        }
        

        AssetDatabase.CreateAsset(levelData,"Assets/Resources/" + assetName + ".asset");
        AssetDatabase.SaveAssets();
        AssetDatabase.Refresh();

    }
    
}
```

# Start在下一帧执行导致的target不正确的问题

在CreateSunDown中创建了太阳并且设置了target，但是由于sun的start在下一帧才会调用，会导致赋值不正确

```csharp
GameObject sun = Instantiate(sunPrefab,bornPos,Quaternion.identity);

float y = Random.Range(leftBottom.y - 80, leftBottom.y - 30);
sun.GetComponent<Sun>().SetTargetPosition(new Vector3(bornPos.x,y,0));
```

![image](assets/image-20250312201647-gxu8b32.png)

![image](assets/image-20250312201656-yvdqf8g.png)

如果把注释打开，值就会被覆盖

# 音效

## PlayOneShot

用于叠加音效，不会覆盖

# 程序动画插件DOTween

Set设置状态，Do执行

## 案例

![image](assets/image-20250320095315-s7vgbap.png)

## 动画序列

![image](assets/image-20250320094839-r0hjvkz.png)

## 回调

![image](assets/image-20250320094942-xksec08.png)

![image](assets/image-20250320095052-3wh9q3v.png)

# 清除补间动画

DOTween.Clear();

## 疑问

![image](assets/image-20250320095216-81x0fwj.png)

# 异步加载场景

```csharp
// 开始加载
AsyncOperation operation = SceneManager.LoadSceneAsync("Menu");
operation.allowSceneActivation = false; // 不立即切换场景

// Update
curProgress = Mathf.Clamp01(operation.progress / 0.9f);
OnSliderValueChange(curProgress);

// 点击后切换
operation.allowSceneActivation = true;
```

# [实现自动排布并且父物体适应子物体尺寸](TA渲染方向/unity基础/UI.md#20250321195159-njxha0m)

# [Json存储](PlantVsZombie/Json存储.md)

‍
