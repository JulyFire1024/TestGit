**MMORPG**

2022年2月7日

19:50

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205102358393.png)


EF框架

[https://www.cnblogs.com/xuf22/articles/5513283.html](https://www.cnblogs.com/xuf22/articles/5513283.html)


数据库生成DB

生成数据库中表的文件

Entities.edmx 用来自动生成SQL语句

右键 新建实体 然后增加属性字段

右键 ->根据模型生成数据库

将SQL脚本放到数据库中执行即可


Protobuf 协议

[https://www.cnblogs.com/zhangguicheng/p/14117962.html](https://www.cnblogs.com/zhangguicheng/p/14117962.html)

[https://zhuanlan.zhihu.com/p/141415216](https://zhuanlan.zhihu.com/p/141415216)

[https://www.cnblogs.com/xiangxiaolin/p/12712720.html#:~:text=Protobuf,%E7%9A%84%E6%B6%88%E6%81%AF%E5%AE%9A%E4%B9%89%E6%96%87%E4%BB%B6%E3%80%82](https://www.cnblogs.com/xiangxiaolin/p/12712720.html#:~:text=Protobuf,%E7%9A%84%E6%B6%88%E6%81%AF%E5%AE%9A%E4%B9%89%E6%96%87%E4%BB%B6%E3%80%82)


协议更改与自动生成

在Src\\Lib\\Proto\\message.proto 中可以更改通信协议 消息发送和响应的字段

要注意如果是新增了一条message，要在最上面的NetMessageRequest和NetMessageResponse中加入新加的消息，才可以在现有的框架下使用。

生成协议后别忘了在消息分发器中新加消息分发否则收不到消息。

然后在Tools/genproto.cmd ,点击即可自动生成更改C#代码 即Src\\Lib\\Protocol\\message.cs

然后服务端，选中GameServer解决方案，全部重新生成一次

然后在Src\\Lib\\Protocol\\bin\\Debug文件夹中的

( protobuf-net.dll 、protobuf-net.xml、Protocol.dll三个文件，这个好像搞错了),

复制Common.dll,conmon.pdb(这是修改conmon代码后的)

Protocol.dll,protocol.pdb(修改协议后的)

  要复制到Src\\Client\\Assets\\References目录下并替换原先的三个，

    即服务端自动生成， 客户端需要自己手工替换




Netclient.cs

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205102359221.png)


网络编程

网络编程中有两种模式：阻塞和非阻塞，默认是采用阻塞方式。

什么是阻塞和非阻塞：

阻塞和非阻塞是对操作请求者在等待返回结果时的状态描述，阻塞时，在操作请求结果返回前，当前线程会被挂起，得到结果之后返回；非阻塞时，如果不能立刻得到结果，系统不会挂起当前线程，而是直接返回错误信息，因此对应非阻塞的情况，调用者需要定时轮询查看处理状态。

本质：阻塞和非阻塞本质上是本地系统对socket的不同处理方式，并不影响socket链接，也不会影响通信对方，通信双方可以自由选择阻塞还是非阻塞，例如：客户端设置成阻塞，服务器端accept 后可以设置成非阻塞都是可以的。


非阻塞是阻塞方式的改进方案，在大部分情况下可以获得更好的性能。

阻塞模式下什么情况下会阻塞：

不管是TCP还是UDP，accept，connect，send，recv等操作都可以分类为发送数据和接收数据，connect和accept本质上也是发送和接收数据。

  对于接收数据，当然需要对方有发送数据，自己能接收到数据，不然就会阻塞。


对于发送数据，数据的发送是由系统管理的，应用层操作只是将数据写入内存缓冲区，因此大部分情况下是不阻塞的，只有当缓冲区满，才会阻塞，（缓冲区不足以保存当前请求发送的数据，不确定是否会阻塞，还是只拷贝内存空闲大小数据）。

阻塞可能导致的问题：

阻塞会导致线程挂起，如果是单线程处理，其它操作会被中断，得不到响应。

一直阻塞会导致程序无法使用，例如：如果对端未发送数据，接收端会一直阻塞在recv函数，导致接收端也无法发送数据了，除非使用多线程处理。



**客户端发送消息到服务器的流程：**

  一、在客户端的 某个物体上挂脚本

    要连接到服务端，
    
    IP端口先初始化
    
    ![](image_3.2bc486e9.png)
    
    注意该场景中必须有一物体已经挂载NetClient组件


  二、添加消息并生成协议

​    

  五、客户端代码

    仍然是某个物体上挂载的脚本
    
    ![](image_4.ded2da3a.png)
    
    某条消息msg是一个消息组，都要通过NetMessage来发送
    
    这条消息可以是请求也可以是回应 （Request Response）
    
    然后将其FirstTest这个可选内容组中的Helloworld这一个string类型赋值
    
    然后单例Instance的方法SendMessage来发送消息


  六、服务端代码

  首先要在GameServer项目中的Services文件下新建一个类，假设命名为HelloWorldService

  包含Init、Start 、 Stop方法

    ![](image_5.e21ba79a.png)


  特别要注意要使用Network 和 SkillBridge.Message两个命名空间

    然后在GameServer.cs中的Init和Start中调用该单例的Init和Start方法
    
      ![](image_6.b8a37941.png)


​      



七、消息分发

在Src\\Lib\\Common\\Network下的 MessageDispatch.cs 消息分发器，要增加新的发送的消息

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205102359101.png)

  注意是Request而不是Response




**UI制作**

- 九宫格，当资源与使用场景大小不匹配时，中间格向四周拉伸，上中下中左中右中分别向上下左右拉伸，四个角的格子不变。选中sprite在sprite editor里编辑

制作loding场景时，28分左右讲到

- Unity可以自制字体，实现用文本的方式来表现图片， 使用字符图片自定义字体

[https://blog.csdn.net/qq\_28849871/article/details/77719054](https://blog.csdn.net/qq_28849871/article/details/77719054)



**用户系统的框架架构**

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000748.png)


**数据的更改和json的生成**

数据存放在Src/Data/Tables中的Excel表里，可以对其进行修改

修改完成后可以 运行 Excel2Json.cmd，自动生成.txt后缀的json格式的文件

之后要将Data文件夹下生成的.txt后缀的文件夹复制到客户端Client/Data目录下覆盖掉（工具已经自动有了这个功能）



*可以在材质界面选择渲染模式以表现出不同的效果*


**如何在UI层显示3D角色**

  角色创建与选择(1)的32:31

  RenderTextures技术

    场景中新建一个UI的Raw Image
    
    在文件中 新建一个Render Texture，
    
    场景中新建一个摄像机，对准想要显示的空间
    
    将该Render Texture同时赋给Raw Image和摄像机，即可实现将摄像机所对准的3D空间展示到2D的RawImage区域的UI层上
    
    Render Texture 可以调节分辨率Size ，数值越高角色越清楚


​    
​    




**重要的Session ，**

在角色登录时用到

可以登陆成功时设置Session的User Chareracter等属性

客户端和服务端交互的媒介， 可以存储当前的用户 ，可以1用于服务端标记 是哪个客户端发来的消息


注意对象之间的关系

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000749.png)



实体

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000751.png)

  每个实体都有一些共同的属性，比如地图位置，速度,ID等等 ，抽象出来写到父类Entity中

  可见或不可见的逻辑实体对象为实体，如一个NPC一个技能中的火球一个怪物等等

  CharacterBase是所有角色的父类， Character是自己的或者别的玩家的角色



