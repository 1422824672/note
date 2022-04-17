## SpringMVC学习笔记



### 一、MVC模式

>MVC 模式最早由 Trygve Reenskaug 在 1978 年提出 ，是施乐帕罗奥多研究中心（Xerox PARC）在 20 世纪 80 年代为程序语言Smalltalk 发明的一种软件设计模式。MVC 模式的目的是实现一种动态的程序设计，使后续对程序的修改和扩展简化，并且使程序某一部分的重复利用成为可能。除此之外，此模式通过对复杂度的简化，使程序结构更加直观。软件系统通过对自身基本部分分离的同时也赋予了各个基本部分应有的功能。专业人员可以通过自身的专长分组开发。

​	从名称中可以看出，MVC模式由三部分组成，分别是M(Model)、V(View)、C(Controller)。

​	M指的是业务模型业务数据这些，通俗一点说就是一个映射的载体对象，M层是一个pojo(Plain Ordinary Java Object)类,例如数据库有一张学生表，里面有学号、姓名、班级，那么对应的pojo类里面也会有这三个属性的学号、姓名、班级，并包含其getter和setter方法，如下所示。



- 数据库中对应的学生表

  | s_number  | name | classname    |
  | --------- | ---- | ------------ |
  | 191205201 | 张三 | 软件工程一班 |
  | 191205202 | 李四 | 软件工程一班 |
  | 191205203 | 王五 | 软件工程一班 |

- pojo类

```java
public class Student {
    private String sNumber;//对应了这个学生的学号

    private String name;//对应了这个学生的姓名

    private String className;//对应了这个学生的班级

    public String getsNumber() {
        return sNumber;
    }

    public void setsNumber(String sNumber) {
        this.sNumber = sNumber;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getClassName() {
        return className;
    }

    public void setClassName(String className) {
        this.className = className;
    }
}
```



​	V指的是就是用户界面，也就是每个用户所看到的，所绘制出来的界面，把数据和业务呈现给用户，浏览网页时你看到的网页，就是View层所绘制的。



​	C指的是控制器，它本身不输出任何东西，它在接受到用户的请求后，它负责调用哪个模型(M)，返回哪个视图(V)，做到一个调度的作用。它就像一个遥控器，用户按哪个频道，他就通过调度，返回用户想要的。



### 二、SpringMVC

#### 1.SpringMVC简介

​	SpringMVC全称是 Spring Web MVC，它是基于Servlet构建的原始Web框架，它从一开始就包含在Spring框架中，它基于MVC设计模式实现。

#### 2.DispatcherServlet

​	SpringMVC是围绕着前端控制器来设计实现的，那什么是前端控制器呢？前端控制器模式（Front Controller Pattern）是用来提供一个集中的请求处理机制，所有的请求都将由一个单一的处理程序处理，我觉得可以理解成又加了一层，通过这层来实现中央调度，也就是我们常说的没有什么是加一层实现不了的。

​	DispatcherServlet就是这么一个东西。接下来看看DispatcherServlet的继承结构图，其继承结构图如下图所示。

![image-20220410140639840](C:\Users\BaiQingyang\AppData\Roaming\Typora\typora-user-images\image-20220410140639840.png)

​	不难看出，DispatcherServlet可以说它是实现了Servlet接口，那既然是Servlet，那它就需要用Java类配置的方式或者在web.xml中根据Servlet的规范来进行声明和映射，这里配置方面的代码就不过多介绍了，官方文档上写的很清晰，两种方式的配置文档都有。

#### 3.SpringMVC核心架构

​	其核心架构图如下图所示。

![](D:\File\photos\临时图片\springmvc架构图.png)



下面举一个小例子来比喻一下（以括号内容为准，例子可能会不妥，接受程度因人而异）：

1. 张三去办事大厅想要办件事（用户向服务器发送请求，被前端控制器接收请求）
2. 办事员根据张三的要求去翻阅手册，看看这件事应该找谁去办（前端控制器根据请求向处理器映射器查询对应的Handler）
3. 办事员翻阅完手册，明白了办好这件事的流程（返回需要执行的Handler链）
4. 办事员又根据张三的要求去向办事处请求办理这件事情（前端控制器继续根据请求去向处理器适配器请求执行相应的方法）
5. 办事处找到了相应人员处理这件事（处理器适配器调用相应的Handler，Handler返回ModelandView对象）
6. 办事处办理好了事情（处理器适配器将ModelandView对象返回给前端控制器，前端控制器根据返回的ModelandView对象去向视图解析器请求解析视图）
7. 办事处将办理好的事情整理成文件交给办事员，就差盖章（绘制视图）了，这样就可以交给张三了（视图解析器解析完将View对象返回给前端控制器）
8. 9.10.11. 办事员根据文件找到了盖章处，盖好了章之后，办事员把这个文件交给了张三，张三的事情办完了（前端控制器通过View对象和Model对象来渲染视图，最后响应给用户）

本次学习就到这里，欢迎大家批评和修正。