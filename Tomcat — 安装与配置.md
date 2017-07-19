## Tomcat 安装与配置
- #### Tomcat 下载
  ##### 在官网 http://tomcat.apache.org/ 可以选择各种版本的 Tomcat 下载。在选好版本后，一般在选择 Core 类型的安装包。

  ![Tomcat下载](https://github.com/StRothschild/Tools/blob/master/resource/Tomcat%20%E2%80%94%20%E4%B8%8B%E8%BD%BD.png?raw=true)

- #### Tomcat 安装配置
  ##### 下载完 Tomcat 安装包后，解压至目标文件夹，则该文件夹就是 Tomcat 的安装目录。因为 Tomcat 是免安装的绿色软件。

  ##### 要启动 Tomcat 唯一需要配置的就是 JDK 和 JDK 的环境变量，因为 Tomcat 是基于 Java 开发的。


- #### Tomcat 启动
  ##### 在配置好 JDK 及相关环境变量后，就可以启动 Tomcat。在 Tomcat 的安装目录下选择 /bin 文件夹，双击运行 startup.bat 脚本或者 tomcat7w.exe 可执行文件，既可以启动 Tomcat。通过浏览器访问 localhost:8080 即可验证 Tomcat 是否启动。

  ##### 需要注意的是，在通过 tomcat7w.exe 可执行文件启动时，可能会有报错："指定的服务未安装"。此时，需要在 Tomcat 安装目录的 /bin 目录下执行命令：service.bat install 即可。
