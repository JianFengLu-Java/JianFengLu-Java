# JavaWeb开发学习

### **Tomcat**

- 下载安装：访问Apache官网http://www.apache.org或者Tomcat官网http://tomcat.apache.org
- Mac OS>选择对应的版本，然后下载二进制tar.gz压缩包。
- 文件结构：
  - bin（Tomcat 的启动命令文件）
  - lib（Tomcat 的核心文件夹，存放的是Jar包）
  - conf（Tomcat 的配置文件夹，存放的各种xml配置相关的文件）
  - logs（Tomcat 的日志文件夹，存放服务器运行日志）
  - webapps（Tomcat的资源文件夹，存放开发的项目文件）

- **启动Tomcat方法：**

  - 在访达中访问Macintosh HD/Library/下新建Tomcat文件夹

  - 将解压的Tomcat文件夹复制到Library/Tomcat/文件夹下

  - 用终端访问Library/Tomcat/apache-tomcat-xxx.xx/bin

  - ```shell
    sudo chmod 755 *.sh //赋予sh管理员权限
    ```

  - 输入管理员密码

  - ```shell
    sh startup.sh //启动Tomcat
    sh shutdown.sh //关闭Tomcat
    ```

  - 当出现：

    ```shell
    Using CATALINA_BASE:   /Library/Tomcat/apache-tomcat-10.1.34
    Using CATALINA_HOME:   /Library/Tomcat/apache-tomcat-10.1.34
    Using CATALINA_TMPDIR: /Library/Tomcat/apache-tomcat-10.1.34/temp
    Using JRE_HOME:        /Users/lujianfeng/Library/Java/JavaVirtualMachines/graalvm-jdk-21.0.5/Contents/Home
    Using CLASSPATH:       /Library/Tomcat/apache-tomcat-10.1.34/bin/bootstrap.jar:/Library/Tomcat/apache-tomcat-10.1.34/bin/tomcat-juli.jar
    Using CATALINA_OPTS:   
    Tomcat started.
    ```

  - 说明Tomcat启动成功了

- **访问Tomcat**

  - 在浏览器中访问http://localhost:8080或http://127.0.0.1:8080
  - ![image-20241226000402141](/Users/lujianfeng/Library/Application Support/typora-user-images/image-20241226000402141.png)
  - 出现该界面说明Tomcat启动成功并可以成功访问了

### **在B/S架构系统当中存在的角色和协议**

- 在B/S架构中有：
  - Browser浏览器开发团队
  - Web Server服务器应用程序开发团队
  - Webapps程序开发团队
  - DB数据库开发团队
- 系统架构示意图：![image-20241226093631129](/Users/lujianfeng/Library/Application Support/typora-user-images/image-20241226093631129.png)

- **Browser**—request(HTTP)—>**WebServer**—Servlet(JavaEE)—>**WebApps**—JDBC—>**DBServer**

### **Servlet本质**

- SUN公司制定了Servlet接口规范

- Tomcat获取Browser发送的请求

- WebApps开发者实现了Servlet接口

  - UserListServlet.java   Implements Servlet 
  - UserLoginServlet.java   Implements Servlet
  - ...

- #### 那么是谁来决定，Tomcat获取到的URL和WebApps中的Java小程序对应起来呢？

- |  URL   |     Servlet      |
  | :----: | :--------------: |
  | /User  | UserListServlet  |
  | /Login | UserLoginServlet |
  |  /...  |       ...        |

  SUN公司？❌ Tomcat服务器？❌ **WebApps开发者！** ✅

- 对于JavaWEB开发者来说，我们可以指定一个配置文件，在配置文件中，描述请求和Servlet之间的对照关系。

### Servlet规范是一个什么规范？

- 遵循Servlet规范的WebApp，这个WebApp就可以放在不同的WEB服务器中运行
- Servlet中规范了哪些东西？
  - 规范了哪些接口
  - 规范了哪些类
  - 规范了Web应用中应该有哪些配置文件
  - 规范了Web应用中配置文件的名字
  - 规范了Web应用中配置文件存放的路径
  - 规范了Web应用中配置文件的内容
  - 规范了Web应用的文件目录结构是什么样的
  - ......

### 开发一个带有Servlet的WebApp（重点）

