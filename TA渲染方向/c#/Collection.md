# Collection

![image](assets/image-20250324105921-rrhbimy.png)

# Array.Sort

从小到大排序

​`Array.Sort(array, (a, b) => a.CompareTo(b));`​

​`Array.Sort(arr, (a,b) => a-b);`​

# 转换

## List转Array

```csharp
List<int[]> res = new List<int[]>();
res.ToArray();
```

## 二维List转二维Array

```csharp
List<List<int>> res = new List<List<int>>();
res.Select(x => x.ToArray()).ToArray();
```

# 遍历

## foreach

只有实现迭代器才可以使用

```csharp
Queue<int> queueList = new Queue<int>();
queueList.Enqueue(1);
queueList.Enqueue(2);
queueList.Enqueue(3);

foreach (int item in queueList)
	Console.WriteLine($"item: {item}");
}
```

## Enumerator

```csharp
Queue<int> queueList = new Queue<int>();
queueList.Enqueue(1);
queueList.Enqueue(2);
queueList.Enqueue(3);
IEnumerator<int> enumerator = queueList.GetEnumerator();
while (enumerator.MoveNext())
{
	Console.WriteLine($"item: {enumerator.Current}");
}
```

## Select

select 返回一个新的IEnumerable

```csharp
List<int> list = new List<int>(new int[] { 1,2,3});
List<int> newList = list.Select((x) =>
{
	return x + 1;
}).ToList();

foreach (var item in list)
{
	Console.WriteLine($"list:[{item}]");
}

foreach (var item in newList)
{
	Console.WriteLine($"newlist:[{item}]");
}

// 输出
list:[1]
list:[2]
list:[3]
newlist:[2]
newlist:[3]
newlist:[4]
```

# Hashtable

```csharp
Hashtable hashtable = new Hashtable();

```

## Hashtable 比较大小（拆箱）

```csharp
Math.Max( (int)hashtable[key],right );
```

## 增

不能存在相同键 

![image](assets/image-20250326204041-ha16d45.png)

## 删

- 只能通过键删除
- 删除不存在的键没反应

![image](assets/image-20250326204132-xu7tkr7.png)

![image](assets/image-20250326204219-qm2am10.png)

## 查

![image](assets/image-20250326204345-djetnbg.png)

Contains通过键查找， 和ContainsKsy同

![image](assets/image-20250326204438-m9ommxx.png)

### 根据值查找

![image](assets/image-20250326204533-1m2fuyq.png)

## 改

![image](assets/image-20250326204654-i4ozt45.png)

## 遍历（四种）

![image](assets/image-20250326205422-1jko202.png)

![image](assets/image-20250326205720-mw4tgcx.png)

# ArrayList

object 类型的数组，因此可以存放任意类型

## 索引器

![image](assets/image-20250324195045-jaih8jj.png)

## 增

![image](assets/image-20250324200124-neqkbwc.png)

![image](assets/image-20250324201017-79us122.png)

## 删

![image](assets/image-20250324200143-3emogq0.png)

![image](assets/image-20250324200202-pyinqv5.png)

## 查   

![image](assets/image-20250324200421-36r02md.png)

![image](assets/image-20250324200844-4eqvmqs.png)

## 改

![image](assets/image-20250324200927-ew99m5b.png)

## 属性

![image](assets/image-20250324201241-lixj4hi.png)

## 装箱拆箱

装箱：值=>引用

拆箱：引用=>值

![image](assets/image-20250324201828-7lyr657.png)

# Stack

## 弹出

### Pop()

## 压栈

### Push()

## 查

### Peek()、Contains()

## 改

### Clear()

## 遍历

### 1、foreach

### 2、转Array

![image](assets/image-20250324210146-ad0ji7j.png)

## 属性

### Count

可以用于判空

# Queue

## 增

![image](assets/image-20250326201925-sdjsi9g.png)

## 取

![image](assets/image-20250326201937-adh5u4b.png)

## 查

![image](assets/image-20250326202033-bjbm0u2.png)

## 改

![image](assets/image-20250326203335-y4lnfx6.png)

## 遍历

![image](assets/image-20250326203517-uopok2f.png)

# 常用泛型数据结构类

很大程度上避免装箱拆箱

![image](assets/image-20250330121259-3ex3ust.png)

# List<T>

## 初始化n个0

```csharp
List<int> dp = Enumerable.Repeat(0, cost.Length).ToList();
```

‍
