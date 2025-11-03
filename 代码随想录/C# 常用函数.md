# C# 常用函数

# 排序

```csharp
Array.Sort(points, (a,b) =>  a[0].CompareTo(b[0]));
```

# 取最值

```csharp
Math.Min(points[i][1],points[i-1][1]);
```

# [Collection](../TA渲染方向/c#/Collection.md)

# dp数组

```csharp
int[] dp = new int[N];
```

# 字符串处理

```c#
string s;
s.Split('/');
```

# 随机数

```c#
Random random = new Random();
random.Next(1,10); [,)
```

# StringBuilder

```c#
StringBuilder sb = new StringBuilder();
sb.Append();
string str = sb.ToString();
str.Reverse();
```
