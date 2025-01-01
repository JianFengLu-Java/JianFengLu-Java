# 01->String类

##### String类中的常用方法（也可以参考API文档）

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
    private int value;
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

  

###### 
