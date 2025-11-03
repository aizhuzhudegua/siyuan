# MMO

# 服务端

- protobuf实现序列化
- 数据包长解决粘包半包

```c++
public static byte[] PackMessage(NetMessage message)
{
    using (MemoryStream ms = new MemoryStream())
    {
        Serializer.Serialize(ms, message); // 序列化消息（得到正文字节）
        byte[] body = ms.ToArray();
        byte[] packet = new byte[body.Length + 4]; // 总长度 = 4字节长度头 + 正文
        
        // 写入4字节长度头（正文长度）
        Buffer.BlockCopy(BitConverter.GetBytes(body.Length), 0, packet, 0, 4);
        // 写入正文
        Buffer.BlockCopy(body, 0, packet, 4, body.Length);
        
        return packet; // 最终发送的数据包：[4字节长度][正文]
    }
}
```

# 连接到数据库

![image](assets/image-20250618150539-b5bcskn.png)

![image](assets/image-20250618150818-kpo67vk.png)

## 点击高级复制以下信息

![image](assets/image-20250618150952-9wg1q4b.png)

```c#
Data Source=JINITAIMEI\MMORPG;Integrated Security=SSPI;Initial Catalog=ExtremeWorld
```

## 粘贴到App.config文件夹下

![image](assets/image-20250618151234-3gwdpyn.png)

# 从模型生成数据库

Entities.edmx

![image](assets/image-20250618151547-emhosph.png)

![image](assets/image-20250618151359-0x6i3s3.png)

![image](assets/image-20250618151345-56i6zuc.png)

## 复制生成的sql的所有内容

![image](assets/image-20250618151611-xuweeol.png)

## 粘贴到数据库执行

![image](assets/image-20250618151701-iv26gxg.png)

# 项目准备

![image](assets/image-20250618153734-9bedutd.png)

## 文档

![image](assets/image-20250618162700-yttlr9s.png)

## 客户端框架

![image](assets/image-20250618154445-g871aud.png)

## 服务端框架

![image](assets/image-20250618154550-1d9joei.png)

# 服务端

基于EF6.0

![image](assets/image-20250618204135-s70cd56.png)

# 设计流程

![image](assets/image-20250619102626-zu6twvi.png)

# 整体设计

![image](assets/image-20250619103322-9as1hwf.png)

# 登录系统

![image](assets/image-20250619103533-ml9jb37.png)

# 服务器架构

![image](assets/image-20250619104048-876p7in.png)

# 游戏框架

![image](assets/image-20250619104125-hvkk6q5.png)

## 细化

![image](assets/image-20250619105113-0lebrh6.png)

# 实体设计

![image](assets/image-20250619105340-uqbwh74.png)

![image](assets/image-20250619105522-ok1fk0u.png)

# 通讯组件

![image](assets/image-20250619151242-f3w3gi8.png)

# 网络模块（NetService、NetClient）

## 客户端连接

```c#
Network.NetClient.Instance.Init("127.0.0.1",8000);
Network.NetClient.Instance.Connect();
```

## 服务端监听

```c#
network = new NetService();
network.Init(8000);
network.Start();
network.Stop();
```

## 测试协议

![image](assets/image-20250619211232-r86afpq.png)

![image](assets/image-20250619211348-1km4u2o.png)

### 启动命令更新协议

以下文件复制到客户端 D:\unityproject\Mymmorpg\Src\Client\Assets\References

![image](assets/image-20250619211704-mxijp4f.png)

### 客户端请求

```c#
void Start()
{

    Network.NetClient.Instance.Init("127.0.0.1",8000);
    Network.NetClient.Instance.Connect();

    SkillBridge.Message.NetMessage msg = new SkillBridge.Message.NetMessage();
	msg.Request = new SkillBridge.Message.NetMessageRequest();
    msg.Request.firstRequest = new SkillBridge.Message.FirstTestRequest();
    msg.Request.firstRequest.Helloworld = "Hello World!";

    Network.NetClient.Instance.SendMessage(msg);
}
```

### 服务端处理

写一个Service

```c#
namespace GameServer.Services
{
    class HelloWoldService :Singleton<HelloWoldService>
    {
        public void Init()
        {
            
        }

        public void Start()
        {
            MessageDistributer<NetConnection<NetSession>>.Instance.Subscribe<FirstTestRequest>(OnFirstTestRequest);
        }

        public void Stop()
        {

        }

        private void OnFirstTestRequest(NetConnection<NetSession> sender, FirstTestRequest request)
        {
            Log.InfoFormat("OnFirstTestRequest: HelloWorld",request.Helloworld);
        }
    
    }
}
```

![image](assets/image-20250619213428-kadwhey.png)

#### 消息分发

![image](assets/image-20250619213822-8vzj9uy.png)

![image](assets/image-20250619213918-skaf6za.png)

