# OpenJDK-11

> **Read the fucking source code**

记录阅读源码的心得体会。

## 项目介绍
`OpenJDK-11`源码，可供阅读学习使用。

* `src`目录存放OpenJDK-11源码。阅读过程中产生的笔记以注释的形式直接写在源码文件中。
* `test`目录存放源码阅读过程中写的一些测试文件，使用时可将相关文件复制到新建项目中。

## 源码版本                                                   
> **openjdk version "11" 2018-09-25**
>
> **OpenJDK Runtime Environment 18.9 (build 11+28)**
>
> **OpenJDK 64-Bit Server VM 18.9 (build 11+28, mixed mode)**

## 使用说明
1. 该源码主要除了包括`src.zip`里提供的源码，此外还包括一部分未公开的源码。
   
   该源码**不支持**直接编译。如想完整编译整个`OpenJDK`项目，请自行到`OpenJDK`项目官网下载完整的工具链。
   
2. 此源码与`Oracle JDK`源码并非完全一致。
   
   `Oracle JDK`仅开源了一部分代码。想深入学习JDK的话建议阅读此源码。

3. 源码原本采用了`JDK 9`之后的`module`模块系统组织，此处修改为熟悉的包组织形式，以便阅读。

4. 因为本源码已经包含了`OpenJDK`中绝大多数公开的源码，所以**不建议**再为此项目重复关联JDK，因为这会造成在代码跳转中，跳转到关联JDK的源码中而不是直接跳转到本项目的源码中。
   
   此外，本项目还有一些源码是JDK里不提供的，所以关联了JDK可能会导致报错信息，提示找不到相关的代码。
   
   如果出于某些特殊需要必须关联JDK，建议在Project Structure->Project Settings->Modules->Dependencies选项卡下调整源码识别优先级，将\<Module source\>调整到列表首位，可以使得源码跳转中优先跳转到本项目自身的源码里。

5. 由于时间关系，本人未对所有代码一一测试。所以，如果因为某个源文件异常或缺失而导致IDE报警告信息或者报错误提示的话，解决方案有两个：
   * 如果代码对你很重要，影响到你对某个方法的理解，请自行到Google搜索相关源文件导入到项目中合适的位置，或作为依赖库关联到项目中，比如部分源码需要关联Junit4测试库。    
   * 如果仅仅是因为显示的异常信息造成了视觉上的干扰，请在IDE中自行设置语法高亮形式。比如在IDEA中阅读此项目时，我会关闭Settings->Editor->Color Scheme->General中关于错误、警告、非法符号的报错提示，并且关闭Settings->Editor->Inspections处的语法检测信息。（当然，这两个地方的设置均支持备份与自定义，所以建议不要直接在原设置上修改，而是新建一份设置再去修改比较好，以方便在不同项目之间切换规则）

6. **欢迎反馈好的想法、建议、意见。**

## Commit图例

| 序号 | emoji | 在本项目中的含义 |
| ---- | ----- | --------------- |
| (0) | :tada: | 初始化项目 |
| (1) | :memo: | 更新README，或更新.gitignore |
| (2) | :bulb: | 完成阅读，该类/接口中的方法已读完，实现过程已看懂 |
| (3) | :bulb::clown_face: | 基本完成阅读，细节待完善，涉及到了一部分目前没接触过的类 |
| (4) | :construction::sparkles: | 阅读进行中，掌握了一部分特性，后续还需继续阅读 |
| (5) | :construction::speech_balloon: | 阅读进行中，处于了解阶段，大概知道该类的作用，原理还不大清楚，后续还需继续完善 |
| (6) | :sparkles: | 在(4)(5)的基础上补充新内容 |
| (7) | :recycle: | 重构代码，主要是修改之前的阅读笔记，极少情形下会修改源码 |
| (8) | :pencil2: | 更正错别字、调节不合理的分组、修改源码排版 |
| (9) | :white_check_mark: | 发布测试文件 |

## 相关链接

[OpenJDK-11官网](http://jdk.java.net/11/)

[OpenJDK存档-第三方网站](https://adoptopenjdk.net/?variant=openjdk11&jvmVariant=hotspot)


## 脚注

Commit信息中的emoji取自[gitmoji](https://gitmoji.carloscuesta.me/)。

## 附录

#### 测试文件简介
* VoidTest - java.lang.Void
  * `VoidTest01` Void在反射中的使用
  * `VoidTest02` Void在泛型中的使用
* StringCharacterIteratorTest - java.text.StringCharacterIterator
  * `StringCharacterIteratorTest01` 双向遍历String
* BreakIteratorTest - 分词器对字符、单词、行、语句的分割
  * `BreakIteratorTest01` 分词器对字符(Unicode符号)的分割
  * `BreakIteratorTest02` 分词器对单词的分割
  * `BreakIteratorTest03` 分词器对行的分割
  * `BreakIteratorTest04` 分词器对句子的分割
* ByteOrderTest - 当前系统字节顺序
  * `ByteOrderTest01` 查看当前系统存储数据用的是大端法还是小端法
* UnsafeTest - 测试Unsafe类常用操作，注意设置JDK>=8或OpenJDK>=9
  * `UnsafeTest00` 获取Unsafe实例，并借助Unsafe创建其他类的对象
  * `UnsafeTest01` 获取字段地址，获取字段地址处的值，为某地址处的字段赋值
  * `UnsafeTest02` 对JVM内存中某对象的数组字段/变量直接操作
  * `UnsafeTest03` 本地内存操作
  * `UnsafeTest04` 利用Unsafe#objectFieldOffse方法获取某个对象的近似大小
  * `UnsafeTest05` 线程的阻塞[park]与唤醒[unpark]
  * `UnsafeTest06` 获取静态字段所属的类对象
* ReferenceTest - 软引用、弱引用、虚引用测试
  * `ReferenceTest01` 软引用SoftReference回收测试
  * `ReferenceTest02` 弱引用WeakReference回收测试
  * `ReferenceTest03` 虚引用PhantomReference回收测试
* CleanerTest - 清洁器测试
  * `CleanerTest01` 创建Cleaner，注册追踪的对象和回调动作
* StreamTest - 流
  * `StreamTest01` Stream的简单使用
  * `StreamTest02` filter测试
  * `StreamTest03` map测试
  * `StreamTest04` flatMap测试
  * `StreamTest05` peek测试
  * `StreamTest06` distinct测试
  * `StreamTest07` sorted测试
  * `StreamTest08` limit测试
  * `StreamTest09` skip测试
  * `StreamTest10` Stream短路操作测试
  * `StreamTest11` Optional测试
  * `StreamTest12` forEach测试
  * `StreamTest13` reduce测试
  * `StreamTest14` min和max测试
  * `StreamTest15` count测试
  * `StreamTest16` collect测试
  * `StreamTest17` Collector（收集器）测试
* SystemTest - java.lang.System
  * `SystemTest01` 标准流
  * `SystemTest02` 属性
  * `SystemTest03` 日志
  * `SystemTest04` 环境变量
* ObjectTest - java.lang.Object
  * `ObjectTest01` 测试wait释放锁的行为
  * `ObjectTest02` 测试wait和notify的配套使用
* ThreadTest - 线程核心操作
  * `ThreadTest01` 测试守护线程的行为
  * `ThreadTest02` 中断非阻塞线程
  * `ThreadTest03` 中断阻塞线程
  * `ThreadTest04` 死锁线程无法被中断唤醒