**进入主城与离开主城**

1、流程

进入游戏：

- 首先客户端通信部分，告诉服务器该角色要进入游戏
  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000752.png)

    

- 然后到服务端，先在UserService中 ，消息分发器分发到GameEnter
  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000753.png)

  

- 然后是服务端的处理
  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205102359000.png)


- Modle/Map.cs的处理

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000754.png)

  

- 客户端结构：
  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205102359167.png)



要注意 角色进入和离开主城，都是在客户端的MapService中做的响应，包括实例化角色存入地图角色清单等等

而UserService中的角色进入离开只负责本地的场景切换和读取用户、角色信息等逻辑


**小地图**

- 实时渲染场景
  - 风格比较写实，性能损耗比较大，直接在俯视角加一个摄像机

- 预渲染顶视图加润色
  - 将地图俯视图提前渲染到一张图片中，然后进行美术加工，增加一些属性

- 纯美术制作
  - 精确度不算高。



更改配置的流程

  同样的这里要从Resouces目录下读取资源，以及从数据目录下读取资源，因此也需要像之前提到的数据修改生成一样的操作



  同时由于在表中新加了字段，要在Src/lib/Common/MapDefine下新加项，并且编译一下。



  同时将

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000755.png)

  这些文件复制到Src/Client/Assets/References目录下覆盖

  （其实就是更改完Common/Data目录下之后，他会把更改放到Common.dll上,需要重新赋值）