![image](assets/image-20250619214024-qbmsh4w.png)

## 总结

服务层订阅了分发器的消息，因此需要修改的有

- 加一条协议
- 分发器添加新的消息
- 新的服务，订阅该消息
- 在GameServer中启动服务

## 用户系统

![image](assets/image-20250623162145-fcjpq08.png)

# 为角色类型定义添加新的属性

![image](assets/image-20250703201810-3ug3j7y.png)

## 生成解决方案，复制D:\unityproject\Mymmorpg\Src\Lib\Common\bin\Debug下文件到D:\unityproject\Mymmorpg\Src\Lib\Common\bin\Debug

![image](assets/image-20250703202509-vqp5ot0.png)

# 服务端端口配置

![image](assets/image-20250708214021-rh99mw3.png)

![image](assets/image-20250708214038-0lw5hej.png)

![image](assets/image-20250708214100-so3rkk7.png)

# 实体关系

![image](assets/image-20250709100559-5vumpa0.png)

# 为什么存储或者传输使用厘米为单位

所有的存储尽量保持int型，不会有误差，乘以100将unity的米转换为厘米，同时可以精确的保留两位两位小数

# 注意吧Data放到Debug目录

![image](assets/image-20250715211601-nvk90ia.png)

# 进入主城

![image](assets/image-20250715212846-s5xgoa5.png)

# 小地图

- 需要Collider的BoundingBox
- 根据偏移量（每个分量归一化）修改地图的pivot

![image](assets/image-20250717202939-mpi4g52.png)

# 修改Table

D:\unityproject\Mymmorpg\Src\Data\Tables

## 加字段

为了和Resource资源映射

![image](assets/image-20250717204022-ywww9b4.png)

![image](assets/image-20250717204126-cscwb6u.png)

### 还要在Server中添加该字段

![image](assets/image-20250717204401-pqqppzh.png)

### 复制Common中的编译结果到客户端

如果修改了协议，把协议一并复制

![image](assets/image-20250717204611-d5j66nx.png)

# 同步

帧同步不利于断线重连，因为本地客户端要模拟断线之前的所有帧

![image](assets/image-20250718205628-op2zoqh.png)

## 同步信息

![image](assets/image-20250718211114-a2rafzo.png)

## 数据流向

![image](assets/image-20250718212535-4r5grl4.png)

# 移动同步

## 关键点

1、三个层次：逻辑层、控制层、网络层

2、控制层更新go位置，逻辑层也在同步更新，都是在FixedUpdate；控制层根据刚体更新，逻辑层则通过直接计算

3、逻辑层在更新的同时将位置同步到网络层

4、在同步包发送的同前需要更新一下网络层和逻辑层的数据

5、第三方客户端收到网络消息同步到逻辑层，由于在第三方客户端我不是Player，所以会使用刚体更新位置

6、误差纠正，在PlayerController的LaterUpdate中，当逻辑层和控制层的误差超过50厘米会强行纠正逻辑层的数据

![image](assets/image-20250721185327-gvb3ty1.png)

![image](assets/image-20250721185538-qhmfoyp.png)

## 一对多的请求-响应

![image](assets/image-20250721194248-ltwjsk0.png)

![image](assets/image-20250722130321-186j98e.png)

# Mono单例需要注意的点

MonoBehaviour对象在每次场景初始化时都会伴随着gameObject实例化，要确保销毁第二次创建的gameObject被销毁：

```c#
    void Awake()
    {
        if (global)
        {
// 当前的Mono实例如果不是自己就销毁
            if (instance != null && instance != this.gameObject.GetComponent<T>())
            {
                Destroy(this.gameObject);
                return;
            }
            DontDestroyOnLoad(this.gameObject);
            instance = this.gameObject.GetComponent<T>();
        }
        this.OnStart();
    }
```

# 关于服务端的Character类

NCharacterInfo同步角色名字地图等信息

NEntity同步角色位置信息

NCharacterInfo中的ID是EntityData的ID

# 传送

![image](assets/image-20250807153308-h30piyu.png)

# 编辑器拓展

```c#
#if UNITY_EDITOR
    private void OnDrawGizmos()
    {
        Gizmos.color = Color.green;
        if (mesh != null)
        {
            Gizmos.DrawWireMesh(mesh,transform.position + Vector3.up * transform.localPosition.y * .5f,transform.rotation,transform.localPosition);
        }
        UnityEditor.Handles.color = Color.red;
        UnityEditor.Handles.ArrowHandleCap(0, transform.position,transform.rotation,1f , EventType.Repaint);
    }
#endif
```

## 在Asset/Editor文件夹下的脚本可以包含到unity菜单

![image](assets/image-20250810204225-0pla4a7.png)

![image](assets/image-20250810204244-tjdbhjb.png)

# UI系统

## 分类

