String

是System.string类的别名，是引用类型。

- 创建String对象
  - 通过给 String 变量指定一个字符串
  - 通过使用 String 类构造函数
  - 通过使用字符串串联运算符（ + ）
  - 通过检索属性或调用一个返回字符串的方法
  - 通过格式化方法来转换一个值或对象为它的字符串表示形式

- String类的属性
  - Chars，在当前String对象中获取Char对象的指定位置
  - Length，在当前的String对象中获取字符数

- String类的方法
  - 字符串的比较
    - Compare ,Equals,==
  - 字符串的拼接
    - +,Format,Concat
  - 字符串的包含
    - Contains，IndexOf，IndexOfAny , LastIndexOf , StartsWith，EndsWith
  - 字符串的插入
    - Insert（生成一个新的字符串进行返回，对原字符串不影响）
  - 是否为空
    - IsNullOrEmpty
  - 移除
    - Remove
  - 替换
    - Replace
  - 切割
    - **public string\[\] Split( char\[\] separator, int count )**
    - **返回一个字符串数组，包含当前的 string 对象中的子字符串，子字符串是使用指定的 Unicode 字符数组中的元素进行分隔的。int 参数指定要返回的子字符串的最大数目，可缺省。**
  - 大小写转换
    - ToLower、ToUpper
  - 去掉前导空格和后置空格
    - Trim、TrimStart、TrimEnd



