## Tomcat 安装与配置
- #### Tomcat 下载
  ##### 在官网 http://tomcat.apache.org/ 可以选择各种版本的 Tomcat 下载。在选好版本后，一般在选择 Core 类型的安装包。

  ![Tomcat下载](https://github.com/StRothschild/Tools/blob/master/resource/Tomcat%20%E2%80%94%20%E4%B8%8B%E8%BD%BD.png?raw=true)

- #### Tomcat 安装配置
  ##### 下载完 Tomcat 安装包后，解压至目标文件夹，则该文件夹就是 Tomcat 的安装目录。因为 Tomcat 是免安装的绿色软件。

  ##### 要启动 Tomcat 唯一需要配置的就是 JDK 和 JDK 的环境变量，因为 Tomcat 是基于 Java 开发的，需要依赖 JRE 环境。


- #### Tomcat 启动
  ##### 在配置好 JDK 及相关环境变量后，就可以启动 Tomcat。在 Tomcat 的安装目录下进入 /bin 目录，双击运行 startup.bat 脚本或者 tomcat7w.exe 可执行文件，即可启动 Tomcat。通过浏览器访问 localhost:8080 可以验证 Tomcat 是否启动。

  ##### 需要注意的是，在通过 tomcat7w.exe 可执行文件启动时，可能会有报错："指定的服务未安装"。此时，需要在 Tomcat 安装目录的 /bin 目录下执行命令：service.bat install 即可。


---
- #### Tomcat 依赖的环境变量
  ##### 1. CATALINA_HOME ：通过 CATALINA_HOME 来得到 bin 和 lib 目录，默认为 Tomcat 解压路径。
  ##### 2. CATALINA_BASE ：默认与 CATALINA_HOME 相同，路径下有 conf, logs, temp, webapps, work 等文件
  ##### 3. CATALINA_TMPDIR ：Web 应用运行过程中使用的临时目录
  ##### 4. JAVA_HOME ：提供 JRE 环境（必需）
  ##### 5. CLASSPATH

  ##### 以上 5 个依赖中只有 JAVA_HOME 是必需设置的。其他的都可以通过 CATALINA_HOME 默认获取。CATALINA_HOME 默认为 Tomcat 解压路径。



---
- #### Tomcat 端口
  ##### Shutdown port ： 此端口用于关闭Tomcat。当执行shutdown.sh脚本时，它会给此端口发出一个信号，Tomcat的进程会监听此端口，如果接收到这样的信号，进程会清理退出。
  ##### Connector port ：此端口是应用对外公开发布的端口。
  ##### ajp port ： Web服务器（例如 Apache 的 httpd Server 或者 Nginx）通过此端口和 Tomcat 进行通信，也可以使用它设置一个负载均衡服务器。
  ##### Redirect port ： 如果此 Connector 支持非SSL请求和接收SSL请求，Catalina会自动将请求指向到此端口。  




  ---
  - #### Tomcat 配置文件 server.xml