![image](assets/image-20250810204448-gdwky3q.png)

## 框架

![image](assets/image-20250810212947-zn8xz2y.png)

# NPC系统

![image](assets/image-20250812105233-13akule.png)

![image](assets/image-20250812110113-f9d3y8w.png)

![image](assets/image-20250812111006-7fr4wnm.png)

# 道具系统

![image](assets/image-20250812200607-k5bbfcn.png)

## 对外接口

![image](assets/image-20250812201251-xjwcw9i.png)

## 系统组成

![image](assets/image-20250812202829-8qx8z8t.png)

## 职责

管理玩家持有的道具

### 客户端

- 单例ItemManager
- item对接Nitem网络信息

### 服务端

- Character持有ItemManager
- item对接Titem数据库信息

#### 道具信息从哪来

- ItemManager在Character创建的时候构造
- ItemManager构造的时候从数据库读取TItem，写入字典
- 传出Item到info网络信息

# 系统设计的过程

1、设计数据结构：数据库结构、协议结构、配置表结构

# 背包系统

## 背包的作用

![image](assets/image-20250814104456-g8lzxpy.png)

## 系统组成

![image](assets/image-20250814104642-03palrv.png)

## 协议设计

### 背包

```c#
message NBagInfo
{
	int32 Unlocked = 1; // 格子的数量
	bytes Items = 2; // Unlocked * 单个BagItem的长度
}
```

### 发送和响应

```c#
//背包保存
message BagSaveRequest
{
	NBagInfo BagInfo = 1;
}

//背包
message BagSaveResponse {
	RESULT result = 1;
	string errormsg = 2;
}
```

## 创建背包

在创建角色的同时要创建一个初始背包

```c#
// 背包
            var bag = new TCharacterBag();
            bag.Owner = character;
            bag.Items = new byte[0];
            bag.Unlocked = 20;
            character.Bag = DBService.Instance.Entities.CharacterBags.Add(bag);
            character = DBService.Instance.Entities.Characters.Add(character);
            sender.Session.User.Player.Characters.Add(character);
            DBService.Instance.Entities.SaveChanges();
```

# 商店系统

## 功能    

![image](assets/image-20250815152931-n9hlaih.png)

![image](assets/image-20250815153041-qfdd6x2.png)

# 商店配置

```c#
{
  "1": {
    "ID": 1,
    "Name": "药水商店",
    "Description": "什么药水商店",
    "Status": 1
  },
  "2": {
    "ID": 2,
    "Name": "杂货商店",
    "Description": "没有杂货商店",
    "Status": 1
  }
}
```

## NPC调用商店系统

ShopManager的Init中注册了NPC系统的事件，每个NPC配置表持有对应的商店id，在触发事件时传入商店系统

```c#
public void Init()
{
	NPCManager.Instance.RegisterNpcEvent(NpcFunction.InvokeShop,OnOpenShop);
}
```

ShopManager收到事件消息后根据id从商店配置表读取对应的商店配置并初始化对应的UIShop

# ISelectHandler实现选中效果（EventSystem）

## 添加组件

![image](assets/image-20250816142309-1izf07t.png)

## 继承ISelectHandler实现OnSelect

```c#
public void OnSelect(BaseEventData eventData)
    {
        Selected = true;
        shop.SelectShopItem(this);
    }
```

# 状态同步

- 处理一次请求返回多个Response的情况
- 管理角色身上发生的状态STATUS_TYPE，发生的行为STATUS_ACTION ，一起包装到NetMessageResponse

```c#
// 打包状态
public byte[] GetResponse()
        {
            if (response != null)
            {
                if (Character != null && Character.StatusManager.HasStatus)
                {
                    Character.StatusManager.ApplyResponse(Response);
                }
                byte[] data = PackageHandler.PackMessage(response);
                response = null;
                return data;
            }
            return null;
        }
```

### 协议

```c#
message NBagInfo
{
	int32 Unlocked = 1;
	bytes Items = 2;
}

enum STATUS_ACTION {
	UPDATE = 0;
	ADD = 1;
	DELETE = 2;
}

enum STATUS_TYPE {
	MONEY = 0;
	EXP = 1;
	SKILL_POINT = 2;
	ITEM = 3;
}

enum STATUS_SOURCE {
	UPDATE = 0;
	ADD = 1;
	DELETE = 2;
}

message NStatus {
	STATUS_TYPE type = 1;
	STATUS_ACTION  action = 2;
	int32 id = 3;
	int32 value = 4;
}

message StatusNotify {
	repeated NStatus status = 1;
}
```