- 开发步骤是怎么样的？

  - 第一步：在**webapps**目录下新建一个目录，起名crm（crm是webapp的名字，也可以是其他项目）

    - 注意：这个crm目录就是web项目的根目录。

  - 第二步：在**crm**目录中创建:file_folder:**WEB-INF**目录（是Servlet中规范的**必须是大写**）

  - 第三步：在**WEB-INF**中新建一个文件夹->:file_folder:**classes**

    - 注意：这个文件夹要**必须全部小写**（Servlet中规范的），这个目录下存放的是Java程序编译之后的class文件（存放的字节码文件）

  - 第四步：在WEB-INF目录下新建📁lib

    - 注意：这个目录不是必须的，但如果一个Webapp需要用到第三方jar包的话，这个包就要放在lib目录下。

  - 第五步：在WEB-INF目录下新建文件📃web.xml

    这个文件是必须的，文件名必须叫web.xml，这个文件必须在这个位置，这个文件就是webapp的配置文件，它映射了URL路径和WebApp的Servlet实现类名的对应关系。

    这个文件最好从其他的WebApp中拷贝，最好不要手写，没必要。

    - ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      
      <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
                            https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
        version="6.0"
        metadata-complete="true">
      
      </web-app>
      ```

  - 第六步：编写一个Java程序，这个Java程序必须实现Servlet接口。

    - 这个Servlet接口不在JDK中。
    - Servlet接口（Servlet.class文件）是Oracle提供的另外一套类库。
    - Servlet是JavaEE规范中的一种。
    - Tomcat服务器实现了Servlet规范，所以Tomcat也需要使用Servlet接口。

  - 第七步：编译Java程序：HelloServlet.java得到class文件。

  - 第八步：将class文件移动到crm/WEB-INF/classes/下

  - 第九步：编写配置文件，在web.xml中描述“请求路径”与“Servlet全限定类名”关联在一起。

    - 这一步叫注册。

    - ```XML
      <?xml version="1.0" encoding="UTF-8"?>
      
      <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
                            https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
        version="6.0"
        metadata-complete="true">
        <!--Servlet描述信息
            servlet-name要一致,每个Servlet都对应一个ServletMapping-->
          <servlet>
            <servlet-name>ServletName</servlet-name>
            <!--这个必须是带包名的全限定类名-->
            <servlet-class>com.web.servlet.HelloServlet</servlet-class>
          </servlet>
      <!--Servlet映射信息-->
          <servlet-mapping>
            <servlet-name>ServletName</servlet-name>
            <!--URL需要以/开头-->
            <url-panttern>/hello</url-panttern>
          </servlet-mapping>
      
      </web-app>
      
      ```

  - 第十步：启动Tomcat服务器

  - 第十一步：使用浏览器访问URL。

  - 总结一下：

    ```
    合格的Webapp的目录结构：
    |------WEB-INF
    					|------classes
    					|------lib
    					|------web.xml
    |------Html
    |------Css
    |------JavaScript
    |------image
    ..
    ```

  - **浏览器发送请求到服务器程序调用Servlet类的方法，是怎么样的一个过程？**

  - 用户输入URL，或者直接点击超链接路径。

  - Tomcat接受到请求，截取到URL路径：/hello。

  - Tomcat服务器在web.xml文件中查找到对应<servlet-mapping>中对应的<servlet-name>标签，找到<servlet>对应的<servlet-class>找到类名。

  - Tomcat通过反射机制，创建<servlet-class>对象，然后调用对象中的service方法。

### 在集成开发环境中，开发Servlet程序

- 第一步：新建一个空的项目，然后往项目里添加模块Module

  - 不是必须，是一种习惯～

- 第二步：新建模块（file-->new-->module.. ）

- 第三步：将module变成JavaEE/JakartaEE模块

  - 双击Shift，输入''*Add Framework Support*''后选择Web Application OK后Idea会自动创建符合Servlet规范的Webapp目录结构，其中web文件夹就是这个webapp的根。

- 第四步（非必须）：根据Web Application 生成的文件中，删除index.jsp文件

- 第五步：编写Servlet：StudentServlet

  - class StudentServlet implement Servlet
  - 此时发现Servlet接口不在集成开发环境中，将CATALINA_HOME/lib/servlet-api.jar & jsp-api.jar添加到CLASSPATH（IDEA中的classpath）

- 第六步：在重写的service方法中编写业务代码。

- 第七步：在WEB-INF下新建目录：lib（目录名是固定的，不能乱改，并且将连接数据库的驱动包放在该目录下。）

- 第八步：在web.xml文件中完成注册Servlet。

- 第九步：在web文件夹下新建新的Html文件，给超链接，将请求路径放进去：

  ```Html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Student page</title>
  </head>
  <body>
  
      <a href="/amd/studentList">Student List</a>
  
  </body>
  </html>
  ```

- 第十步：让IDEA工具关联Tomcat服务器，关联过程中，将webapp部署到Tomcat服务器中。

  - 右上角的Edit Configurations,点击后找到Tomcat，配置服务器
  - 配置完服务器后关联web应用程序项目，并设置好项目根路径名。

- 第十一步：启动Tomcat

### Servlet对象的生命周期

- **什么是Servlet对象的生命周期？**

  - Servlet对象什么时候被创建。
  - Servlet对象什么时候被销毁。
  - Servlet对象被创建了几个。
  - 它的生命周期指代Servlet对象从出生到死亡的整个过程是怎么样的。

- **Servlet对象是由服务器来维护管理的**

  - Servlet对象的创建，对象上方法的调用，对象最终的销毁Webapp程序员是无权干预的。

  - Servlet对象的生命周期是由Tomcat服务器全权负责的。

  - Tomcat服务器又叫**Web容器**「Web Container」

  - Servlet被服务器创建之后，会被放进<HashMap>的一个集合中，它对应了URL请求路径和Servlet类名的关联关系。

  - | KEY  |           VALUE           |
    | :--: | :-----------------------: |
    | /crm | ClientRedisManagerServlet |
    |  /a  |         AServlet          |
    |  /b  |         BServlet          |

- **Servlet对象在Tomcat服务器启动的时候会被创建吗？**

  - 通过测试，发现Servlet对象在Tomcat服务器启动的周期**不会被创建**，而是在Tomcat第一次接收到路径请求时被创建，并调用无参构造方法。

- **如何让Servlet对象在Tomcat服务器启动的时候创建？**

  - 可以在web.xml文件中配置<servlet>，添加<Load-on-startup>标签，它的值是一个整数，*<u>[0,n)</u>*设置在多个Servlet对象时配置启动时创建的优先级～

  - **注意：一般情况下不用配置改该文件**

  - ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
             version="6.0">
        <servlet>
            <servlet-name>LifeCycle</servlet-name>
            <servlet-class>com.ljf.servlet.LifeCycleText</servlet-class>
            <load-on-startup>0</load-on-startup>
        </servlet>
        <servlet-mapping>
            <servlet-name>LifeCycle</servlet-name>
            <url-pattern>/life</url-pattern>
        </servlet-mapping>
    
        <servlet>
            <servlet-name>LifeCycle2</servlet-name>
            <servlet-class>com.ljf.servlet.LifeCycleTest02</servlet-class>
        </servlet>
        <servlet-mapping>
            <servlet-name>LifeCycle2</servlet-name>
            <url-pattern>/life2</url-pattern>
        </servlet-mapping>
    </web-app>
    ```

