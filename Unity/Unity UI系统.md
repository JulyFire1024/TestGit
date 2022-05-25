[https://blog.csdn.net/q764424567/article/details/119992141](https://blog.csdn.net/q764424567/article/details/119992141)


-----
#Unity UI系统#

UI ,由Canvas以及各种UI组件组成

固定铺在一块分辨率大小的画布上，不随摄像机移动改变


  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005464.png)

  

### Image组件 ###

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005326.png)





### 脚本操作UI

==首先必须要引入UI的命名空间才可以在脚本中对UI进行操作==

`using unityEngine.UI`

之后就是老样子，引用组件，操作属性

###Panel组件

作为一个容器来 放置其他的UI组件

### Text组件

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005915.png)



  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/image_6.30ec9959.png)

###Button组件

UI中的按键，同时由Text和Image组成，

  <img src="image_7.709874b8.png" style="zoom: 67%;" />




  <img src="https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005538.png" style="zoom: 67%;" />

  

<img src="https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005634.png" style="zoom: 67%;" />



InputField组件

用于承载玩家的输入

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005748.png)

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005272.png)


事件

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005211.png)


    ![](image_13.5bb07fab.png)




Toggle组件

模拟控制开关的组件，主要使用的场景有，开关声音、开关灯光等。
在实际UI中多表现为==勾选==的形式，

  Toggle用法跟Button很相似，都是点击按钮响应事件

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005021.png)


同样可以在面板中hi'jia添加事件或者通过脚本添加事件

可以通过Toogle Group组件来实现单选的效果

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005421.png)



Slider组件

Slider是一个滑动条组件，一般用来制作血条或者进度条，或者调节亮度、音量等

Slider和Scrollbar的区别呢：

Slider更偏向于用来改变一个数值，比如说血条、进度条，或者改变声音的大小等。

Scrollbar则是改变目标比例的组件，是一个百分比0-100%，例如改变滚动视野的显示区域。

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110005819.png)

  仍然可以在面板中添加 事件 ， 在脚本中依旧是利用委托来调用




ScrollBar组件

ScrollBar 滚动条组件，是一个用来展示进度的组件，主要用于显示当前内容在全部内容下的比例或者位置在哪里。

主要用于形象的拖动以改变目标比例的控件，他的最恰当应用是用来改变一个整体值变为他的指定百分比例，最大值1（100%），最小值0（0%），拖动滑块可在此之间改变，例如改变滚动视野的显示区域。

Scrollbar 滚动条组件通常与ScrollView组件配合使用，用来显示内容。

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006524.png)


两边颜色一致，没有填充


ScrollView组件

滚动视图组件

组成的结构有：

  Viewport，它是可以显示的部分，内含一个coment ，所有的内容，以及一个遮罩组件（mask）

  一个ScrollbarHorizontal和一个ScrollbarVertical ，横向和纵向的滚动条



DropDown组件

下拉组件，可快速创建大量选择项

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006306.png)





Grid Layout Group组件

表格布局组件，类似于背包这种排列整齐的UI场景

不是直接create UI 里的选项，是新建一个物体之后将该 组件附加给它

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006739.png)


Horizontal Layout Group组件

横向的一排布局

Vertical Layout Group组件

纵向的一排布局


UI布局

Rect Transform属性：

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006163.png)

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006327.png)



Canvas画布

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006707.png)



  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006150.png)




  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006548.png)

  

UI事件

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006386.png)


事件接口

  ![](https://cdn.jsdelivr.net/gh/JulyFire1024/JulyFireMarkdownPictureBed/202205110006132.png)