**实现思路：**

建立一个和地图场景一样大的cube作为映射，然后计算角色在这个cube的相对坐标(x y 坐标均是0~1范围内)，然后将同样是0~1范围的小地图的中心点privot设为该值，这时候transform会发生改变，将其置为0即可实现小地图跟随角色。


**移动同步**


[https://blog.csdn.net/weixin\_43679037/article/details/122848197](https://blog.csdn.net/weixin_43679037/article/details/122848197)

类别：

- 状态同步 MMORPG
- 帧同步 RTS游戏，MOBA游戏
  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000756.png)





帧同步断线重连要从游戏开始第一帧之后的所有消息都重新发送一遍，来达到重连的效果

并且帧同步一个小数点的误差都不能有，只要错一帧，之后的所有游戏时间都错误了，对于数值精度有很高的要求

但状态同步却随时可以再次加入


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000757.png)

  

关于重构entityId

弃用characterId改用entityId,否则又有角色又有怪物之后就不严谨了

服务端在EntityManager中 将列表索引作为Entity的Id，每生成一个实体就将赋给它一个Id，并且在客户端和服务端通用



  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000758.png)




同步的目标对象

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205102359963.png)



同步流程

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000759.png)

  在InputController中接收到玩家的输入信息后，首先对当前客户端的自己控制的角色的位置，方向，速度进行改变，然后根据操作通过Entity Controller来控制一些动画等等（entityController.OnEntityEvent），然后InputController在收到输入后直接调用客户端MapService发送消息（在SendEntityEvent方法中的SendMapEntitySync）


  服务端的MapService收到消息（MapEntitySyncRequest）后根据消息发送方的当前地图Id，通过MapManager找到对应的Maps字典中的 Modle.Map Class执行 UpdateEntity方法，该方法循环检测该地图的角色字典中所有角色，如果是发送消息的角色，就更新其在服务器存储的Entity数据，Pos，Dir，Speed，如果是循环到别的角色，就向他们发送一条消息告知（SendEntityUpdate），某唯一ID的实体的移动信息已经发生改变，变为了什么什么。


  消息中有一个entitySyncs List，循环该List，每一个都调用EntityManager的OnEntitySync方法



**地图传送**

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000760.png)


扩展编辑器，增加一个菜单项，直接生成传送点

要先在根目录下创建一个Editor目录，在里面放置脚本


**UI框架设计**


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000653.png)



  可扩展性，将结构定好，易于扩展，则在前期不需要特别惊喜。

    ![](image_24.0c18803f.png)







**NPC系统**

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000761.png)



  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000762.png)




**新增一个表的步骤：**

- 首先在Src/Data/Table目录下新建excel表并写入想要的东西，这是所有配置表的基础
- 然后在Lib/Common/Data 下新建对应的cs文件，仿照定义属性
- 然后在客户端和服务端的DataManager分别在开头字典和Load方法中引用表
- 记住客户端修改完成后，要重新生成解决方案，在Lib/Common/bin/Debug下的Common(两个文件)复制到Client/Assets/References
- 然后要运行Src/Data下的excel转json工具，并将Data目录下生成的txt分别复制到服务端和客户端



NPC要可交互，可点击：

  MonoBehaviour 的message中的很多都很有用

  例如这里用到的OnMouseDown ,PC和移动通用，只要玩家点击到有碰撞体的物体，就会自动调用该方法


