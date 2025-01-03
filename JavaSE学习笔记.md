# 01->String类

[TOC]

------

### String类中的常用方法（也可以参考API文档）

- char charAt(int index):返回索引处的char值。

  ```JAva
  String a = "abc";
  char c = a.charAt(2);//返回值类型为char；
  System.out.println(c);//c
  ```

- int length():获取字符串的长度。

  ```Java
  String a = "abc";
  int i = a.length();
  System.out.println(i);//3
  ```

- boolean isEmpty():判断字符串是否是空字符串，如果length()为0，就是空字符串。

  ```Java
  String a = "";
  System.out.println(a.isEmpty());//true
  ```

- boolean equals(String s):判断两个字符串是否相等。

  ```Java
  String a = "123";
  String b = "123";
  System.out.println(a.equals(b));//true
  ```

- boolean equalsIsIgnoreCase(String s1):判断两个字符串是否相等，忽略大小写。

  ```Java
  String bigWord = "ABC";
  String littleWord = "abc";
  System.out.println(bigWord.equalsIsIgnoreCase(littleWord));//true
  ```

- boolean contains(CharSequence s):判断字符串中是否包含某个子字符串。

  ```
  String a = "123456";
  String b = ""234;
  System.out.println(a.contains(b));//true
  ```


------

# 基本数据类型&包装类

| 基本数据类型 |      对应包装类       |
| :----------: | :-------------------: |
|    `byte`    |   `java.lang.Byte`    |
|    `char`    | `java.lang.Character` |
|    `int`     |  `java.lang.Integer`  |
|   `short`    |   `java.lang.Short`   |
|    `long`    |   `java.lang.Long`    |
|   `float`    |   `java.lang.Float`   |
|   `double`   |  `java.lang.Double`   |
|  `boolean`   |  `java.lang.Boolean`  |

**包装类属于引用类型，为了方便开发**

- 如果在调用的方法里传的参数是Object类型的对象，则没有办法传入参数了，所以现在需要将数据包装成Object类型

- ```java
  public class IntegerTest01{
    public static void main(String[] args){
      //定义要传的值
      int value = 10;
      MyInteger integer = new MyInteger(value);
      method(integer);
    }
    
    public void method(Object obj){	
      //这里的参数是Object类型，但是我要将int数据传进来，该怎么做呢？
    	//将int基本类型数据包装成Object类，再传进来～
      //然后将Object类对象向下转型成MyInteger对象
      MyInteger myInteger = (MyInteger)obj;
      //再调用getValue()方法
      System.out.pringln(myInteger.getValue());
    }
  }
  ```

  ```java
  public class MyInteger{
    //这个类是默认集成所有类的老祖宗：Object基类的。
    //所以这个int值传进来以后，它就被包装成一个Object类的对象了。
    private final int value;
    public MyInteger(int value){
      this.value = value;
    }
    //提供set、get方法访问成员变量
    public int getValue(){
      return value;
    }
    
    public void setValue(int value){
      this.value = value;
    }
  }
  ```

- 包装类的实现原理⬆️

### 装箱与拆箱

#### 拆箱(unboxing)

- Byte、Short、Integer、Long...等六个数字型包装类都继承了Number类

- 因此这些类中都有以下方法

  | Method                   |
  | ------------------------ |
  | byteValue()-> `byte`     |
  | shortValue()-> `short`   |
  | intValue()-> `int`       |
  | longValue()-> `long`     |
  | floatValue()-> `float`   |
  | doubleValue()-> `double` |

  这些方法的作用是将**包装类型数据**转换成**基本类型数据**，调用以上六个方法中任何一个都叫<u>*‘拆箱’*</u>

- Boolean的拆箱方法是：booleanValue()
- Charaction的拆箱方法是：charValue()
- 

### UUID

- 工具类java.util.UUID
- UUID是一种软件构建标准，用来生成具有唯一性的ID
- UUID具有以下特点：
  - UUID可以在分布式系统中生成唯一标识符，避免因主键冲突等造成的问题带来的麻烦。
  - UUID具有足够的唯一性，重复的概率相当低，UUID使用的是128位数字
  - UUID在生成时不依赖任何中央控制器或者数据库服务器，可以在本地方便快捷的生成唯一标识符
  - UUID生成后可以被许多其他的编程语言支持，并方便的转化为字符串的形式表示，适用于多种应用场景。
  - 在Java开发中，UUID的作用非常广泛，可以用于生成数据表主键，场景标识符、链路追踪、缓存key等
- 使用：
  - 生成UUID: static UUID randomUUID();
  - 将UUID转换为字符串:  String toString();