```c#
message NetMessageResponse{
	UserRegisterResponse userRegister = 1;
	UserLoginResponse userLogin = 2;
	UserCreateCharacterResponse createChar = 3;
	UserGameEnterResponse gameEnter = 4;
	UserGameLeaveResponse gameLeave = 5;

	MapCharacterEnterResponse mapCharacterEnter = 6;
	MapCharacterLeaveResponse mapCharacterLeave = 7;

	MapEntitySyncResponse mapEntitySync = 8;
	
	ItemBuyResponse itemBuy = 10;

	StatusNotify statusNotify = 100; // 状态同步
}
```

## 状态变化

只要金币系统或者其他系统的状态发生变化就记录到状态管理器

## 金币发生改变时加入状态

```c#
public long Gold
        {
            get { return Data.Gold; }
            set
            {
                if (Data.Gold == value)
                {
                    return;
                }
                // 金币发生改变的状态
                StatusManager.AddGoldChange((int)(value - Data.Gold));
                Data.Gold = value;
            }
        }
```

## 道具系统发生变化时加入状态

![image](assets/image-20250816201507-fn297dz.png)

## 客户端

## StatusService

维护一个状态——委托字典

```c#
Dictionary<StatusType, StatusNotifyHandler>
```

在收到服务器消息时触发字典里的事件

```c#
private void OnStatusNotify(object sender, StatusNotify response)
        {
            foreach (NStatus status in response.Status)
            {
                Notify(status);
            }
        }
```

通过注册Service的事件以触发其他系统的更新

## 道具系统的变化会通知到背包系统

例如删除

```c#
private void RemoveItem(int itemId, int count)
        {
            if (!Items.ContainsKey(itemId))
            {
                return;
            }
            Item item = Items[itemId];
            if (item.Count < count)
            {
                return;
            }
            item.Count -= count;
            BagManager.Instance.RemoveItem(itemId, count);
        }
```

# 装备系统

## 编号规则

![image](assets/image-20250818110123-woxw1c4.png)

## 功能

![image](assets/image-20250818111112-67hvtxz.png)

## 数据结构

28个字节

![image](assets/image-20250818111222-u1uhand.png)

## 设计

![image](assets/image-20250818111349-k3snggf.png)

![image](assets/image-20250818111401-xtfcx51.png)

## 协议

### 装备的槽位定义

```c#
enum EQUIP_SLOT {
	WEAPON = 0;
	ACCESSORY = 1;
	HELMET = 2;
	CHEST = 3;
	SHOULDER = 4;
	PANTS = 5;
	BOOTS = 6;
	SLOT_MAX = 7;
}
```

### 在角色定义装备

```c#
message NCharacterInfo {
	int32 id = 1;
	int32 tid = 2;
	string name = 3;
	CHARACTER_TYPE type = 4;
	CHARACTER_CLASS class = 5;
	int32 level = 6;
	int32 mapId = 7;
	NEntity entity = 8;
	
	int64 gold = 9;
	repeated NItemInfo Items = 10;
	NBagInfo Bag = 11;
	bytes Equips = 12;
}
```

### 装别的穿和脱需要协议请求

![image](assets/image-20250818144458-160ks3b.png)

定义了槽位对应的itemId的穿脱（0脱 1穿）

```c#
message ItemEquipRequest {
	int32 slot = 1;
	int32 itemId = 2;
	bool isEquip = 3;
}

message ItemEquipResponse {
	RESULT result = 1;
	string errormsg = 2;
}
```

## 穿装备的过程

- 客户端发送Request
- 服务端收到后交给EquipManager的EquipItem处理
- EquipItem先根据角色身上的ItemManager校验角色是否拥有该物体
- 服务端返回消息，客户端更新

# C#的指针

必须包裹在fixed内部声明，并且声明unsafe

```c#
unsafe void UpdateEquip(byte[] equipData ,int slot ,int itemId, bool isEquip)
        {
            fixed(byte* pt = equipData)
            {
                int* slotid = (int*)(pt + slot * sizeof(int));
                if (isEquip)
                {
                    *slotid = itemId;
                }
                else
                {
                    *slotid = 0;
                }
            }

        }
```

![image](assets/image-20250818184939-pvz6itb.png)

# 任务系统

![image](assets/image-20250819110603-gxxqeft.png)

![image](assets/image-20250819113615-wtalv1c.png)

## 定义不同任务事件

![image](assets/image-20250819113735-3vqejyo.png)

![image](assets/image-20250819130012-0ufyde4.png)

![image](assets/image-20250819130250-z3mqjk2.png)

![image](assets/image-20250819130458-fxcqvx1.png)

## 数据结构

![image](assets/image-20250819131005-hzq33u5.png)

```c#
AddNpcQuest(kv.Value.Define.AcceptNPC, kv.Value);
AddNpcQuest(kv.Value.Define.SubmitNPC, kv.Value);
```

AcceptNPC和SubmitNPC定义了任务从哪个NPC接，提交给哪个NPC

## 与NPC系统的交互

