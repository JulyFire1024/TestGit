ISelectHandler接口

一个物体上可以绑定Selectable脚本，这样子同样绑定在该物体上的mono脚本就可以继承一个该接口，实现该接口可以做到和按键相同的效果，在点击时触发实现的接口的方法


-----
IPointerClickHandler接口

指针点击处理器，一个物体上可以绑定Selectable脚本，


-----
Content Size Fiter

Vertical Layout Group

二者配合使用

一个UI自适应的组件，例如在一个Text组件上绑定该组件，并且设定其横向和纵向是预制还是自适应，就可以在Text中文本内容变化时，同属于一个父物体的其他UI子物体将自动下移让出位置

要实现效果必须要父物体也同时具备两个组件才可

但是不支持多级嵌套，在上一级已有该组件时使用时会有警告，最显著的问题是当Text内容变少后，他不会自动收缩回原来的位置，当内容的大小改变布局时，必须再有一次内容改变，才会有自适应的变化，所以给该Text赋值时，最好两次赋值，后面再追加一个空格


-----
- [ ] Ienumerator
- [ ] Ienumerable
- [ ] C#notifiers
- [ ] INotify类