NPC和其它系统要交互，在NPCManager里面通过事件监听的方式来完成


交互流程 ：

用户在点击NPC的身体之后，触发NPCController里面的 OnmouseDown函数

这时候该函数内部的 Interactive函数发挥作用，将角色的状态改为正在交互(一个bool变量）

并将交互具体协程 DoInteractive 启动

具体交互协程中调用了NPCManager中的Interactive函数，该函数将判断当前npc是任务npc还是交互npc

转到对应的行为函数DoTaskInteractive 和 DoFunctionalIteractive ，在DoFunctionalIteractive中利用找到字典中存储的传入npc信息的Function找到对应的委托，通过委托来使用方法


**道具系统**

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000029.png)



  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000763.png)



  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000764.png)




**背包系统**

  可以考虑的一种方案，将背包内存储的东西序列化为类似于json的字符串，但是这样需要频繁的转换解析，降低了性能，并且加大了存储的空间成本

  我们用的方案：用二进制数据，可以方便的存储到数据库，包括现实中很多头像啊这种图片资源也是化为二进制数据来存储。

    ![](image_30.3bf1906c.png)


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110001871.png)


  为了简化逻辑，服务端不关心背包到底是怎么样的，所有处理的逻辑都放到客户端，相当于一个单机背包，只需要把最终的布局整合成二进制数据流发送到服务端存到DB里面就可以。（BagSaveRequest）


  此外要在服务端和客户端Character 创建和进入的时候分别做对应的初始化

  客户端UserService的 OnGameEnter

  服务端UserService的 OnCreateCharacter 以及Character实体的构造函数


Moders.BagItem 用结构体，是值类型而不是引用类型，交换格子是值交换，所以不用类，省去装箱拆箱的GC


**商店系统**

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110001291.png)



  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000767.png)


序列图，画出了函数执行顺序和生命周期

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000768.png)


结果图

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000769.png)



一个物体上可以绑定Selectable脚本，这样子同样绑定在该物体上的mono脚本就可以继承一个ISelectHandler接口

就可以重写一个OnSelect方法，实现点击选择时的自定义的变化。不需要射线检测和按键了。


新加的状态系统，比如说购买东西，发送一个购买东西的消息

然后客户端要收到购买的反馈，还要收到身上的钱少了，还要收到增加了道具

来一个回三个，这样子就增加了服务器的压力，设计的不够好，因此要优化


具体实现是在协议中的STATUS\_ACTION，STATUS\_TYPE， NStatus ，StatusNotify 设计的非常精妙，将可能会改变的 分别枚举出了类型和变化行为 ，这样可以通过一条repeated关键字的消息，来达到一条消息中容纳多个变化的目的


同时对服务端的NetConnection 和Netsession做了优化

Netsession是从收到消息开始到给客户端发一条消息结束是全程存在的并且是唯一的，所以比如说客户端发来一条消息涉及到多个Manager和Service的变化，就可以在各处都对Netsession进行操作，但只在一处发送，这样就实现了一条消息可以承载多处的信息，不用分多条发送

在一个会话周期而不是方法周期


为了配合这样的状态变更方法，可以将会修改的字段扩展为属性，在修改其值时自动更改角色管理器的状态，这样就不必在外部逻辑时关心角色管理器的状态有无变更


**装备系统**


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000770.png)



![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000771.png)

DB只需要在角色身上加一个4\*7=28字节的字段来代表穿着的装备即可


**任务系统**

  



  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000772.png)


  数据结构：

    ![](image_39.ab746df9.png)




  配表技巧：



一个小注意事项，Modle实体Quest中有两个信息：

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110000773.png)


整个过程只有在QuestManager里的RefreshQuestStatus方法中给 Info赋值，因此就不需要额外的信息来存储任务是接取还是提交，在整个流程中都可以使用Info为不为null来判断是要做什么，因此提交任务和接取任务很多方法都可以合二为一，只要加条件判断即可



58min在介绍UI怎么拼 ，以及1h9min 第二节的23.54

1h20min26s在介绍任务对话面板UI

自己改的地方 都注释了maybe error

QuestManager Client 的UnityAction OnQuestStatuschanged 还没有使用