- 提供必要的查询：NPC身上的任务
- 建立NPC与任务的配置表，维护所有任务
- NPC可以根据npcId打开dialog

```c#
private bool DoTaskInteractive(NpcDefine npc)
        {
            var status = QuestManager.Instance.GetQuestStatusByNpc(npc.ID);
            if (status == NpcQuestStatus.None)
            {
                return false;
            }

            return QuestManager.Instance.OpenNpcQuest(npc.ID);
        }
```

## 服务端

- 服务端只需要关心角色接了哪些任务，因此QuestManager是Character的一个属性

# 刷怪系统

![image](assets/image-20250827125939-glx0z1f.png)

## 数据结构

![image](assets/image-20250827130020-6kp74k6.png)

## 系统组成

![image](assets/image-20250827130544-3o08xy0.png)

## 协议

协议复用GameEnter来通知其他客户端有新的怪物生成了

## 模块关系

![image](assets/image-20250827131520-gxknqco.png)

## 导出刷怪点

- 保存当前场景
- 遍历所有场景，查找SpawnPoint对象，保存到每个地图中
- 保存到配置文件，恢复场景

```c#
[MenuItem("Map Tools/Export SpawnPoints")]
    public static void ExportSpawnPoints()
    {
        DataManager.Instance.Load();

        Scene current = EditorSceneManager.GetActiveScene();
        string currentScene = current.name;
        if (current.isDirty)
        {
            EditorUtility.DisplayDialog("提示","请先保存当前场景","确定");
            return;
        }

        if (DataManager.Instance.SpawnPoints == null)
        {
            DataManager.Instance.SpawnPoints = new Dictionary<int, Dictionary<int, SpawnPointDefine>>();
        }

        foreach (var map in DataManager.Instance.Maps)
        {
            string sceneFile = "Assets/Levels/" + map.Value.Resource + ".unity";
            if (!System.IO.File.Exists(sceneFile))
            {
                Debug.LogWarningFormat("Scene {0} not  exitsted!",sceneFile);
                continue;
            }

            EditorSceneManager.OpenScene(sceneFile,OpenSceneMode.Single);

            SpawnPoint[] spawnPoints = GameObject.FindObjectsOfType<SpawnPoint>();

            if (!DataManager.Instance.SpawnPoints.ContainsKey(map.Value.ID))
            {
                DataManager.Instance.SpawnPoints[map.Value.ID] = new Dictionary<int, SpawnPointDefine>();
            }

            // 将出生点加入到对应的地图中
            foreach (var sp in spawnPoints)
            {
                if (!DataManager.Instance.SpawnPoints[map.Value.ID].ContainsKey(sp.ID))
                {
                    DataManager.Instance.SpawnPoints[map.Value.ID][sp.ID] = new SpawnPointDefine();
                }

                SpawnPointDefine def = DataManager.Instance.SpawnPoints[map.Value.ID][sp.ID];
                def.ID = sp.ID;
                def.MapID = map.Value.ID;
                def.Position = GameObjectTool.WorldToLogicN(sp.transform.position);
                def.Direction = GameObjectTool.WorldToLogicN(sp.transform.forward);
            
            }
        }

        DataManager.Instance.SaveSpawnPoints();
        EditorSceneManager.OpenScene("Assets/Levels/" + currentScene + ".unity");
        EditorUtility.DisplayDialog("提示","刷怪点导出完成","确定");
    }
```

## 刷怪规则

- 刷怪规则定义了刷怪点刷新的怪物
- 从刷怪规则中添加对应的刷怪点

```c#
if (DataManager.Instance.SpawnRules.ContainsKey(map.Define.ID))
            {
                foreach (var define in DataManager.Instance.SpawnRules[map.Define.ID].Values)
                {
                    Rules.Add(new Spawner(define, this.map));
                }
            }
```

## 刷怪

怪物作为角色一起回传

```c#
foreach (var kv in MonsterManager.Monsters)
{
	conn.Session.Response.mapCharacterEnter.Characters.Add(kv.Value.Info);
}
```

## 减轻服务器压力

这里可以不发，当产生其他交互时一起返回，即一次请求N次返回

![image](assets/image-20250827210048-7q6se9w.png)

# 好友系统

## 系统结构

![image](assets/image-20250828144920-rutli3p.png)

![image](assets/image-20250828144942-ohhg4p9.png)

## 数据结构

![image](assets/image-20250828145849-0i6vn6d.png)

### 协议

客户端不仅要处理请求，也要处理响应

```c#
	FriendAddRequest friendAddReq = 15;
	FriendAddResponse friendAddRes = 16;

```

## 服务端

- 每个character持有一个characterManager
- SessionManager维护了Session列表，进入游戏的时候Add，退出的时候Remove
- PostResponser

在Enter初始化后处理

```c#
sender.Session.PostResponser = character;
```

### 角色上线时通知他的好友

