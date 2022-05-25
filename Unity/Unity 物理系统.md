Unity2D

  首先，相机Camera 的Projection设置为Orthographic ,正交模式，忽略距离


Sprite组件

  Sprite，一种在2D游戏中表示角色、场景的图片资源

  SpriteSheet，切割一个图片为多个Sprite，就是SpriteSheet

  通过更改资源的Inspector中的Sprite Mode改为 Multiple 可以在Sprite Editor通过组件进行切割



  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110002794.png)



  在脚本中修改sprite的各种属性：

    ![](image_2.727a1047.png)




物理系统

可以在Edit—\>ProjectSettings 中的Physics 2D中修改诸如重力等一系列物理系统参数

  刚体：

  给gameobject增加RigidBody（2D）组件，使其具备刚体属性，可以运动

    ![](image_3.c5d3ea42.png)
    
      该组件中的Material，物理材质，也是一种资源，
    
        具有Friction（摩擦力），Bounciness（弹力）两种属性



    常用的API:
    
    - MovePosition ，向坐标移动
  - velocity ，改变力，
- AddForce ，施加力

  
    碰撞体：

    给gameobject增加（Box/…）Collider（2D）组件，使其具备碰撞体属性，作为一个游戏物体的物理边缘，用来防止穿模、碰撞检测

      Edit Collider 可以在Scene面板中编辑碰撞体尺寸

      - Offset，偏移量
    - Size ，碰撞体尺寸
  - Material，物理材质


    碰撞检测：
    
      ![](image_4.ea99cafa.png)





1) ==双方都不是碰撞体和刚体，不会触发碰撞事件==
2) ==双方都有碰撞体和刚体，可以触发==
3) ==一方有刚体和碰撞体，另外一方只有碰撞体，双方均可以触发碰撞事件==
4) ==双方都没有刚体。无法触发==


-----
Unity3D

可以在Edit—\>ProjectSettings 中的Physics 中修改诸如重力等一系列物理系统参数

刚体：

  给gameobject增加RigidBody组件，使其具备刚体属性，可以运动

    |**参 数**|**含义**|**功 能**|
|-------|------|-------|
    |Mass|质量|物体的质量（任意单位）。建议一个物体的质量不要与其他物体 相差100倍|
    |Drag|阻力|当受力移动时物体受到的空气阻力。0表示没有空气阻力，极 大时使物体立即停止运动|
    |Angular Drag|角阻力|当受扭力旋转时物体受到的空气阻力。0表示没有空气阻力， 极大时使物体立即停止旋转|
    |Use Gravity|使用重力|该物体是否受重力影响，若激活，则物体受重力影响|
    |Is Kinematic|是否是运动学|游戏对象是否遵循运动学物理定律，若激活，该物体不再受物理 引擎驱动，而只能通过变换来操作。适用于模拟运动的平台或 者模拟由铰链关节连接的刚体|
    |Interpolate|插值|物体运动插值模式。当发现刚体运动时抖动，可以尝试下面的 选项：None(无），不应用插值；Interpolate(内插值），基于上一巾贞 变换来平滑本帧变换；Extrapolate(外插值），基于下一帧变换来 平滑本帧变换|
    |Collision Detection|碰撞检测|碰撞检测模式。用于避免高速物体穿过其他物体却未触发碰 撞。碰撞模式包括Discrete (不连续）、Continuous (连续）、 Continuous Dynamic (动态连续〉3种。其中，Discrete模式用来 检测与场景中其他碰撞器或其他物体的碰撞；Continuous模式 用来检测与动态碰撞器（刚体）的碰撞；Continuous Dynamic模 式用来检测与连续模式和连续动态模式的物体的碰撞，适用于 高速物体|
    |Constraints|约束|对刚体运动的约束。其中，Freeze Position(冻结位置）表7TC刚体 在世界中沿所选HZ轴的移动将无效，Freeze Rotation(冻结 旋转）表示刚体在世界中沿所选的X、Y、Z轴的旋转将无效|


​    


碰撞体：

  给gameobject增加（Box/…）Collider组件，使其具备碰撞体属性，作为一个游戏物体的物理边缘，用来防止穿模、碰撞检测

​    


碰撞检测：

  同2D

​    


触发：

  类似2D

​    



射线：

用于判断射击是否命中、点击地面建造建筑物等功能

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110002898.png)




  **RaycastHit**`类用于存储发射射线后产生的碰撞信息。常用的成员变量如下：`

  - `collider与射线发生碰撞的碰撞器`
- `distance 从射线起点到射线与碰撞器的交点的距离`
- `normal 射线射入平面的法向量`
- `point 射线与碰撞器交点的坐标（Vect` `or3对象）`




**屏幕的鼠标射线**

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110002005.png)


Raycast是可以重载的，前两个参数合二为一，一个Ray型参数传入





刚体移动：

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110002240.png)



-----