[https://www.runoob.com/csharp/csharp-string.html](https://www.runoob.com/csharp/csharp-string.html)



-----
StringBuilder

System.Text.StringBuilder 类

由于String 对象是不可改变的，每次使用 System.String 类中的方法之一时，都要在内存中创建一个新的字符串对象，这就需要为该新对象分配新的空间。在需要对字符串执行重复修改的情况下，与创建新的 String 对象相关的系统开销可能会非常昂贵。如果要修改字符串而不创建新的对象，应当使用该类来提升性能

- 设置容量和长度
  - StringBulider类是动态对象，允许扩充它所封装的字符串中字符的数量，但可以为其可容纳的最大字符值指定一个值，当实际字符数超过时，容量将自动扩大一倍，否则，它不会为自己重新分配空间
  - 通过重载的构造函数之一来指定类的容量
    - StringBuilder MyStringBuilder = new StringBuilder("Hello World!", 25);
  - 使用 Capacity 属性来定义对象的最大长度。
    - MyStringBuilder.Capacity = 25;

- StringBulider类的常用方法
  - Append 方法
    - 可用来将任意文本或字符串添加到由当前 StringBuilder 对象表示的字符串的结尾处。
    - MyStringBuilder.Append(" What a beautiful day.");
  - AppendFormat 方法
    - 可用来将标准格式的字符串添加到由当前 StringBuilder 对象表示的字符串的结尾处。
    - MyStringBuilder.AppendFormat("{0:C} ", MyInt);
  - Insert方法
    - 将字符串或对象添加到当前StringBulider中的指定位置
    - MyStringBuilder.Insert(6,"Beautiful ");
  - Remove 方法
    - 从当前StringBulider中移除指定数量的字符
    - MyStringBuilder.Remove(5,7);删除索引从5至7的字符
  - Replace 方法
    - 可以用另一个指定的字符来替换 StringBuilder 对象内的字符
    - MyStringBuilder.Replace('!', '?'); //将所有的！替换为？
  - 链式表达
    - StringBuilder MyStringBuilder = new StringBuilder("Hello Wo");
    - MyStringBuilder.Append(" r").Append(" l").Append(" d")；
    - 则对象变为 HelloWorld



-----
FileStream

System.IO.FileStream 类

用于文件的读写

- 类的创建
  - FileStream <object\_name> = new FileStream( <file\_name>，

  <FileMode Enumerator>, <FileAccess Enumerator>, <FileShare Enumerator>);

  - 例如，创建一个 FileStream 对象 F 来读取名为 sample.txt 的文件：

  FileStream F = new FileStream("sample.txt", FileMode.Open, FileAccess.Read, FileShare.Read);


- 构造函数的参数的枚举类型
  - FileAccess，设置文件的访问权限
    - Read：以只读方式打开文件。
    - Write：以只写方式打开文件。
    - ReadWrite：以读写方式打开文件。
  - FileMode，用于设置文件打开或创建的方式，
    - CreateNew：创建新文件，如果文件已经存在，则会抛出异常。
    - Create：创建文件，如果文件不存在，则删除原来的文件，重新创建文件。
    - Open：打开已经存在的文件，如果文件不存在，则会抛出异常。
    - OpenOrCreate：打开已经存在的文件，如果文件不存在，则创建文件。
    - Truncate：打开已经存在的文件，并清除文件中的内容，保留文件的创建日期。如果文件不存在，则会抛出异常。
    - Append：打开文件，用于向文件中追加内容，如果文件不存在，则创建一个新文件。
  - FileShare ，用于设置多个对象同时访问同一个文件时的访问控制，
    - None：谢绝共享当前的文件。
    - Read：允许随后打开文件读取信息。
    - ReadWrite：允许随后打开文件读写信息。
    - Write：允许随后打开文件写入信息。
    - Delete：允许随后删除文件。
    - Inheritable：使文件句柄可由子进程继承。
  - FileOptions， 用于设置文件的高级选项，包括文件是否加密、访问后是否删除等，
    - WriteThrough：指示系统应通过任何中间缓存、直接写入磁盘。
    - None：指示在生成 System.IO.FileStream 对象时不应使用其他选项。
    - Encrypted：指示文件是加密的，只能通过用于加密的同一用户账户来解密。
    - DeleteOnClose：指示当不再使用某个文件时自动删除该文件。
    - SequentialScan：指示按从头到尾的顺序访问文件。
    - RandomAccess：指示随机访问文件。
    - Asynchronous：指示文件可用于异步读取和写入。

- [http://c.biancheng.net/view/2928.html](http://c.biancheng.net/view/2928.html)


-----
StreamWriter、StreamReader

用于从流中读取字符串或写入字符串到流中

- StreamWriter
  - 构造方法
    |StreamWriter(Stream stream)|为指定的流创建 StreamWriter 类的实例|
|---------------------------|-------------------------|
    |StreamWriter(string path)|为指定路径的文件创建 StreamWriter 类的实例|
    |StreamWriter(Stream stream, Encoding encoding)|用指定的字符编码为指定的流初始化 StreamWriter 类的一个新实例|
    |StreamWriter(string path, Encoding encoding)|用指定的字符编码为指定的文件名初始化 StreamWriter 类的一个新实例|

  - 属性或方法
    |bool AutoFlush|属性，获取或设置是否自动刷新缓冲区|
|--------------|-----------------|
    |Encoding Encoding|只读属性，获取当前流中的编码方式|
    |void Close()|关闭流|
    |void Flush()|刷新缓冲区|
    |void Write(char value)|将字符写入流中|
    |void WriteLine(char value)|将字符换行写入流中|
    |Task WriteAsync(char value)|将字符异步写入流中|
    |Task WriteLineAsync(char value)|将字符异步换行写入流中|


  

- StreamReader
  - 构造方法
    |StreamReader(Stream stream)|为指定的流创建 StreamReader 类的实例|
|---------------------------|-------------------------|
    |StreamReader(string path)|为指定路径的文件创建 StreamReader 类的实例|
    |StreamReader(Stream stream, Encoding encoding)|用指定的字符编码为指定的流初始化 StreamReader 类的一个新实例|
    |StreamReader(string path, Encoding encoding)|用指定的字符编码为指定的文件名初始化  StreamReader 类的一个新实例|

  - 属性或方法

  
    |Encoding CurrentEncoding|只读属性，获取当前流中使用的编码方式|
|------------------------|------------------|
    |bool EndOfStream|只读属性，获取当前的流位置是否在流结尾|
    |void Close()|关闭流|
    |int Peek()|获取流中的下一个字符的整数，如果没有获取到字符， 则返回 -1|
    |int Read()|获取流中的下一个字符的整数|
    |int Read(char\[\] buffer, int index, int count)|从指定的索引位置开始将来自当前流的指定的最多字符读到缓冲区|
    |string ReadLine()|从当前流中读取一行字符并将数据作为字符串返回|
    |string ReadToEnd()|读取来自流的当前位置到结尾的所有字符|




-----
Directoryinfo类

用于文件夹的操作

- 类的创建
  - DirectoryInfo(string path)
  - 例如创建路径为 D 盘中的 test 文件夹的实例，代码如下。

  DirectoryInfo directoryInfo = new DirectoryInfo("D:\\\\test");

  - 需要注意的是路径中如果使用 \\，要使用转义字符来表示，即\\\\ ，或者在路径中将 \\ 字符换成 /

- 类的属性和方法
  |Exists|只读属性，获取指示目录是否存在的值|
|------|-----------------|
  |Name|只读属性，获取 Directorylnfo 实例的目录名称|
  |Parent|只读属性，获取指定的子目录的父目录|
  |Root|只读属性，获取目录的根部分|
  |void Create()|创建目录|
  |DirectoryInfo CreateSubdirectory(string path)|在指定路径上创建一个或多个子目录|
  |void Delete()|如果目录中为空，则将目录删除|
  |void Delete(bool recursive)|指定是否删除子目录和文件，如果 recursive 参数的值为 True，则删除，否则不删除|
  |IEnumerable<DirectoryInfo>  EnumerateDirectories()|返回当前目录中目录信息的可枚举集合|
  |IEnumerable<DirectoryInfo>  EnumerateDirectories(string searchPattern)|返回与指定的搜索模式匹配的目录信息的可枚举集合|
  |IEnumerable<FileInfo> EnumerateFiles()|返回当前目录中的文件信息的可枚举集合|
  |IEnumerable<FileInfo> EnumerateFiles(string searchPattern)|返回与搜索模式匹配的文件信息的可枚举集合|
  |IEnumerable<FileSystemInfo>  EnumerateFileSystemInfos()|返回当前目录中的文件系统信息的可枚举集合|
  |IEnumerable<FileSystemInfo>  EnumerateFileSystemInfos(string searchPattern)|返回与指定的搜索模式匹配的文件系统信息的可枚举集合|
  |DirectoryInfo\[\] GetDirectories()|返回当前目录的子目录|
  |DirectoryInfo\[\] GetDirectories(string searchPattern)|返回匹配给定的搜索条件的当前目录|
  |FileInfo\[\] GetFiles()|返回当前目录的文件列表|
  |FileInfo\[\] GetFiles(string searchPattern)|返回当前目录中与给定的搜索模式匹配的文件列表|
  |FileSystemInfo\[\] GetFileSystemInfos()|返回所有文件和目录的子目录中的项|
  |FileSystemInfo\[\] GetFileSystemInfos(string searchPattern)|返回与指定的搜索条件匹配的文件和目录的子目录中的项|
  |void MoveTo(string destDirName)|移动 DirectoryInfo 实例中的目录到新的路径|




- [http://c.biancheng.net/view/2915.html](http://c.biancheng.net/view/2915.html)
- Directory类，静态类，省去了创建实例的过程，可以直接使用