这里将friendchang设置为了true，这样在map广播的时候就会携带好友列表消息

![f5e8a3eb14d8749caf77ebaa73d194d5](assets/f5e8a3eb14d8749caf77ebaa73d194d5-20250907170333-rv5zitf.png)

后处理携带从数据库更新的好友列表消息

```c#
public void PostProcess(NetMessageResponse message)
        {
            if (friendChanged)
            {
                InitFriends();
                if (message.friendList == null)
                {
                    message.friendList = new FriendListResponse();
                    message.friendList.Friends.AddRange(friends);
                }
            }
            friendChanged = false;
        }
```

### 存在的问题

![image](assets/image-20250907213949-71np2s7.png)

# 组队系统

服务端的队伍信息并未持久化，而是TeamManager维护的，每个队伍维护队长和成员信息

服务端每个成员Character持有队伍的引用和本地时间戳

客户端的队伍信息来自于网络更新，即NTeamInfo，保存在User单例中，只在收到这个Response的时候才更新队伍信息UI。

![image](assets/image-20250909213443-n7xoegn.png)

![image](assets/image-20250909213525-d8rz7x3.png)

## 如何将一个队伍的更新传递到每个人

- 每个角色拥有一个时间戳
- 队伍的更新会修改队伍的时间戳
- 当角色后处理时发现自己的时间戳小于队伍的时间戳就转去处理队伍的后处理，将队伍的更新信息附加到当前会话

 这样就不需要写一个for循环再每次更新队伍信息的时候显式的发送队伍信息，减少消息的发送量

## TeamManager

维护了所有的队伍，新创建的队伍会先从池子里取，如果池子里都在用就new 一个Team

## Team

- 维护了所有的成员
- 更新时会更新时间戳

## Bug修复

修改移动同步的响应，使其可以应用后处理

![image](assets/image-20250913194830-jyn3oz3.png)

注销事件

![image](assets/image-20250913215235-7r9rplh.png)

# 为什么下断点会报错

在多线程环境下会报错，因为一次性无法把所有线程停掉

# 自动拷贝项目文件

![image](assets/image-20250911141604-xsw8068.png)

# 工会系统

![image](assets/image-20250915095917-e6rap8g.png)

## 数据库

![image](assets/image-20250915100108-p86ys1t.png)

## 流程

### 1、服务器启动时

服务器启动时加载所有公会到公会管理器

### 2、角色进入时

- 角色进入时创建Character，根据角色的GuildId从GuildManager获取公会到字段，如果公会信息不为空则后处理返回角色的公会信息。
- 客户端的Guild初始信息从GuildService获得，消息由GameEnterResponse捎回，由GuildService处理

### 3、点击公会时（包括权限管理）

- 用若已经加入公会则用户的Guild信息不为空，打开公会面板，否则打开弹窗
- 根据用户的职位激活对应的按钮组

```c++
panelAdmin.SetActive(GuildManager.Instance.myMemberInfo.Title > GuildTitle.None);
panelLeader.SetActive(GuildManager.Instance.myMemberInfo.Title == GuildTitle.President);
```

# 聊天系统

![image](assets/image-20251004171434-3qddhum.png)

## 自定义HyperText

```c++
public class HyperText : TextMeshProUGUI, IPointerClickHandler
{

    [Serializable]
    public class LinkInfo
    {
        public string Name;
        public LinkInfo(TMP_LinkInfo linkInfo)
        {
            Name = linkInfo.GetLinkID();
        }
    }

    public UnityEvent<HyperText, LinkInfo> onLinkClicked;

    public void OnPointerClick(PointerEventData eventData)
    {
        // 检查点击的区域是否是文本链接
        int linkIndex = TMP_TextUtilities.FindIntersectingLink(this, Input.mousePosition, null);
        if (linkIndex != -1)
        {
            TMP_LinkInfo linkInfo = textInfo.linkInfo[linkIndex];
            LinkInfo info = new LinkInfo(linkInfo);
            onLinkClicked?.Invoke(this, info);
           
        }
        
    }
}
```

```c++
using UnityEditor;

[CustomEditor(typeof(HyperText))]
public class HyperTextEditor : Editor
{
   
}
```

## 点击任意地方隐藏

最外层使用组件

![image](assets/image-20251004185708-zgahcuz.png)

节点层次，panel是root

![image](assets/image-20251004190358-pf393au.png)

实现接口IDeselectHandler

```c++
public void OnDeselect(BaseEventData eventData)
    {
        var ed = eventData as PointerEventData;
        if (ed.hovered.Contains(gameObject)) // 如果点击的不是根节点就关闭
        {
            return;
        }
        Close(WindowResult.None);
    }
```

窗口打开时要选中，这样才能正确触发不选中的回调

```c++
public void OnEnable()
    {
        GetComponent<Selectable>().Select();
    }
```

