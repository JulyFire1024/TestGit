老师教Debug的地方

移动同步2 在24分之后讲解了不报错的问题的断点调试流程

逆向查找，在期待正常发生的行为往前追溯，寻找调用它的点，下断点调试，尤其是要注意if语句

移动同步3整个在教Debug

移动传送 58分之后在教扩展编辑器


-----

玩家之间的通讯互动 通过查找彼此的角色的ID来实现

因此用字典来存储角色 ，方便查找


客户端是以M为单位，服务端以cm为单位

用整型而不用浮点型，避免在大型的数据通信中的误差
CPU的位数的精度问题导致浮点数的计算的误差问题

浮点有效精度只有六到七位

避免动画和刚体碰撞的冲突，在 预制体上创建一个父节点，子节点上绑定动画组件，而移动等等脚本绑定到父节点上


世界坐标的UI，

例如角色血条和名字显示在世界坐标下，可以给他两个脚本，一个是UIWorldElement，表示是世界UI的一个实体，一个是UINameBar，来控制它的独有的属性



游戏对象在切换场景时会销毁，为了使得他不销毁，需要有一个单例， 单例是默认有一个bool global(自己改过的那个)

单例类不能写Start，不然还是会销毁，必须使用一个 protected override void onStart 方法


弃用characterId改用entityId,否则又有角色又有怪物之后就不严谨了


EnityId 和EnityData.Id 是一致的

EnityId是标识唯一性的一个Id

现在character.Id是EntityId, character.info.Id是数据库中的DbId



C#notifiers

INotify类


在组件相互调用时，因为不能确定谁会被先销毁，所以在第一句先检测为不为空，为空就return




协议都在Src/Lib/Proto里


字典中TryGetValue 比 ContainsKey+GetValue要节省一倍的性能消耗


Mono单例放到只加载一次的场景中是没有问题的，但是如果一个场景被多次加载，则该场景中的Mono单例会重复生成好几份


如何实现对话的时候NPC转向，用到了normalized，归一化向量，返回一个单位长度为一的方向向量，具体看NPCController里面的FaceToPlayer的代码

Vector3.Lerp，插值函数


关于如何操作数据库，在Server端的ItemManager中AddItem方法中有示例

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/image_1.afda90e0.png)



除了用户注册这种，不会大规模的集中发送的需要数据库实时保存的，可以让数据库每次更改都立即保存，

其他的诸如用户升级了，捡到个道具啊诸如此类的东西，如果没更改一次就让数据库实时保存，那压力特别大可能会经常宕机。

因此一般都是先将数据临时存到服务端，待累计一定时间或者规模之后再进行数据库的保存更改，这也是很多时候意外发生会回档的原因。


Mono脚本，第一时间先执行Awake，第二执行OnEnable，第三时间才执行Start，并且Start的执行顺序不是十分严格的



==一个物体上可以绑定Selectable脚本，这样子同样绑定在该物体上的mono脚本就可以继承一个ISelectHandler接口==

就可以重写一个OnSelect方法，实现点击选择时的自定义的变化。不需要射线检测和按键了。

涉及到系统和系统，逻辑和逻辑之间的调用，还是要走Manager，不能和UI有强的相关联


新加的状态系统，比如说购买东西，发送一个购买东西的消息

然后客户端要收到购买的反馈，还要收到身上的钱少了，还要收到增加了道具

来一个回三个，这样子就增加了服务器的压力，设计的不够好，因此要


DBService.Instance.Entities.CharacterQuests.Create();

创建一个实例，但并不将该实例添加到实体集中

