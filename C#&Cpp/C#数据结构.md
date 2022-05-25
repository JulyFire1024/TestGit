数组

int \[ \] array1 = new int \[3\] {1,2,3};

int \[ \] array2 = {1,2,3 ,4 ,5 };

int \[ \] array3 ; array3 = new int \[2\] ; array3\[0\] = 5 ; array3\[1\]=2;

Length属性 , for循环遍历


-----
动态数组

ArrayList

- 对象的有序集合，

动态数组会自动重新调整它的大小

可以使用索引在指定的位置添加或移除项目，它也允许在列表中进行动态内存分配

本质上存储的是Object类，将存储的内容转换

ArrayList arraylist1 = new ArrayList();

- 方法
  - Add ， 添加新的元素
  - AddRange ， 直接添加数组等
  - Contains， 是否包含于
  - IndexOf, 查询元素的索引
  - Insert , 指定位置插入元素
  - Remove 删除指定的元素
  - Reverse , 反转数组中元素顺序
  - Sort, 对数组进行排序


-----
List

- 泛型容器 List< >，

作用与功能近似arrayList

无需装箱拆箱和类型转换

类型安全

List<int> list1 = new List<int>();

需要提前指定存储元素的数据类型

- 方法
  - Count , 长度
  - Add ， 添加新的元素
  - AddRange ， 直接添加数组等
  - Contains， 是否包含于
  - IndexOf, 查询元素的索引
  - Insert , 指定位置插入元素
  - Remove 删除指定的元素
  - Reverse , 反转数组中元素顺序
  - Sort, 对数组进行排序


-----
哈希table

Hashtable

- Hashtable类代表了 基于键的哈希代码组织起来的 键—值 对的集合

不安全的，存储为object类，

Hashtable ht1 = new Hashtable();

Key（键）、value（值）都可以是任意类型的，

- 方法
  - Add ， 添加新的元素
  - Contains，ContainsKey ，ContainsValue， 是否包含于
  - Clear
  - Remove

- 访问

ht1\[key\]

- 遍历

ICollection key = ht1.Keys 通过ICollection属性可以获得Hashtable的键值列表

foreach ( var k in key )


-----
字典

- 泛型容器 Dictionary< , >

作用与功能近似Hashtable

存储键—值 对数据的集合

但需要对key和value都指定固定类型

类型安全,无需装箱拆箱 类型转换，效率更高

Dictionary<int,string\> dic1 = new Dictionary<int,string> ( );

- 方法
  - Add ， 添加新的元素
  - Contains，ContainsKey ，ContainsValue， 是否包含于
  - Clear
  - Remove

- 访问

dic1\[key\]

- 遍历

用Hashtable那一种

或者 foreach ( KeyValuePair<int,string> kvp in dic1 )

kvp.Key 和kvp.Value 分别访问


-----
HashSet

- HashSet<>包含不重复元素的无序列表
- 泛型容器，需要提前指定存储的数据类型

HashSet<int> hs1 = new hs1<int> ( );

- 方法
  - Add ， 添加新的元素
  - IntersctWith , 取两个HashSet的交集
  - UnionWith ， 取两个HashSet的并集
  - ExceptWith ， 取两个HashSet的差集，去掉（）中HashSet的元素后所操作的HashSet所余元素
  - SymmetricExceptWith ，取两个HashSet的对称差集 ，二者相并再去掉共有元素


-----
链表

- 双向链表，LinkedList<\>
- 泛型容器，需要提前指定存储的数据类型
- 和上述类不同的是，在内存空间中的分配是不连续的，通过指针串联在一起
- 删除和插入时不需要进行移位，但查找效率较低

LinkedList<int> linlist1 = new LinkerList<int> ( );

LinkedListNode<int> node;

- 方法
  - AddFirst , AndLast , AndBefore , AndAfter ， 添加新结点


-----
堆栈

- Stack

*Stack st1 = new Stack ( )*

- 方法
  - Pop
  - Push
  - Peek 取栈顶元素
  - Count


-----
队列

- Queue

*Queue queue1;*

- 支持泛型

*Queue <int> queue1;*

二者所在命名空间不一样，取舍同上

- 方法
  - Enqueue
  - Dequeue
  - Peek 取栈顶元素
  - Count