## 自适应界面

horizontal layout group + layoutelement

主要是通过flexiblewidth控制的比例

![image](assets/image-20251005200828-togjggh.png)

![image](assets/image-20251005200819-ixv43e4.png)

target显示时

![image](assets/image-20251005200836-0v2pfuu.png)

target隐藏时

![image](assets/image-20251005201433-xnbgkbx.png)

![image](assets/image-20251005201157-ogvr6jh.png)

## 组成

![image](assets/image-20251008143631-3za5d30.png)

## 任意频道组合

- 利用二进制位，比如所有+本地就是 0000011 也就是3
- int的-1的二进制码是全1 （补码存储）

![image](assets/image-20251008144152-gdm7tp3.png)

## Bug修复Local消息

### 服务端

在地图传送发生时，要重置Chat状态，防止上一个地图的聊天消息索引错误的继承到当前地图，例如：

地图A的idx是4，消息数量是5，此时切换到地图B，由于idx未重置仍然为4，假如在地图B只有1条消息，然而idx是4，result收集的结果就为空，直到在地图B发的消息达到5条，此时才会进入循环，返回第五条消息，中间就丢失了4条消息。

![image](assets/image-20251009132110-2twzj8b.png)

![image](assets/image-20251009131635-em2xfh7.png)

### 客户端

客户端需要在进入地图时候重置Manager状态

![image](assets/image-20251009132521-vm42tu7.png)

# 坐骑系统

沿用了移动同步

## 组成

![image](assets/image-20251009151558-47637pt.png)

## 协议

新增坐骑事件

![image](assets/image-20251009184714-7eyplzx.png)

## 局部空间转到世界空间

```c++
// offset是相对于mountPoint的偏移量，要考虑旋转
rider.SetRidePosition(mountPoint.position + mountPoint.TransformDirection(offset));
```

## 骑乘点

坐骑生成在角色下面

![image](assets/image-20251012211603-7z8gl37.png)

坐骑定义了骑乘点position，骑乘点加上角色位置相对于角色骑乘点骨骼的偏移量向量就是最终的骑乘位置

```c++
public void SetRidePosition(Vector3 position)
    {
        anim.transform.position = position + (anim.transform.position - rideBone.position);
    }
```

## 动画分层

同步

![image](assets/image-20251012212119-6poznm5.png)

同样的Idle，在不同的层绑定不同的Idle

![image](assets/image-20251012212241-a0iirjd.png)

![image](assets/image-20251012212250-lzldrle.png)

# 音效系统

![image](assets/image-20251013173929-cvan26z.png)

## 分类

![image](assets/image-20251013181521-d95oh9g.png)

## Unity原生系统

![image](assets/image-20251013181825-ef2mmmb.png)

## SoundManager

![image](assets/image-20251013182109-39c6vik.png)

## 混音器

![image](assets/image-20251013201537-97g8c3r.png)

### 暴露参数以进行代码控制

暴露混音器参数

![image](assets/image-20251013201152-fh253fw.png)

自定义名称

![image](assets/image-20251013201316-f6r9p8d.png)

# 寻路系统

![image](assets/image-20251017180551-sohfld0.png)

![image](assets/image-20251018144425-jja1ttc.png)

## 客户端寻路，服务端只做校验

## npc位置

### NpcManager统计npc的位置

```c++
Dictionary<int, Vector3> npcPosition = new Dictionary<int, Vector3>();
```

### Npc控制器初始化时更新位置

![image](assets/image-20251030212030-mgihijm.png)

## 服务端如何校验

将navmesh的数据转换成三维索引，发送同步消息时，服务端检查xyz对应是0还是1

### 1、处理点阵，输出配置信息

将x-y-z作为ID，体素化

```c++
 [MenuItem("Map Tools/Generate NavData")]
    public static void GenerateNavData()
    {
        Material red = new Material(Shader.Find("Particles/Standard Unlit"));
        red.color = Color.green ;
        red.SetColor("_Albedo", Color.red);
        red.enableInstancing = true;
        GameObject go = GameObject.Find("MiniMapBoundingBox");
        if (go != null)
        {
            GameObject root = new GameObject("Root");
            BoxCollider bound = go.GetComponent<BoxCollider>();
            float step = 1f;
            for (float x = bound.bounds.min.x; x < bound.bounds.max.x; x+= step)
            {
                for (float z = bound.bounds.min.y; z < bound.bounds.max.z; z += step)
                {
                    for (float y = bound.bounds.max.y; y < bound.bounds.max.y + 5f; y+=step)
                    {
                        var pos = new Vector3((int)x,(int)y,(int)z);
                        NavMeshHit hit;
                        if (NavMesh.SamplePosition(pos, out hit, 0.5f, NavMesh.AllAreas))
                        {
                            if (hit.hit)
                            {
                                string key = ((int)pos.x).ToString() +"-"+ ((int)pos.y).ToString() + "-" + ((int)pos.z).ToString();
                                DataManager.Instance.MapValidCheckPoints.Add(key, new MapValidCheckDefine()
                                {
                                    ID = key,
                                    X = (int)pos.x,
                                    Y = (int)pos.y,
                                    Z = (int)pos.z,
                                }) ;
                                var box = GameObject.CreatePrimitive(PrimitiveType.Cube);
                                box.name = "Hit" + hit.mask;
                                box.GetComponent<MeshRenderer>().sharedMaterial = red;
                                box.transform.SetParent(root.transform, true);
                                box.transform.position = pos;
                                box.transform.localScale = Vector3.one * 0.9f;
                            }
                        }
                    }
                }
            }
        }
        DataManager.Instance.SaveMapValidCheckPoints();
        EditorUtility.DisplayDialog("提示", "占位点导出完成", "确定");
    }
```