- #### 结论

  - Tomcat服务器启动时默认不会创建Servlet对象。
  - 用户在第一次发送请求后，Tomcat会创建Servlet对象（调用了对象的无参构造方法）。
  - 在创建Servlet对象后，立马调用了Servlet对象中的init方法，紧接着Tomcat执行完init后调用Servlet对象中的Service方法
  - Servlet对象是单例的，创建后便不再创建新的对象了～（Servlet类并不符合单例模式，这种情况称作假单例。是因为Servlet的创建WebApp程序员管不着）。
  - 无参构造方法、init方法只会在第一次请求的时候被调用一次。
  - 发送一次请求，service方法就会被调用一次。
  - destroy在服务器销毁对象内存之前会被调用一次。（类似于写遗书）:laughing:destroy方法执行之前Servlet对象还在，执行后对象会被销毁。

- **如果在Servlet中写了有参数的构造方法，无参构造方法被覆盖后，会在Tomcat服务器中导致一个HTTP：500的错误。**

  - 因为Tomcat找不到Servlet的无参构造方法了，无法实例化Servlet类。
  - 所以不建议在Servlet的实现类中写构造方法。
  - 我们可以选择将同样需求的代码写在init()方法中。（init方法可以报错，可以抛出、处理异常）。
  - 因为init()方法和构造方法同样，都是在对象第一次创建的时候执行，并且也是只执行一次。
  - Servlet规范了，不建议写构造方法，可以将代码写在init方法中
  - 在Servlet中最常用的就是service方法，是处理用户请求的核心方法。
  - 在init方法中，通常是做初始化操作，并且只做一次，例如：初始化数据库连接池、初始化线程池等。

- **什么时候使用destroy方法？**

  - 通常是在释放资源前，需要处理的操作，在destroy中进行。

- **我们直接实现Servlet接口有什么缺点？**

  - 大部分场景下我们只写service方法，其他方法是不需要使用的，代码不美观

- #### 适配器设计模式

- 「没有什么事是加一个中间件解决不了的」

  - 编写一个适配器，然后将常用的方法归成抽象方法
  
- **思考以下问题**

  - 继承了GeneralServlet类的子类还会调用init方法吗？
  
    - 会，会调用GeneralServlet中的init方法
  
  - init方法是谁调用的？
  
    - 是Tomcat调用的
  
  - init方法中的ServletConfig对象时谁创建的？是谁传过来的？
  
    - 是Tomcat干的
  
    - Tomcat服务器先创建了ServletConfig对象，然后再调用init方法，将创建的ServletConfig对象传过来
  
    - 思考一下Tomcat的模拟代码
  
      ```Java
      public class Tomcat{
        public static void main(String[] args){
          //Tomcat模拟代码。
          //创建Servlet对象
          Class clazz = Class.forName("com.ljf.servlet.LifeCycleText");
          Object obj = clazz.newInstance();
          //向下转型
          Servlet servlet = (Servlet)obj;
          //创建ServletConfig对象
          ServletConfig servletConfig = new ServletConfigImpl();
          //调用init方法
          servlet.init(servletConfig);
          
        }
      }
      ```
  
      

### 关于JavaEE的版本

- JavaEE目前最高版本是JavaEE8
- JavaEE被Oracle捐献给Eclipse了。
- Eclipse把JavaEE换名字了，以后叫做JakartaEE。
- <img src="/Users/lujianfeng/Library/Application Support/typora-user-images/image-20241228101710632.png" alt="image-20241228101710632" style="zoom: 50%;" />

解压Jar包的命令：

```bash
unzip xxxx.jar -d ./xxxx
```

