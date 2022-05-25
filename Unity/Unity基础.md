界面基础

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110002178.png)


![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110002437.png)


![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003928.png)

按住V找到A上的某一个小方块拖动到B上的某一个小方块，就可以实现两者吸附




-----
不一定每一个脚本都是组件

只有继承自MonoBehaviour类的才是组件

C#脚本组件里的public类可以在unity界面直接进行编辑

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003377.png)


-----
Transfrom的基本属性和方法

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003965.png)


eulerAngles 直接对应编辑器页面的Transform的Rotation

rotation虽然可以完成同样的操作，但不对应





![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003339.png)

等价于

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003931.png)


-----
GameObjcet的基本属性和方法

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003366.png)

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003300.png)



  二者已有其一可获取另一

    gameObject.transform
    
    transform.gameObjectri




![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003988.png)

eg: private SpriteRenderer spriteRenderer;

  spriteRenderer = GetComponent<SpriteRenderer>();



-----
预制体


![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003745.png)


![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003208.png)


![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003141.png)

也就是说，

关于套娃，当A预制体中包含B预制体时，对B预制体再单独改动，不会影响到A预制体（包括异世界以及场景中所有实例）

关于变体，如果B预制体是A的变体，若对B预制体改动，不会影响到A，但若对A预制体改动，则==会影响到A==


-----
生命周期函数

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003249.png)


-----
Invoke

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003179.png)


-----
协程

非多线程，“协同程序”，

在主程序（生命周期函数）进行时，“同时”运行其他逻辑

协程以一个函数的形式出现

以yield return返回。 并且协程的返回不影响后续程序的继续运行。

public Ienumerator Demo（）

{

yield return new WaitForSeconds(0.01f); //等待

yield return Demo2(); //可以返回另一个协程

}

协程的使用,

  StartCoroutine(string method Name)


协程的停止，

  StopAllCoroutines()，停止所有协程

  StopCoroutines()，停止某个协程

    可以是StopCoroutine(string method Name) //但不要这样用，因为实际中可能



会有很多同名协程一起使用

  ==应当在使用时 Corutine cor = StartCoroutine(协程名(参数));==

  ==停止时 StopCoroutine(cor) ，可以做到对应启动对应停止==



-----
常用的工具

数学工具

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003544.png)



时间工具

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003124.png)

deltaTime可以用来在不同帧数时统一每一秒的操作

方向\*速度\*帧时间

  private void Update（）

  {

  transform.Translate(==new Vector3(0,1f,0) *1*Time.deltaTime==);

  }

  /\*因为updata是每帧执行一次，而delatTime是帧与帧之间的时间间隔，

  这样子就可以做到无论帧数是多少，都是每一秒y方向位移1m

  1s内总位移\= 位移次数（帧数）\*每帧位移

  每帧位移即 总位移 \* 帧与帧之间的间隔 \*/



-----
四舍六入五取偶


-----
输入系统

键盘输入

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003195.png)


鼠标输入

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003025.png)




注意鼠标坐标和开发时Scene无关，是实际Game界面，以左下角为（0,0）,右上角为最大值点的一个坐标系中的值，如分辨率为1920\*1080,最右上角点j就为（1920，1080）



输入管理器InputManager

Edit-->ProjectSettings-->InputManager

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003411.png)



提供的W,A,S,,D方案

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003541.png)

  

一个基本的移动方案

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003225.png)

  Horizontal 获取A,D横向输入 Vertical获取W,S纵向输入



-----
渲染基础

摄像机

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003113.png)


灯光

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003875.png)



![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003376.png)

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003771.png)


Shader

  渲染管线

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003629.png)


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110003577.png)

  

![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004349.png)

Shader可以附加给材质，材质附加给网格化模型


粒子

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004199.png)



-----
Unity动画系统

模型的动作，一般只服务于视觉，在数据计算上仍然依赖碰撞体等

程序做的是如何配置动作，切换动作，代码控制动作


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004285.png)


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004874.png)

  


在Animator面板可以设置动画的衔接和切换

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004503.png)


关于状态面板

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004156.png)

  

脚本中控制动画

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004803.png)

  

人形动画

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004532.png)

  

动画事件

  可以在GameObject的 Animation面板的 中选择某一帧时间后，在Inspector 面板处选择添加动画事件，动画事件在绑定该Gameobject的脚本中的public函数定义

  对于已有的动画资源，可以Inspector面板中的Events选择添加事件

  

角色控制器组件

  Character Controller

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004582.png)


基于角色控制器的移动方案

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004263.png)

  使用方法与之前的Transformlate 和rigibody.moveposition一样



-----
Unity导航系统

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004601.png)



导航烘培

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004331.png)



NavMeshAgent 组件

导航代理

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004882.png)


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004478.png)

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004782.png)



Navigation 面板

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004242.png)

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004583.png)


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004862.png)


NavMeshObstacle属性

动态障碍物

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004552.png)




-----
Unity资源管理

预制体实例化

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004498.png)

    |**original**|要复制的现有对象。|
|------------|---------|
    |**position**|新对象的位置。|
    |**rotation**|新对象的方向。|
    |**parent**|将指定给新对象的父对象。|
    |**instantiateInWorldSpace**|分配父对象时，传递 true 可直接在世界空间中定位新对象。传递 false 可相对于其新父项来设置对象的位置。|



Resouce资源加载

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004162.png)


可以有多个同名的Resource文件夹，并且不一定要在Assets下一层，可以在更深的层次，不需要指定前缀路径，都可以查找的到


数据存档PlayPrefsr

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110004071.png)

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005106.png)




场景加载

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005353.png)

  ![](image_53.ebc0c22e.png)

  

声音系统

AudioListener组件，可以让玩家听到音效

  一般放在相机身上

  AudioSource组件

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005003.png)

    常用方法
    
    ![](image_55.c90db084.png)
    
    InPause ，接着播放，而不是从第一帧重新开始