### 2、服务端读入

```c++
json = File.ReadAllText(this.DataPath + "MapValidCheckPoints.txt");
this.MapValidCheckPoints = JsonConvert.DeserializeObject<Dictionary<string, MapValidCheckDefine>>(json);
```

### 3、校验

```c++
if ((GameObjectTool.WorldToLogic(this.rb.transform.position) - this.character.position).magnitude > 50) // cm
{
	// this.character.SetPosition(GameObjectTool.WorldToLogic(this.rb.transform.position));
	// this.SendEntityEvent(EntityEvent.None);
	// 以服务器为准
	rb.transform.position =  GameObjectTool.LogicToWorld(character.position);
}
```

```c++
// 校验位置合法性
string key = ((int)(entity.Entity.Position.X / 100 + 0.5)).ToString() + "-" + ((int)(entity.Entity.Position.Z / 100 + 0.5)).ToString() + "-" + ((int)(entity.Entity.Position.Y / 100+ 0.5) ).ToString();
bool isValid = DataManager.Instance.MapValidCheckPoints[ID].ContainsKey(key);

Log.InfoFormat("Sysnc Pos:{0}, isValid:{1}", key, isValid);
```

### 4、非法处理

#### 客户端

客户端会收到error的同步消息

![image](assets/image-20251102181928-3aehvpz.png)

在实体层直接重置位置为网络位置，这样只要收到网络矫正信息，就能够及时纠正

```c++
void FixPosition()
    {
        this.position = GameObjectTool.LogicToWorld(entity.position);
        this.rb.transform.position = position;
    }
```

#### 服务端

服务端先将位置矫正，在进行广播，同时给请求者发送一个错误消息

```c++
public void UpdateEntity(NEntitySync entity)
        {
            // 校验位置合法性
            string key = ((int)(entity.Entity.Position.X / 100 +0.5)).ToString() + "-" + ((int)(entity.Entity.Position.Z / 100 + 0.5)).ToString() + "-" + ((int)(entity.Entity.Position.Y / 100 + 0.5)).ToString();
            bool isValid = DataManager.Instance.MapValidCheckPoints[ID].ContainsKey(key);
            Log.InfoFormat("Sysnc Pos:{0}, isValid:{1}", key, isValid);
            // 位置矫正
            foreach (var kv in MapCharacters)
            {
                if (kv.Value.character.entityId == entity.Id) // 找到自己
                {
                    if (!isValid)  // 如果非法
                    {
                        // NVector3 newpos = new NVector3() { X = 4700, Y = 3000, Z = 800 };
                        // 更新到上一次有效的位置，消息同步到自己
                        entity.Entity.Position = kv.Value.character.LastPosition;
                        entity.Event = EntityEvent.Error;
                        MapService.Instance.SendEntityUpdate(kv.Value.connection, entity);
                    }
                    else // 更新有效的位置
                    {
                        kv.Value.character.LastPosition = entity.Entity.Position;
                    }
                }
            }

            // 广播给其他用户，并更新服务端存储的位置信息
            foreach (var kv in MapCharacters)
            {
                if (kv.Value.character.entityId == entity.Id)
                {
                    kv.Value.character.Position = entity.Entity.Position;
                    kv.Value.character.Direction = entity.Entity.Direction;
                    kv.Value.character.Speed = entity.Entity.Speed;
                    if (entity.Event == EntityEvent.Ride)
                    {
                        kv.Value.character.Ride = entity.Param;
                    }
                }
                else
                {
                    MapService.Instance.SendEntityUpdate(kv.Value.connection,entity);
                }    
            }

        }
```

### 补充：点的结构

```c++
namespace Common.Data
{
    public class MapValidCheckDefine
    {
        public string ID { get; set; }
        public int MapID { get; set; }
        public int X { get; set; }
        public int Y { get; set; }
        public int Z { get; set; }
    }
}

```

‍
