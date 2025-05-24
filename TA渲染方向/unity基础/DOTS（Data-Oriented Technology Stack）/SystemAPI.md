# SystemAPI

- 只能在ISystem内部调用

# 获取物理世界单例

```csharp
PhysicsWorldSingleton physicsWorldSingleton = SystemAPI.GetSingleton<PhysicsWorldSingleton>();
```

# 查询

```csharp
SystemAPI.Query<RefRO<LocalTransform>, RefRO<FindTarget> ,...>()
```

‍
